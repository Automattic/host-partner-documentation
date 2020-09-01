# Provisioning Jetpack Plans

In [another document](../../jetpack/plan-provisioning.md), we discussed how to provision and cancel plans by using the shell script that ships with Jetpack. But, for partners where running shell commands won't work, it is possible to communicate directly to the API on WordPress.com.

If you have any questions or issues, our contact information can be found on the [README.md document](../../README.md).

## Provisioning a plan

Plans can be provisioned by making a request using your partner token from the step above along with local_user, siteurl, and plan parameters.

### Endpoint information (/provision)

- __Method__: POST
- __URL__:    `https://public-api.wordpress.com/rest/v1.3/jpphp/provision`

### Request Parameters (/provision)

- __local_user__:      The username, ID or email on the local website (not the WordPress.com username) that should own the plan. The corresponding user _must_ already exist.
- __siteurl__:         The URL where the WordPress core files reside.
- __plan__:            A slug representing which plan or item to provision.
    - Plans: `free`, `personal`, `premium`, or `professional`.
    - Backups: `jetpack-backup-realtime` or `jetpack-backup-daily`.
    - Scan: `jetpack-scan`
    - Anti Spam: `jetpack-anti-spam`
- __force_register__:  (optional) A true/false value indicating whether to re-register a site even if we already have tokens for it. Useful for sites that have gotten into a bad state.
- __force_connect__:   (optional) A true/false value indicating whether to re-connect a user even if we already have tokens for them. Useful for sites that have gotten into a bad state.
- __onboarding__:      (optional) If true, put the user through our onboarding wizard for new sites.
- __wpcom_user_id__:   (optional) For certain keys, enables auto-connecting a WordPress.com user to the site non-interactively.
- __ssh_user__:        (optional) Set SSH user.
- __ssh_pass__:        (optional) Set SSH password.
- __ssh_private_key__: (optional) Set SSH private key.
- __ssh_host__:        (optional) Set SSH host. Will be deduced from `siteurl` if missing.
- __ssh_port__:        (optional) Set SSH port. Will default to 22 is missing.
- __ftp_user__:        (optional) Set FTP user.
- __ftp_pass__:        (optional) Set FTP password.
- __ftp_host__:        (optional) Set FTP host. Will be deduced from `siteurl` if missing.
- __ftp_port__:        (optional) Set FTP port. Will default to 21 is missing.

_Note: All the SSH parameters are optional but if you pass `ssh_user` you will need to either pass `ssh_pass` or `ssh_private_key`._

### Response Parameters (/provision)

Below, the responses are grouped by whether the call to provision a plan was successful or not.

#### Successful response

- __success__:       (bool) Was the operation successful?.
- __auth_required__: (bool) Does the user need to authorize the connection on WordPress.com to finish provisioning?
- __next_url__:      (string) When `auth_required` is true, the URL to redirect the user to in order to finish authorization.

If SSH parameters have been passed, these extra fields will be present in the response:

- __ssh_set__:       (bool) Weather the SSH credentials have been saved or not.
- __ssh_error__:     (string) Empty if save was successful, otherwise contains the error message.

#### Errored response

- __error_code__:    (string) Error code, if any.
- __error_message__: (string) Error message, if any.

### Endpoint Errors (/provision)

The following is non-exhaustive list of errors that could be returned.

| HTTP Code | Error Identifier          | Error Message                                                             |
| --------- | ------------------------- | ------------------------------------------------------------------------- |
| 400       | invalid_siteurl           | The required "siteurl" argument is missing.                               |
| 400       | invalid_local_user        | The required "local_user" argument is missing.                            |
| 400       | plan_downgrade_disallowed | Can not automatically downgrade plans. Contact support.                   |
| 400       | invalid_plan              | %s is not a valid plan                                                    |
| 403       | invalid_scope             | This token is not authorized to provision partner sites                   |
| 400       | method_not_found          | remoteRegister method not found on remote site.                           |
| 400       | method_not_found          | remoteProvision method not found on remote site. Try calling again with --force_register=true. |

For more explanation about the `method_not_found` errors, including solutions, please see [this documentation](method-not-found.md).

### Examples (/provision)

Here's an example using cURL in shell.

```shell
curl --request POST \
  --url https://public-api.wordpress.com/rest/v1.3/jpphp/provision \
  --header "authorization: Bearer $ACCESS_TOKEN" \
  --header 'cache-control: no-cache' \
 --form plan=plan_here \
 --form siteurl=siteurl_here \
 --form local_user=local_user_here
```

Here's an example using the request module in NodeJS.

```js
var request = require( 'request' );
var accessToken = 'access_token_here';
var plan = 'plan_here';
var siteurl = 'http://example.com';
var local_user = 'username_id_or_email_here';

var options = {
    method: 'POST',
    url: 'https://public-api.wordpress.com/rest/v1.3/jpphp/provision',
    headers: {
        'cache-control': 'no-cache',
        authorization: 'Bearer ' + accessToken,
    },
    formData: {
        plan: plan,
        siteurl: siteurl,
        local_user: local_user
    }
};

request( options, function ( error, response, body ) {
    if ( error ) {
        throw new Error( error );
    }

    console.log( body );
} );
```

### Considerations for domain names that do not resolve

During the typical provisioning process, several calls are made between WordPress.com and the site that will receive a plan. For calls from WordPress.com to the site to succeed, we must be able to resolve the host of the URL provided to this endpoint.

That typical provisioning process presents an issue in the case of provisioning a plan to a site with a new domain name. As of early August 2018, we are able to gracefully degrade in this case.

When WordPress.com cannot communicate to the remote site due to not being able to resolve the host, cURL error 6, WordPress.com will flag the URL for future provisioning of a plan. After doing this, the API will return a response that looks like this:

```
{
  "success": true,
  "next_url": "",
  "auth_required": true
}
```

This response is the same as the standard `/provision` response, with the exception of `next_url` being blank. Since WordPress.com is not able to communicate to the remote site, the API is not able to set secrets that are needed in the `next_url` that allows users to finish the authorization process. Authorization is still required by the user to receive the plan, which the user can do by visiting `/wp-admin` of their WordPress site and clicking the "Set Up Jetpack" button.
