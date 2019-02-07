### Cancel

Cancel the order created from host plan registration.

```
POST /cancel
```

Example request:

```
curl -i -X POST 'https://woocommerce.com/wp-json/wccom/host-plan/v1.0/cancel' \
  -H 'Authorization: Bearer <key>' \
  -H 'Content-Type: application/json' \
  -d '{
    "order_id": 2666932
}'

HTTP/1.1 200 OK
{
  "order_id": 2666932,
  "status": "cancelled"
}
```

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| `order_id` | `number` | Order ID in WooCommerce.com. |

```
{
  "order_id": 2666932
}
```

#### Response

| Name | Type | Description |
| ---- | ---- | ----------- |
| `order_id` | `number` | Order ID in WooCommerce.com. |
| `status` | `string` | Order status in WooCommerce.com. |

```
HTTP/1.1 200 OK
{
  "order_id": 2666932,
  "status": "cancelled"
}
```