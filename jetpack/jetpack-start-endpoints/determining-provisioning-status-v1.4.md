# Determining Provisioning Status of a Jetpack Site

At times, it may be desirable to check the provisioning status of a site to get information such as:

- Does a given site have a plan/product provisioned? If so, which?
- Does a given site have a pending activation?
- Was provisioned made by a given partner?
- Is the site connected to WordPress.com?

To provide the provisioning status of a site, there is the `/1.4/jpphp/{$siteOrBlogId}/status` endpoint.

## Getting an access token

To query this status endpoint, you'll first need to retrieve an access token. Information about that can be found on the [Authentication API document](../jetpack-start-endpoints/authentication.md#getting-a-jetpack-partner-access-token ).

## Endpoint Information

- __Method__: GET
- __URL__:    `https://public-api.wordpress.com/rest/v1.4/jpphp/{$siteOrBlogId}/status`

`$siteOrBlogId` can either be:
 
 - The WordPress.com blog ID.
 - The site's domain and path where `/` in the path is replaced with `::`. For example:

| Site URL              | $site Identifier        |
| --------------------- | -------------------     |
| `example.com`         | `example.com`           |
| `example.com/demo`    | `example.com::demo`     |
| `example.com/demo/wp` | `example.com::demo::wp` |

## Query Parameters

- __http_envelope__: Default to `false`. Sending `true` will force the HTTP status code to always be `200`. The JSON response is wrapped in an envelope containing the "real" HTTP status code and headers.
- __pretty__:        Defaults to `false`. Setting to `true` will output pretty JSON.

## Response Parameters

- __blog__:                                (array) Blog specific information.
  - __is_connected__:                      (bool) Is the site connected to WordPress.com?
  - __has_backups_credentials__:           (bool) Does the site have Jetpack Backup SSH credentials set?
- __products__:                            (array) A list with everything that was provisioned for this site.
  - __slug__:                              (string) The slug of the provisioned product.
  - __is_provisioned_by_partner__:         (bool) Was this product provisioned by a partner?
  - __is_provisioned_by_calling_partner__: (bool) Was this product provisioned by the partner making this status request?
  - __is_pending__:                        (bool) Does the site have a pending product that requires connection authorization?
  
## Endpoint errors

| HTTP Code | Error Identifier      | Error Message                                                             |
| --------- | --------------------- | ------------------------------------------------------------------------- |
| 400       | partner_key_disabled  | This key is disabled.                                                     |
| 403       | invalid_scope         | This token is not authorized to provision partner sites                   |
| 403       | invalid_blog          | The blog ID %s is invalid                                                 |

## Examples

Here's an example using cURL in shell.

```shell
ACCESS_TOKEN="access_token_here"
SITE_DOMAIN="example.com"
curl --request GET \
    --url https://public-api.wordpress.com/rest/v1.4/jpphp/"$SITE_DOMAIN"/status \
    --header "authorization: Bearer $ACCESS_TOKEN" \
    --header 'cache-control: no-cache' \
```

Here's an example using the request module in Node JS.

```javascript
var request = require( 'request ');
var accessToken = 'access_token_here';
var siteDomain = 'example.com';

var options = {
    method: 'GET',
    url: 'https://public-api.wordpress.com/rest/v1.4/jpphp/' + siteDomain + '/status',
    headers: {
        'cache-control': 'no-cache',
        authorization: 'Bearer ' + accessToken
    }
};

request( options, function ( error, response, body ) {
    if ( error ) {
        throw new Error( error );
    }

    console.log( body );
} );
```
