# Get the status of a fixer job

Gets the status of one or multiple fixer jobs that were started.

### Endpoint Information

- __Method__: GET
- __URL__: `https://public-api.wordpress.com/wpcom/v2/sites/<blog_id>/alerts/fix`
- __blog_id__: (number) Site to query.

Authentication: [Bearer token](/jetpack/reporting-endpoints/README.md).

### Request Parameters

Parameters must be passed by query string.

- __threat_ids__: (array) An array of threat ids.


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

### Example

Request URL: https://public-api.wordpress.com/wpcom/v2/sites/212734736/alerts/fix/?_envelope=1&threat_ids%5B%5D=81444650&threat_ids%5B%5D=81444645&threat_ids%5B%5D=81444565


Fetch fixer information for site `212734736` and for the threats `81444650`, `81444645` and `81444565`:

`https://public-api.wordpress.com/wpcom/v2/sites/212734736/alerts/fix/?threat_ids[]=81444650&threat_ids[]=81444645&threat_ids[]=81444565`
