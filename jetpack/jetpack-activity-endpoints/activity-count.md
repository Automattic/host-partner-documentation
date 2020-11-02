# Fetch Counts of Activity Groups

Returns a list of available activity groups for a site along with their counts.

### Endpoint Information

- __Method__: GET
- __URL__: `https://public-api.wordpress.com/wpcom/v2/sites/<blog_id>/activity/count/group`
- __blog_id__: Site to request groups for.

Authentication: [Access token](/jetpack/jetpack-start-endpoints/authentication.md).

### Request Parameters

- __number__: (number) Total number of activities to search.
- __aggregate__

### Successful response

```
{
  "groups": {
    "post": {
      "name": "Posts and Pages",
      "count": 69
    },
    "attachment": {
      "name": "Media",
      "count": 5
    },
    "user": {
      "name": "People",
      "count": 2
    },
    "rewind": {
      "name": "Backups and Restores",
      "count": 10
    },
  },
  "totalItems": 86,
  "took": 0.094605
}
```

### Example

`https://public-api.wordpress.com/wpcom/v2/sites/155308227/activity/count/groups?aggregate=1&number=1000`

### Notes



