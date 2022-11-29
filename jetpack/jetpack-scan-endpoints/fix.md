# Fix multiple threats

Fixes multiple threats at once.

### Endpoint Information

- __Method__: POST
- __URL__: `https://public-api.wordpress.com/wpcom/v2/sites/<blog_id>/alerts/fix`
- __blog_id__: (number) Site to query.

Authentication: [Bearer token](/jetpack/reporting-endpoints/README.md).

### Request Parameters

Request parameters can be serialized in json.

- __threat_ids__: (array) An array of threat ids.

## Request body example

```
{
    threat_ids: [81444650, 81444645, 81444565]
}
```

### Response Format

Object with the following fields encapsulated:

- __ok__: (boolean) A boolean indicating if the request was successful.
- __threats__: (object) An object containing a key for each threat id that was passed in the request. Each key will have it's own object with a status node indicating how the fixer for that particular threat is progressing.

### Successful Response

```
{
	"ok": true,
	"threats": {
		"81444650": {
			"status": "in_progress"
		},
		"81444645": {
			"status": "in_progress"
		},
		"81444565": {
			"status": "in_progress"
		}
	}
}
```