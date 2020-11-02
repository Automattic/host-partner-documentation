# Fetch Activity for a Site

Returns a list of activities for the specified site. 

### Endpoint Information

- __Method__: GET
- __URL__: `https://public-api.wordpress.com/wpcom/v2/sites/<blog_id>/activity`
- __blog_id__: Site to request activities for.

Authentication: [Access token](/jetpack/jetpack-start-endpoints/authentication.md).

### Request Parameters

- __action__
- __after__: (date) Start of date range.
- __before__: (date) End of date range.
- __by__
- __date_range__
- __group__: (string, array) List of activity types to filter on, examples: `plugin, theme, rewind`. See also the [group counts endpoint.](/jetpack/jetpack-activity-endpoints/activity-count.md)
- __locale__
- __name__
- __not_group__
- __number__: (number) Total number of activities to return.
- __on__
- __page__
- __search_after__
- __sort_order__
- __aggregate__
- __aggregate_show__


### Successful response

```
{
  "@context": "https://www.w3.org/ns/activitystreams",
  "summary": "Activity log",
  "type": "OrderedCollection",
  "totalItems": 36,
  "page": 1,
  "totalPages": 1,
  "itemsPerPage": 1000,
  "id": "https://public-api.wordpress.com/wpcom/v2/sites/155308227/activity?_envelope=1&aggregate=1&number=1000",
  "oldestItemTs": 1529570198443,
  "first": "https://public-api.wordpress.com/wpcom/v2/sites/155308227/activity?_envelope=1&aggregate=1&number=1000&page=1",
  "last": "https://public-api.wordpress.com/wpcom/v2/sites/155308227/activity?_envelope=1&aggregate=1&number=1000&page=1",
  "current": {
    "type": "OrderedCollectionPage",
    "id": "https://public-api.wordpress.com/wpcom/v2/sites/155308227/activity?_envelope=1&aggregate=1&number=1000",
    "totalItems": 36,
    "orderedItems": [
      {
        "summary": "User added",
        "content": {
          "text": ""
        },
        "name": "user__added",
        "actor": {
          "type": "Person",
          "name": "examplename",
          "external_user_id": 1,
          "wpcom_user_id": 16623280,
          "icon": {
            "type": "Image",
            "url": "https://secure.gravatar.com/avatar/123456789?s=96&d=mm&r=g",
            "width": 96,
            "height": 96
          },
          "role": "administrator"
        },
        "type": "Add",
        "published": "2020-09-23T10:58:03.300+00:00",
        "generator": {
          "jetpack_version": 8.9,
          "blog_id": 155308227
        },
        "is_rewindable": false,
        "rewind_id": "1600858683.3001",
        "gridicon": "user",
        "status": null,
        "activity_id": "AXS6nQl-ZME8RSzT89VO",
        "object": {
          "type": "Person",
          "name": null,
          "external_user_id": 16623280,
          "wpcom_user_id": 0
        },
        "is_discarded": false
      }
    ]
  }
}
```

### Example

`https://public-api.wordpress.com/wpcom/v2/sites/155308227/activity?aggregate=1&number=1000`

### Notes

Full backup complete events and restore events are in group `rewind`. Events that can be restored to (full snapshots and incremental changes) have the property `is_rewindable: true`.

