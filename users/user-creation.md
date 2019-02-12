# User Creation

Aside from [automatic account creation](/jetpack/automatic-account-creation-connection.md) there is an endpoint available for creating a WordPress.com user. This endpoint assumes the user creation is part of a product provisioning flow, such as provisioning a WooCommerce package to someone that does not yet have a WordPress.com account.

## Authentication
In order to make use of this endpoint you will need to be authenticated. Information on this can be found [here](/jetpack/plan-provisioning-direct-api.md###endpoint-information)

## Endpoint Information (/user)

- __Method__: POST
- __URL__: `https://public-api.wordpress.com/rest/v1.3/jpphp/user`

## Request Parameters (/user)

- __email__: The email address for the user that will be created.
- __product_type__: The product type that is being provisioned for the user being created. This is either `woocommerce` or `jetpack`


## Response Parameters (/user)

Below, the responses are grouped by whether the call to create a user was succesful or not.

## Successful response

- __success__: (bool) Was the operation successful?.
- __bearer_token__: (string) The access token for the newly created user.

## Errored response

- __error_code__: (string) Error code, if any.
- __error_message__: (string) Error message, if any.

## Endpoint Errors (/user)

The following is non-exhaustive list of errors that could be returned.

| HTTP Code | Error Identifier          | Error Message                                                             |
| --------- | ------------------------- | ------------------------------------------------------------------------- |
| 403 | forbidden | {partner} is not whitelisted for allowing user creation. |
| 400 | invalid_input_no_email | email is required to create a new WordPress.com account. |
| 400 | invalid_input_no_product_id | product_id is required to provide context for newly created WordPress.com accounts. |
| 400 | invalid_input_unknown_product_id | The supplied product ID is unknown. |
| 400 | user_exists | A WordPress.com user with given email address already exists. |
| 500 | error_access_token | Failure to create acess token

## Examples

***Replace access_token, product_type and email requirements***
```shell
RESULT=$( curl -X POST \
  https://public-api.wordpress.com/rest/v1.3/jpphp/user \
  -H 'Authorization: Bearer {access_token}' \
  -H 'cache-control: no-cache' \
  -F product_tye={product_type} \
  -F email={email} )
```
