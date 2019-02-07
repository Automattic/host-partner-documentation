## Host Integration Guide

### WPCOM

1. **Registration**

   Once a new customer data (email, first name, last name, and site URL) is available
   from plan registration, a request to WooCommerce.com [register](#register) endpoint
   must be made. If site URL is not ready or not propagated yet, it's fine to send
   temporary URL. There's another endpoint to [update](#update-site-url) site's URL.

   The response from register endpoint will be used for subsequent actions:

   * Cancellation request requires `order_id` parameter.
   * Updating site URL request requires `access_token` and `access_token_secret`.
   * Helper API request.

   So it should be saved in customer site options:

   ```php
   <?php
   WC_Helper_Options::update(
       'auth',
       array(
           'access_token'        => $response['access_token'],
           'access_token_secret' => $response['access_token_secret'],
           'site_id'             => $response['site_id'],
           'user_id'             => get_current_user_id(),
           'updated'             => time(),
       )
   );
   ```

   `WC_Helper_Options` is available when WooCommerce is activated.

2. **Cancellation**

   Once a WPCOM plan is expired, a request to WooCommerce.com [cancel](#cancel) endpoint
   must be made. This will cancel the order created from registration request and
   revoke all subscription keys for the extensions (customers still able to use
   the extension, but no update and support from WooCommerce.com will be given
   for those extensions).

3. **Update URL**

   Update a customer site URL for a WooCommerce.com-connected site.

4. **Product Info**

   Get information about products in a package / host plan. Response includes
   latest version and download URL to our internal repository.