# User Creation

Aside from [automatic account creation](/jetpack/automatic-account-creation-connection.md) there is an endpoint available for creating a WordPress.com user. This endpoint assumes the user creation is part of a product provisioning flow, such as provisioning a WooCommerce package to someone that does not yet have a WordPress.com account.

To successfully create a WordPress.com account for a given user, there are two pre-requisites that must be met:

- The hosting partner making the request must be whitelisted.
- There must not be an existing WordPress.com account for the given email.

## Authentication
In order to make use of this endpoint you will need to be authenticated. Information on this can be found [here](/jetpack/jetpack-start-endpoints/plan-provisioning.md###endpoint-information)

## Endpoint Information (/user)

- __Method__: POST
- __URL__: `https://public-api.wordpress.com/rest/v1.3/jpphp/user`

## Request Parameters (/user)

- __email__: The email address for the user that will be created.
- __product_type__: The product type that is being provisioned for the user being created. This is either `woocommerce` or `jetpack`
- __language__(optional): The ISO 639 code for the language for the user being created. Used to ensure that the email sent to the user to verify their account is translated. Supported languages include: en,af,ar,as,be,bg,bm,bn,bo,ca,cs,csb,cy,da,de,dz,el,eo,es,et,fa,fi,fo,fr,fur,fy,ga,gu,he,hi,hu,ia,id,is,it,ja,ka,km,kn,ko,ku,la,li,lo,lt,ml,ms,nds,nl,nn,no,non,nv,oc,or,os,pa,pl,ps,pt,ro,ru,sc,sk,sl,sq,sr,sv,ta,te,th,tt,uk,ur,wa,yi,tr,az,als,arc,ast,av,ay,ba,br,ce,cv,dv,eu,gn,hr,ii,ks,kv,mk,nah,nap,pt-br,qu,sd,su,ty,udm,ug,vec,vi,xal,za,zh-cn,zh-tw,lv,bs,tl,ne,gl,uz,so,mr,kk,va,mwl,mt,hy,el-po,ilo,si,mn,fil,fr-ch,fr-ca,gd,yo,fr-be,ky,tir,am,en-gb,mya,rup


## Response Parameters (/user)

Below, the responses are grouped by whether the call to create a user was succesful or not.

### Successful response

- __success__: (bool) Was the operation successful?.
- __bearer_token__: (string) The access token for the newly created user.

### Errored response

- __error_code__: (string) Error code, if any.
- __error_message__: (string) Error message, if any.

### Endpoint Errors (/user)

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
