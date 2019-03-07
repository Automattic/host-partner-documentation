# WooCommerce Integration Overview

The WooCommerce `host-plan` endpoints are used to provision either a single extension or a bundle of extensions to a given site and user. The extensions that a host partner may provision are defined in what we call a package. This package is unique to a partner and is guarded by a pre-shared secret key that is sent along with requests. This pre-shared secret key is unique to each package, so a given host may have multiple keys if that host is provisioning from multiple packages.

Below, we'll go over the various integration steps that a hosting partner will need to implement.

1. **Registration**

   Once a new customer data (email, first name, last name, and site URL) is available
   from plan registration, a request to WooCommerce.com [register](plan-register.md) endpoint
   must be made. If site URL is not ready or not propagated yet, it's fine to send
   temporary URL. There's another endpoint to [update](update-url.md) a site's URL.

   The response from the register endpoint is important as it is used for establishing a connection between the customer's site and WooCommerce.com as well as in follow-up requests to manage the provisioned package. For example:

   - Cancellation request requires `order_id` parameter.
   - Updating site URL request requires `access_token` and `access_token_secret`.

    To save the response in the customer's site options:

   ```php
   <?php
   WC_Helper_Options::update(
       'auth',
       array(
           'access_token'        => $response['access_token'],
           'access_token_secret' => $response['access_token_secret'],
           'site_id'             => $response['site_id'],
           'user_id'             => $user_id, // This is the ID of the user on the customer's site, which is usually 1.
           'updated'             => time(),
       )
   );
   ```

   **Note** `WC_Helper_Options` is available when WooCommerce is activated.

   **Note** See [Considerations for WP-CLI](management-via-wp-cli.md#considerations-for-using-wp-cli) if you will be running the above via WP-CLI.

   Documentation can be found [here](plan-register.md). For an overview of the flow see the following flowchart:

   ![WooCommerce registration flow](/assets/woocommerce-register-flow-chart.png)

1. **Cancellation**

   Once a WPCOM plan is expired, a request to the WooCommerce.com [cancel](plan-cancel.md) endpoint
   must be made. This will cancel the order created from the registration request and
   revoke all subscription keys for the extensions (customers still able to use
   the extension, but no update and support from WooCommerce.com will be given
   for those extensions).

   Documentation can be found [here](plan-cancel.md).

1. **Update URL**

   Update a customer site URL for a WooCommerce.com-connected site.

   Documentation can be found [here](update-url.md).

1. **Package/Product Information**

   Get information about products in a package / host plan. Response includes latest version and download URL to our internal repository, and as such, that makes these endpoints important for ensuring that a hosting partner is installing the latest WooCommerce products from their package.

   Documentation can be found [here](product-info.md).
