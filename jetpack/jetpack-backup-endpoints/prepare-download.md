# Prepare a Backup Snapshot for Download

Request an archive of a backup snapshot for downloading.

### Endpoint Information

- __Method__: POST
- __URL__: `https://public-api.wordpress.com/wpcom/v2/sites/<blog_id>/rewind/downloads`
- __blog_id__: (number) Site to request the download for.

Authentication: [Access token](/jetpack/jetpack-start-endpoints/authentication.md).

### Request Parameters

- __rewindId__: (number) Optional unix timestamp of the snapshot to download. Assumes latest timestamp is not provided.
- __types__: (object) Optional object with keys `themes`, `plugins`, `uploads`, `sqls`, `roots`, `contents`, `all`. Specify true for each type of data to be included in the archive. Assumes all if not provided.

### Successful Response

Returns status info about the archive preperation:

```
{
  backupPoint: "2020-11-05T14:01:13+00:00"
  downloadId: 277467
  progress: 0
  rewindId: "1604584873.7525"
  startedAt: "2020-11-05T14:01:13+00:00"
}
...
```

### Example

Prepare download of the latest backup data for site `155308227`:

`https://public-api.wordpress.com/wpcom/v2/sites/155308227/rewind/downloads`

### Notes

After calling this endpoint, poll for progress of the archive preparation with the the [download status endpoint](/jetpack/jetpack-backup-endpoints/download.md).

