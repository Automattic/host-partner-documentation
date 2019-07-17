# Setting Jetpack Backups SSH credentials

There are two ways to set Jetpack Backups SSH credentials. One way of doing this is during [plan provisioning](jetpack/plan-provisioning.md). The second one is by calling the `/jpphp/{blog_id}/ssh-credentials` endpoint directly. This document explains the latter.

## Getting an access token

To query this status endpoint, you'll first need to retrieve an access token. Information about that can be found on the [plan provisioning via API document]( plan-provisioning-direct-api.md#getting-a-jetpack-partner-access-token ).

## Endpoint Information

- __Method__: POST
- __URL__:    `https://public-api.wordpress.com/rest/v1.3/jpphp/{$blog_id}/ssh-credentials`

`$blog_id` is the is the WordPress.com blog id.

### Request Parameters

- __ssh_user__:                    Set SSH user.
- __ssh_pass__:        (optional*) Set SSH password.
- __ssh_private_key__: (optional*) Set SSH private key.
- __ssh_host__:                    Set SSH host.
- __ssh_port__:        (optional)  Set SSH port. Will default to 22 is missing.

_\*Note: You need to pass at least `ssh_pass` or `ssh_private_key`; both cannot be empty._

#### Successful response

- __success__:       (bool) Was the operation successful?

#### Errored response

- __error_code__:    (string) Error code, if any.
- __error_message__: (string) Error message, if any.

### Example

```shell
curl --request POST \
  --url https://public-api.wordpress.com/rest/v1.3/jpphp/$BLOG_ID/ssh-credentials \
  --header 'Accept: */*' \
  --header 'Authorization: Bearer $ACCESS_TOKEN' \
  --header 'Cache-Control: no-cache' \
  --header 'Host: public-api.wordpress.com' \
  --form ssh_host=$SSH_HOST \
  --form ssh_user=$SSH_USER \
  --form ssh_pass=$SSH_PASS
```