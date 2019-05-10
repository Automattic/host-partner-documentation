# Migrating from version 1.2 to version 1.3

Migrating your existing integration from version 1.2 of the Jetpack Start API to version 1.3 will allow you to take advantage of improved speed, improved UX, and features that are only available in version 1.3.

A number of things have changed between versions 1.2 and 1.3. This document will attempt to cover the high-level changes between versions 1.2 and 1.3, but please be aware that there may be some nuances that are covered in detail outside of this migration document. Please consult the rest of the [Jetpack](./) documentation to get more in-depth description of the functionality in version 1.3.

## Understanding the flows

Before we discuss how to migrate from version 1.2 to 1.3, let's take a moment to understand the provisioning process of each version of the API.

### Version 1.2 integration flow

Below is a high-level diagram of the version 1.2 integration flow.

![Jetpack version 1.2 flow diagram](/assets/jps-v1-2-overview.png)

There are a few key things which we'll point out from this diagram:

- A WordPress.com oAuth token from the user is required to call the endpoint
  - This requires sending users through the WordPress oAuth flow
  - This also requires that users have, or create, a WordPress.com account
  - In some cases, the oAuth token may not be accepted if the site is already connected to another WordPress.com user
- The host is required to set many values via WP-CLI or some other method to activate and setup Jetpack, Akismet, and VaultPress

### Version 1.3 integration flow

Below is a high-level diagram of the version 1.3 integration flow.

![Jetpack version 1.3 flow diagram](/assets/jps-v1-3-overview.png)

At first glance, you may notice that the diagram for version 1.3 is more complex. That's because version 1.3 of the API is definitely more complex beneath the hood. But, I'll point out that much of that complexity is hidden "under the hood".

From the hosting partner's perspective, we believe the integration is actually much simpler for the following reasons:

- oAuth is not required before calling the API
- If a user does not already exist on WordPress.com then the API will attempt to create the user and connect the site automatically (if the partner is whitelisted)
- The host does not have to run WP-CLI commands to install Akismet and VaultPress
- The host does not have to run WP-CLI commands to set key for Jetpack, Akismet, and VaultPress

We created version 1.3 with the goal of making the integration process simpler for hosting partners. Now, hosting partners should only have to:

1. Make an API request to the `/v1.3/jpphp/provision` endpoint with the following information:
   - Site URL
   - User ID, email, or username
   - The plan to provision to the site
2. Choose whether to redirect the user based on the response from the API
   - If the API returns a response that includes `auth_required: true`, then the user will need to connect their Jetpack site
   - In this case, a `next_url` value should be returned, if possible, which will allow the user to connect their site to WordPress.com
   - Alternatively, the user can click the "Set Up Jetpack" button within WordPress.com to go through the connection process and then receive their plan

## Doing the migration

With the above in mind, let's go over the changes for migration.

### Base URL

The base URL has changed from the `https://public-api.wordpress.com/rest/v1.2` to `https://public-api.wordpress.com/rest/v1.3`.

### Endpoint

The endpoint paths have changed from `/product-keys` in version 1.2 to `/provision` in version 1.3.

### oAuth flow no longer needed

Version 1.3 no longer user oAuth tokens from user, so you can completely remove the WordPress.com oAuth flow from your provisioning process if you'd like.

### Jetpack is required to be installed and active

In version 1.3 of the Jetpack Start API, Jetpack is required to be installed and active when making a call to the `/v1.3/jpphp/provision` endpoint so that the WordPress.com API can communicate back to the Jetpack site. This was not the case for version 1.2 of the API.

### CLI calls minimized

Version 1.3 of the Jetpack Start API now remotely installs and configures Akismet and VaultPress via an API call from WordPress.com to the Jetpack site.

Because of this, you can remove all of the WP-CLI calls that you previously ran to:

- Install Akismet
- Install VaultPress
- Set keys for Akismet, VaultPress, and Akismet

### Handling successful provision requests

There are three cases of a successful API response to consider how to handle for the integration.

#### Authorization is not required

In this case, you can expect a response like this:

```json
{
    "success": true,
    "next_url": "https://example.com/wp-login.php?action=jetpack-sso&redirect_to=https%3A%2F%2Fexample.com%2Fwp-admin",
    "auth_required": false
}
```

In this case the plan has already been provisioned to the site and no further action is required. The `next_url` value, in a default configuration, should be a Jetpack Secure Sign On link that will automatically log the user in to the `wp-admin` of their site. That being said, it is not required to redirect the user anywhere.

#### Authorization is required and next URL is not empty

In this case, you can expect a response like this:

```json
{
    "success": true,
    "next_url": "https://jetpack.wordpress.com/jetpack.authorize/1/...",
    "auth_required": true
}
```

In this case, the plan has not yet been added to the Jetpack site yet, but a pending activation has been registered for the site on WordPress.com. For the site to receive the plan that you have attempted to provision to them, the site must connect to WordPress.com.

The `next_url` value is a URL at which the user can connect their site to WordPress.com and then be provisioned the plan that was set in the pending activation. That being said, the `next_url` is provided for convenience. You can choose to redirect the user to this URL or display it somehow in your dashboard, but it is not a hard requirement that the user go to this `next_url` value. Instead, the user can also click the "Set Up Jetpack" button that appears in their `wp-admin`.

Note: Hosting partners are not charged for pending activations where a plan is a plan was never provisioned. Hosts are only charged for active plans. Therefore, only after a user connects the WordPress.com site.

Note: Pending activations are only valid for two weeks. Afterwards, another request will need to be made to the provisioning API to provision a plan for a given site.

#### Authorization is required and next URL is empty

In this case, you can expect a response like this:

```json
{
    "success": true,
    "next_url": "",
    "auth_required": true
}
```

This case is very similar to the one above directly above, the only difference being that the `next_url` value is empty. This is a very specific use case where hosting partners are provisioning plans to sites where the DNS has not yet propagated. In this case, we choose to register a pending activation for a given URL, but we are not able to populate the `next_url` since we're not able to communicate to the site.

In this case, the hosting partner is not able to automatically redirect the user to the `next_url` value in order to have the user go throug the Jetpack connection process. Instead, the hosting partner must rely on the user clicking the "Set Up Jetpack" button in the `wp-admin` of their site.