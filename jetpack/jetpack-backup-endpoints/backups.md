# List Backup

Return a list of the last 10 backup attempts.

### Endpoint Information

- __Method__: GET
- __URL__: `https://public-api.wordpress.com/wpcom/v2/sites/<blog_id>/rewind/backups`
- __blog_id__: (number) Site to queury.

Authentication: [Access token](/jetpack/jetpack-start-endpoints/authentication.md).

### Request Parameters

None

### Response Format

Array of objects, each containing information about one backup attempt:

```
[{
  id: (string) The backup ID
  started: (string) Backup started datetime ("2019-11-08 18:44:35")
  last_updated: (string) Backup last updated datetime ("2019-11-08 18:44:48")
  status: (string) Backup status ("finished", "started", "no-credentials", "no-credentials-atomic", "credential-error", "not-accessible", "error", "error-will-retry")
  period: (string) Backup period in unix timestamp ("1573238675")
  has_snapshot: (bool) Backup has snapshot
  stats: (object) Backup stats, if set {
    themes: (object) Backed up themes stats, if set {
      count: (int) Backed up themes count, if set
      list: (array) List of backed up theme slugs, if set
    }
    plugins: (object) Backed up plugins stats, if set {
      count: (int) Backed up plugins count, if set
      list: (array) List of backed up plugin slugs, if set
    }
    uploads: (object) Backed up uploaded files stats, if set {
      count: (int) Backed up uploaded files count, if set
      images: (int) Backed up uploaded images count, if set
      movies: (int) Backed up uploaded movies count, if set
      audio: (int) Backed up uploaded audio count, if set
      archives: (int) Backed up uploaded archives count, if set
    }
    tables: (object) Backed up tables stats, if set
      table_name: (object) Backed up table stats, if set
      rows: (int) Count of backed up rows in table, if set
    }
  }
  prefix: (string) WP prefix ("wp_")
  wp_version: (string) WP version ("5.2.4")
},
...
]
```
