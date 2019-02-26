# Method Not Found Errors

When calling the [Jetpack provisioning API directly](plan-provisioning-direct-api.md), one side-effect is an increase in communication between WordPress.com/Jetpack servers and the remote site that a hosting partner maintains.

The primary reason that this communication is necessary is that we require a site to be connected to WordPress.com/Jetpack before a plan can be provisioned to that site. The extra communication handles an initial registration of the site as well as setting secrets and gathering information necessary to create an authorization URL so that a user may authorize a connection between WordPress.com/Jetpack and their site.

One side-effect of this extra communication is that it increases the possibilities that something can go wrong. The most common and confusing issues that occur with this extra communication are errors with code `method_not_found`. Below, I'll go over the cases where a `method_not_found` error may occur as well as options for fixing the issue.

## remoteRegister Not Found

An example response of what you'll get back from this specific `method_not_found` error is:

```
{
  "error": "method_not_found",
  "message": "remoteRegister method not found on remote site."
}
```

Here are the known cases for this error as well as suggested solutions.

### Jetpack is not installed and active

If Jetpack is not installed and active then the `jetpack.remoteRegister` method is never add to the list of available XML-RPC methods. The simplest fix here is to simply install and activate Jetpack. You can do that via WP-CLI:

```
wp plugin install jetpack
wp plugin activate jetpack
```

Note: The `bin/partner-provision.sh` script that is packaged in the Jetpack plugin will attempt to silently active the Jetpack plugin before calling to the API. So, installing the Jetpack plugin and then calling the `bin/partner-provision.sh` script is an alternative to fix this error as well.

### Site uses https but https not specified in siteurl argument

For some hosting partners, this error has occurred when passing only the domain, or the host portion of the url. This typically work fine since we run `esc_url_raw()` on the WordPress.com/Jetpack side to get a proper URL to call out to. But, in the case of one hosting partner, where the site automatically redirect `http` to `https`, the `method_not_found` error was returned.

One fix in this case is to pass the full URL with the correct protocol in the `siteurl` argument. We will consider options for improving this on the WordPress.com/Jetpack side in the future.

## remoteProvision Not Found


An example response of what you'll get back for this specific `method_not_found` error is:

```
{
  "error": "method_not_found",
  "message": "remoteProvision method not found on remote site. Try calling again with --force_register=true."
}
```

This error usually occurs because there is a mismatch in tokens between the WordPress.com/Jetpack side and the site that is hosted with the hosting partner. Specifically, there is a blog token on the WordPress.com/Jetpack side but there is not a matching token on the hosted site. Some reasons that this error might have occurred are:

1. The site was disconnected but the call to WordPress.com/Jetpack failed
1. The `jetpack_options` and/or `jetpack_private_options` options were deleted

The recommended solution for this issue is to pass `force_register=1` in direct calls to the API or `--force_register=true` when running the `bin/partner-provision.sh` script.

In the past, some hosting partners have asked if they could always set `force_register` to true. In our experience, this does work. But, it does slow down the request by adding at least one network request.
