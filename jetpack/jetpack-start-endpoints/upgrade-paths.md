# Upgrade Paths

Not all Jetpack product offerings should be provisioned concurrently. Some products contain the functionality of others so it doesn't make sense to provision them concurrently. The logic to determine which products can be provisioned for a particular site is quite complex and should not be implemented by partners. This is exactly what the upgrade paths endpoint is about. In short, given a blog ID or a URL, it will return what products can be provisioned.

The only time when we allow products with overlapping functionality to be provisioned is when the product to be provisioned is a superset of a product already in place. For example, Jetpack Professional includes Realtime Backups as part of its functionality. Consider these two scenarios:

1. A site already has Realtime Backups provisioned. A hosting partner wants to provision Jetpack Professional. Even though Jetpack Professional already includes Realtime Backups, this action *will* be allowed as the site would be gaining extra functionality.
2. A site already has Jetpack Professional provisioned. A hosting partner wants to provision Realtime Backups. This *will not* be allowed because the site would not gain anything from provisioning Realtime Backups as that same functionality is already included in the existing Jetpack Professional plan. 

## Getting an access token

To query this status endpoint, you'll first need to retrieve an access token. Information about that can be found on the [Authentication API document](../jetpack-start-endpoints/authentication.md#getting-a-jetpack-partner-access-token ).

### Endpoint information (/provision)

- __Method__: GET
- __URL__:    `https://public-api.wordpress.com/rest/v1.3/jpphp/{$blog_id}/upgrade-paths`

`{$blog_id}` is the WordPress.com blog ID.

### Response Parameters (/upgrade-paths)

Below, the responses are grouped by whether the call was successful or not.

#### Successful response

The response will include as top level keys the name of the product family that the available upgrade paths belong to. At the time of this writing, the available product families are `jetpack-plans` and `jetpack-backup`. Each of those keys will contain an array of possible upgrades. For example, a site with a free Jetpack plan would return these upgrade paths:

```
{
    "jetpack-backup": [
        "jetpack-backup-daily",
        "jetpack-backup-realtime"
    ],
    "jetpack-plans": [
        "personal",
        "premium",
        "professional"
    ]
}
```

The above means that for this particular site, both daily and realtime backup products can be provisioned, and personal, premium, and professional Jetpack plans can be provisioned as well.

It is important to understand that the above response does not mean that a host can provision *all* of those plans but just *one*. The reason is that by virtue of provisioning any of those plans, the available upgrade paths will change.

#### Errored response

- __error__:    (string) Error code, if any.
- __message__:  (string) Error message, if any.

### Examples (/provision)

Here's an example using cURL in shell.

```shell
curl --request POST \
  --url https://public-api.wordpress.com/rest/v1.3/jpphp/$BLOG_ID/upgrade-paths \
  --header "authorization: Bearer $ACCESS_TOKEN" \
  --header 'cache-control: no-cache' \
 --form plan=plan_here \
 --form siteurl=siteurl_here \
 --form local_user=local_user_here
```