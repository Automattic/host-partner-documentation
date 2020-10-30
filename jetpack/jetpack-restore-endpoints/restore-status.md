# Get Restore Status

Returns the current status of a given restore for the specified site.

### Endpoint Information

- __Method__: GET
- __URL__: `https://public-api.wordpress.com/wpcom/v1.1/activity-log/<blog_id>/rewind/<restore_id>/restore-status`
- __blog_id: Site to request info for.
- __restore_id__: The restore to request info for.

### Request Parameters

None.

### Response Format



### Successful response

```
{
  "ok":true,
  "error":"",
  "restore_status":{
    "percent":0,
    "status":"queued",
    "rewind_id":"1603977475",
    "is_dismissed":false,
    "context":"main",
    "message":"",
    "error_code":"",
    "failure_reason":""
  }
}
```
