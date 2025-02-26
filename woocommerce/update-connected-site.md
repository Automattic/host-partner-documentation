# Update Connected Site

Change the site connected to the plan.

```
POST /update-connected-site
```

- [API v2.0](#api-v20)

## API v2.0

Example request and response:

```
curl -i -X POST 'https://woocommerce.com/wp-json/wccom/host-plan/v2.0/update-connected-site' \
  -H 'Authorization: Bearer <key>' \
  -H 'Content-Type: application/json' \
  -d '{
    "url": "https://example.com",
    "order_id": 123
}'

HTTP/1.1 200 OK
{
  "order_id": 123,
  "site_id": 42506,
  "url": "https://example.com",
}

```

### Parameters v2.0

| Name       | Type     | Description                 |
|------------|----------|-----------------------------|
| `url`      | `string` | New customer site URL.      |
| `order_id` | `number` | Order ID in WooCommerce.com |

### Response v2.0

| Name       | Type     | Description                          |
|------------|----------|--------------------------------------|
| `url`      | `string` | New customer site URL.               |
| `order_id` | `number` | Order ID in WooCommerce.com          |
| `site_id`  | `number` | Customer site ID in WooCommerce.com. |

```
HTTP/1.1 200 OK
{
  "url": "https://example.com",
  "order_id": 123,
  "site_id": 42506
}
```
