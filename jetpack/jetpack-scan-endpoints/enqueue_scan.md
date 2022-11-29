# Enqueue a scan attempt.

Enqueue a scan attempt for a site.

### Endpoint Information

- __Method__: POST
- __URL__: `https://public-api.wordpress.com/wpcom/v2/sites/<blog_id>/scan/enqueue`
- __blog_id__: (number) Site to query.

Authentication: [Bearer token](/jetpack/reporting-endpoints/README.md).

### Request Parameters

None

### Response Format

Object with the following fields encapsulated:

- __success__: (boolean) A boolean indicating if the scan attempt was successfully enqueued.

### Successful Response

```
{
    success: true
}
```

### Example

Fetch scan information for site `155308227`:

`https://public-api.wordpress.com/wpcom/v2/sites/155308227/scan`
