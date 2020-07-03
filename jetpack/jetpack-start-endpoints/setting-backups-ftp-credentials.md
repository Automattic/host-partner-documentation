# Setting Jetpack Backups FTP credentials

There are two ways to set Jetpack Backups FTP credentials. One way of doing this is during [plan provisioning](jetpack/plan-provisioning.md). The second one is by calling the `/jpphp/{blog_id}/ftp-credentials` endpoint directly. This document explains the latter.

## Getting an access token

To query this endpoint, you'll first need to retrieve an access token. Information about that can be found on the [Authentication API document]( jetpack/../authentication.md#getting-a-jetpack-partner-access-token ).

## Endpoint Information
- __Method__: POST
- __URL__:    `https://public-api.wordpress.com/rest/v1.3/jpphp/{$blog_id}/ftp-credentials`

`$blog_id` is the is the WordPress.com blog id.

### Request Parameters

- __ssh_user__:                    Set FTP user.
- __ssh_pass__:        (optional*) Set FTP password.
- __ssh_host__:                    Set FTP host.
- __ssh_port__:        (optional)  Set FTP port. Will default to 21 is missing.

#### Successful response

- __success__:       (bool) Was the operation successful?

#### Errored response

- __error_code__:    (string) Error code, if any.
- __error_message__: (string) Error message, if any.

### Example

```shell
curl --request POST \
  --url https://public-api.wordpress.com/rest/v1.3/jpphp/$BLOG_ID/ftp-credentials \
  --header 'Accept: */*' \
  --header 'Authorization: Bearer $ACCESS_TOKEN' \
  --header 'Cache-Control: no-cache' \
  --header 'Host: public-api.wordpress.com' \
  --form ftp_host=$FTP_HOST \
  --form ftp_user=$FTP_USER \
  --form ftp_pass=$FTP_PASS
```
