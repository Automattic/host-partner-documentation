# Cancelling a plan

Plans can be cancelled by making a request using your partner token from the step above and the URL of the site being cancelled.

### Endpoint Information (/partner-cancel)

- __Method__: POST
- __URL__:    `https://public-api.wordpress.com/rest/v1.3/jpphp/{$siteOrBlogId}/partner-cancel`

`$siteOrBlogId` can either be:
 
 - The WordPress.com blog ID.
 - The site's domain and path where `/` in the path is replaced with `::`. For example:

| Site URL              | $site Identifier        |
| --------------------- | -------------------     |
| `example.com`         | `example.com`           |
| `example.com/demo`    | `example.com::demo`     |
| `example.com/demo/wp` | `example.com::demo::wp` |

### Request Parameters (/partner-cancel)
- __plan__: A slug representing which plan or item to cancel. Note this is an optional parameter for Jetpack Plans (Personal, Premium, Professional) but required for cancelling standalone items including Jetpack backups.
    - Plans: `free`, `personal`, `premium`, or `professional`.
    - Backups: `jetpack-backup-realtime` or `jetpack-backup-daily`.
    - Scan: `jetpack-scan`
    - Anti Spam: `jetpack-anti-spam`
- __cancel-all__: Optional. If this option is set to true, ALL purchased items provisioned by the calling partner for a given site URL will be cancelled.


### Query Parameters (/partner-cancel)
- __http_envelope__: Default to `false`. Sending `true` will force the HTTP status code to always be `200`. The JSON response is wrapped in an envelope containing the "real" HTTP status code and headers.
- __pretty__:        Defaults to `false`. Setting to `true` will output pretty JSON.

### Response Parameters (/partner-cancel)

Below, the response parameters are grouped by whether the request to cancel errored or not.

#### Successful response (/partner-cancel)

- __success__:       (bool) Was the operation successful?. It is possible for success to be false if a plan did not exist for the site.

- __pending_activations__: (conditional) (array) If cancel-all is set for the request, then this property will be added to the response to indicate all pending activations that were cancelled.

- __activations__: (conditional) (array) If cancel-all is set for the request, then this property will be added to the response to indicate all activations that were cancelled.

#### Errored response (/partner-cancel)

- __error_code__:    (string) Error code, if any.
- __error_message__: (string) Error message, if any.

### Endpoint errors (/partner-cancel)

| HTTP Code | Error Identifier      | Error Message                                                             |
| --------- | --------------------- | ------------------------------------------------------------------------- |
| 400       | invalid_input         | Unable to delete subscription                                             |
| 400       | not_jps_plan          | The plan for this site was not provisioned by Jetpack Start               |
| 403       | invalid_scope         | This token is not authorized to provision partner sites                   |
| 403       | invalid_blog          | The blog ID %s is invalid                                                 |
| 403       | incorrect_partner_key | Subscriptions can only be cancelled by the oAuth client that created them |

### Examples (/partner-cancel)

Here's an example using cURL in shell.

```shell
ACCESS_TOKEN="access_token_here"
SITE_DOMAIN="example.com"
curl --request POST \
    --url https://public-api.wordpress.com/rest/v1.3/jpphp/"$SITE_DOMAIN"/partner-cancel \
    --header "authorization: Bearer $ACCESS_TOKEN" \
    --header 'cache-control: no-cache' \
```

Here's an example using the request module in Node JS.

```javascript
var request = require( 'request ');
var accessToken = 'access_token_here';
var siteDomain = 'example.com';

var options = {
    method: 'POST',
    url: 'https://public-api.wordpress.com/rest/v1.3/jpphp/' + siteDomain + '/partner-cancel',
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
