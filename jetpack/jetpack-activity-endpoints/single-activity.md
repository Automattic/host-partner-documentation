# Fetch a Single Activity

Lookup an activity by rewind id.

### Endpoint Information

- __Method__: GET
- __URL__: `https://public-api.wordpress.com/wpcom/v2/sites/<blog_id>/activity<rewind_id>`
- __blog_id__: Site to request activities for.
- __rewind_id__: ID of the activity to request, returned from the [site activity endpoint](/jetpack/jetpack-activity-endpoints/activity.md).

Authentication: [Access token](/jetpack/jetpack-start-endpoints/authentication.md).

### Request Parameters

None

### Successful response

```
{
  "activity_id": "AXXl1dQ8RFPhDhBzy4Be",
  "actor": {"type": "Application", "name": "Jetpack"},
  "content": {"text": "34 plugins, 11 themes, 50 uploads, 6 posts"},
  "generator": {"jetpack_version": 9.1, "blog_id": 155308227},
  "gridicon": "cloud",
  "is_discarded": false,
  "is_rewindable": true,
  "name": "rewind__backup_complete_full",
  "object": {"type": "Backup", "backup_type": "full", "rewind_id": "1605878792.626", "backup_stats": "{"themes":{"count":11,"list":["bookshop","dara","g…:{"rows":0}},"prefix":"wp_","wp_version":"5.5.3"}", "backup_period": 1605878535},
  "published": "2020-11-20T13:26:32.626+00:00",
  "rewind_id": "1605878792.626",
  "status": "success",
  "summary": "Backup and scan complete",
}
```

### Example

`https://public-api.wordpress.com/wpcom/v2/sites/155308227/activity/1605878792.626`

### Notes

None.
