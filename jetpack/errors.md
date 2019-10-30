# Errors

This endpoint returns the error codes than can be returned by the API. For each possible error, it contains a key and a description in English.

## Endpoint Information

- __Method__: GET
- __URL__:    `https://public-api.wordpress.com/rest/v1.3/jpphp/errors`

#### Successful response

- __errors__:       (object) Errors list.

### Example

```shell
curl --request GET \
  --url https://public-api.wordpress.com/rest/v1.3/jpphp/errors \
  --header 'Accept: */*' \
  --header 'Cache-Control: no-cache'
```

### Example output

Note: the output has been shortened to simplify the documentation. Please call the endpoint to get all the possible errors.

```json
{
    "errors": {
        "activation_limit_reached": "This key has reached its activation limit for product %s",
        "could_not_load_product_class": "Could not load a product class",
        "error_access_token": "Failed to create access token",
        "failed_registration_unknown_blog": "Remote site returned an invalid site ID"
    }
}
```
