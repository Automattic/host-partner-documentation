# Update Site URL

Update customer site URL for a WooCommerce.com-connected site.

```
POST /update-url
```

- [API v2.0](#api-v20)
  - Simplifies arguments required for updating a URL to new URL and order ID for a site.
- [API v1.0](#api-v10)

## API v2.0

Example request and response:

```
curl -i -X POST 'https://woocommerce.com/wp-json/wccom/host-plan/v2.0/update-url' \
  -H 'Authorization: Bearer <key>' \
  -H 'Content-Type: application/json' \
  -d '{
    "url": "https://example.com",
    "order_id": 123
}'

HTTP/1.1 200 OK
{
  "url": "https://example.com",
  "order_id": 123,
  "site_id": 42506
}

```

### Parameters v2.0

| Name | Type | Description                  |
| ---- | ---- |------------------------------|
| `url` | `string` | New customer site URL.       |
| `order_id` | `number` | Order ID in WooCommerce.com. |

### Response v2.0

| Name | Type | Description                          |
| ---- | ---- |--------------------------------------|
| `url` | `string` | New customer site URL.               |
| `order_id` | `number` | Order ID in WooCommerce.com.         |
| `site_id` | `number` | Customer site ID in WooCommerce.com. |

```
HTTP/1.1 200 OK
{
  "url": "https://example.com",
  "order_id": 123,
  "site_id": 42506
}
```


## API v1.0

Example request and response

```
curl -i -X POST 'https://woocommerce.com/wp-json/wccom/host-plan/v1.0/update-url' \
  -H 'Authorization: Bearer <key>' \
  -H 'Content-Type: application/json' \
  -d '{
    "url": "https://example.com",
    "access_token": "48db97200442b67582147beb6b538f7bafb800d3",
    "signature": "beea26f5215d1c1a2312509c1ea0eff2964431972bd45812cae0b27f032f36bf"
}'

HTTP/1.1 200 OK
true
```

### Parameters v1.0

| Name | Type | Description |
| ---- | ---- | ----------- |
| `url` | `string` | New customer site URL. |
| `access_token` | `string` | Customer access token. |
| `signature` | `string` | New customer site url signed (sha256) with the access token secret. |

Example to create signature in PHP:

```php
hash_hmac( 'sha256', 'https://example.com', $access_token_secret );
```

```
{
  "url": "https://example.com",
  "access_token": "48db97200442b67582147beb6b538f7bafb800d3",
  "signature": "beea26f5215d1c1a2312509c1ea0eff2964431972bd45812cae0b27f032f36bf"
}
```

### Response v1.0

```
HTTP/1.1 200 OK
true
```
