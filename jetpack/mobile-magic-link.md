# Sending magic links for logging in to the WordPress mobile app

Partners can request that users be sent an email with a "magic" link that will allow them to log in to the WordPress app just by following a link they receive via email. This prevents them from having to remember their username/password and streamlines the whole login process. The following API call requests such an email be sent to the specified user.

### Endpoint Information

- __Method__: POST
- __URL__:    `https://public-api.wordpress.com/rest/v1.3/jpphp/mobile-magic-link`

### Request Parameters

- __email__: The user's email to send the magic link to.

### Successful response

- __success__: (bool) Was the operation successful?

### Errored response

- __error__:   (string) Error code, if any.
- __message__: (string) Error message, if any.

### Example

Here is an example using cURL in shell. Note that for this call, `$ACCESS_TOKEN` should be a `jetpack-partner` scope token.

```bash
curl --request POST \
    --url https://public-api.wordpress.com/rest/v1.3/jpphp/mobile-magic-link \
    --header 'cache-control: no-cache' \
    --header 'content-type: multipart/form-data;' \
    --header "authorization: Bearer $ACCESS_TOKEN" \
    --form email="$EMAIL"
```

Here is an example of the email that is sent.

![alt text](https://github.com/Automattic/host-partner-documentation/assets/sample-magic-link-email.png "Sample magic link email")

### Notes

This endpoint is throttled and will only allow up to 5 requests per email per hour. If this limit is exceeded the following error will be returned:

```json
{"error":"too_many_requests","message":"Too many requests per time interval"}
```