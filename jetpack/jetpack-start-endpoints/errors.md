# Errors

This endpoint returns the error codes than can be returned by the API. The default response is that for each possible error, it returns an error key and a description in English. You can specify to use a verbose mode which will also include possible causes and solutions for each error.

## Endpoint Information

- __Method__: GET
- __URL__:    `https://public-api.wordpress.com/rest/v1.3/jpphp/errors`

### Query Parameters (/errors)

- __verbose__: Returns a verbose response with possible causes and solutions for each error. There is no need to set it to a value; as long as it is present in the request, a verbose answer will be returned.

#### Successful response

- __errors__:       (object) Errors list.

### Example

```shell
curl --request GET \
  --url https://public-api.wordpress.com/rest/v1.3/jpphp/errors \
  --header 'Accept: */*' \
  --header 'Cache-Control: no-cache'
```

### Example output (brief)

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

### Example output (verbose)

Note: the output has been shortened to simplify the documentation. Please call the endpoint to get all the possible errors.

```json
{
    "errors": {
        "activation_limit_reached": {
            "description": "This key has reached its activation limit for product %s",
            "cause": "You're trying to provision a plan using a key that can no longer provision more of the requested plan.",
            "solution": "Contact the Jetpack Start team."
        },
        "could_not_load_product_class": {
            "description": "Could not load a product class",
            "cause": "We could not find a product that matched the requested plan.",
            "solution": "Make sure the value of the `plan` parameter is valid."
        }
    }
}
```
