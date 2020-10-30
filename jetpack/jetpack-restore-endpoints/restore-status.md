# Get Restore Status

Returns the current status of a given restore for the specified site.

### Endpoint Information

- __Method__: GET
- __URL__: `https://public-api.wordpress.com/wpcom/v1.1/activity-log/<blog_id>/rewind/<restore_id>/restore-status`
- __blog_id__: Site to request info for.
- __restore_id__: The restore to request info for.

### Request Parameters

None.

### Response Format

The `restore_status` object contains the following fields:
- __percent__: (number) current restore progress.
- __status__: (string) One of `finished|fail|queued|aborted|running|killed`.
- __rewind_id__: (number) the restore 
###ID.
- __is_dismissed__: (boolean) Can be used to track UI display status, refers to whether UI notice has been dismissed by the user.
- __context__: (string) The credentials role, one of `main|alternate|import`.
- __message__: (string) Further info about the status.
- __error_code__: (number) Error code.
- __failure_reason__: (string) Further information about any failure.

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

### Example

Fetch status for rewind `234725` on site `155308227`:

`https://public-api.wordpress.com/rest/v1/activity-log/155308227/rewind/234725/restore-status`

### Notes
