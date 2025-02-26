# Install Product

Install a product from the plan on the connected site.

```
POST /install
```

- [API v2.0](#api-v20)

## API v2.0

Example request and response:

```
curl -i -X POST 'https://woocommerce.com/wp-json/wccom/host-plan/v2.0/install' \
  -H 'Authorization: Bearer <key>' \
  -H 'Content-Type: application/json' \
  -d '{
    "product_slug": "dynamic-pricing",
    "url": "https://example.com",
    "order_id": 123
}'

HTTP/1.1 200 OK
{
    "request_id": 168,
    "status": "completed",
    "order_id": 18734003407356,
    "product_id": 18643,
    "product_slug":"dynamic-pricing",
    "url":"https://example.com"
}
```

### Parameters v2.0

| Name           | Type     | Description                             |
|----------------|----------|-----------------------------------------|
| `url`          | `string` | URL of the site to install the product. |
| `order_id`     | `number` | Order ID in WooCommerce.com             |
| `product_slug` | `string` | Slug of the product to install          |


### Response v2.0

| Name           | Type     | Description                              |
|----------------|----------|------------------------------------------|
| `request_id`   | `number` | ID of the installtion request.           |
| `status`       | `string` | Status of the installtion request        |
| `order_id`     | `number` | Order ID in WooCommerce.com              |
| `product_id`   | `number` | Product ID in WooCommerce.com            |
| `product_slug` | `string` | Slug of the product to install           |
| `url`          | `string` | URL of the site the product is installed |

```
HTTP/1.1 200 OK
{
    "request_id": 168,
    "status": "completed",
    "order_id": 18734003407356,
    "product_id": 18643,
    "product_slug":"dynamic-pricing",
    "url":"https://example.com"
}
```
