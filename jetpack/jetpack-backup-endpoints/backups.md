# List Backups

Return a list of the last 10 backup attempts.

### Endpoint Information

- __Method__: GET
- __URL__: `https://public-api.wordpress.com/wpcom/v2/sites/<blog_id>/rewind/backups`
- __blog_id__: (number) Site to queury.

Authentication: [Access token](/jetpack/jetpack-start-endpoints/authentication.md).

### Request Parameters

None

### Response Format

Array of objects with the following fields:

- __id__: (number) Backup id.
- __started__: (date) Backup start time.
- __last_updated__: (date) Time of the most recent event, or backup end time if complete.
- __status__: (string) Backup status, one of `finished|started|no-credentials|credential-error|not-accessible|error|error-will-retry`.
- __period__: (number) Unix timestamp representation of backup start time.
- __is_scan__: (boolean) `true` if a security scan was performed as part of the backup (depends on plan).
- __has_snapshot__: (boolean) `true` if backup was a success and a snapshot was stored.
- __stats__: (object) Information about the number and types of items backed up. Object with keys `themes`, `plugins`, `uploads`, `tables`, `prefix` (table prefix), and `wp_version`.

### Successful Response

```
[{
  has_snapshot: true
  id: "134296140"
  is_backup: "1"
  is_scan: "1"
  last_updated: "2020-11-05 13:23:36"
  percent: "100"
  period: "1604582319"
  started: "2020-11-05 13:18:40"
  stats: {themes: {…}, plugins: {…}, uploads: {…}, tables: {…}, prefix: "wp_", …}
  status: "finished"
},
…
]
```

### Example

Fetch last 10 backup attempts for site `155308227`:

`https://public-api.wordpress.com/wpcom/v2/sites/155308227/rewind/backups`

### Notes



