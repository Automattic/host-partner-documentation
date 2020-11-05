# Get Status of Downloads

Returns the status of backup downloads for a site. Response contains the URL to download from once the archive has been generated.

### Endpoint Information

- __Method__: GET
- __URL__: `https://public-api.wordpress.com/wpcom/v2/sites/<blog_id>/rewind/downloads/<download_id>
- __blog_id__: (number) Site to request download status for.
- __download_id__: (number) Optional, request status only for this download. Returns all downloads if omitted.

Authentication: [Access token](/jetpack/jetpack-start-endpoints/authentication.md).

### Request Parameters

None.

### Successful response

```
backupPoint: "2020-11-05T13:23:37+00:00"
downloadCount: 0
downloadId: 277469
rewindId: "1604582617.404"
startedAt: "2020-11-05T14:05:24+00:00"
url: "https://public-api.wordpress.com/wpcom/v2/sites/155308227/rewind/downloads/277469/data?token=n94gJ0emrtzE1xMk12wUH6kASWlTVN3nQIqpdlfKSOjbe1exwIBfmYZ5JJd8VmIv"
validUntil: "2020-11-06T14:05:33+00:00"
```

### Example

Fetch the status of all downloads for site `155308227`:

`https://public-api.wordpress.com/wpcom/v2/sites/155308227/rewind/downloads`

### Notes

URLs are valid for 24 hours after the archive finished packing.

