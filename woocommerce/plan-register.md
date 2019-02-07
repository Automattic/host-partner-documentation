### Register

Register a new WooCommerce.com customer with initial order of a host plan.

```
POST /register
```

Example request and response:

```
curl -i -X POST 'https://woocommerce.com/wp-json/wccom/host-plan/v1.0/register' \
  -H 'Authorization: Bearer <key>' \
  -H 'Content-Type: application/json' \
  -d '{
    "url": "https://example.com",
    "customer": {
      "first_name": "John",
      "last_name": "Doe",
      "email": "john.doe@example.com",
      "wpcom_user_id": 123
}}'

HTTP/1.1 200 OK
{
  "customer_id":1872797,
  "order_id":2666930,
  "access_token":"e95a8cc87027ec3c303e904d2ea69dd8e0ad0acf",
  "access_token_secret":"f71287fdce053102c71536b1648f27657e8be912",
  "site_id":42506
}
```

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| `url` | `string` | Customer site URL. |
| `customer` | `object` | Customer object. See below. |
| `products` | `array` | Array of product slugs. This is optional. |


| Name | Type | Description |
| ---- | ---- | ----------- |
| `first_name` | `string` | Customer first name. |
| `last_name` | `string` | Customer last name. |
| `email` | `string` | Customer email address. Required |
| `wpcom_user_id` | `integer` | WordPress.com user ID. Optional if `wpcom_accesss_token` is passed and will be deprecated in the future. |
| `wpcom_accesss_token` | `string` | WordPress.com user access token. |

```
{
  "url": "https://example.com",
  "customer": {
    "first_name": "John",
    "last_name": "Doe",
    "email": "john.doe@example.com",
    "wpcom_user_id": 123,
    "wpcom_access_token": "#K(EkA1*$gx*!JrC#DCe45meEAllcnXjhKNM2Eu!if%^BAAx3z(AaOw@t(CVFnjK)))"
  },
  "products": [ 'facebook-for-woocommerce', 'woocommerce-shipping-ups' ]
}
```

#### Response

| Name | Type | Description |
| ---- | ---- | ----------- |
| `customer_id` | `number` | Customer ID in WooCommerce.com. |
| `order_id` | `number` | Order ID in WooCommerce.com. |
| `access_token` | `string` | Customer access token. |
| `access_token_secret` | `string` | Customer access token secret. |
| `site_id` | `number` | Customer site ID in WooCommerce.com. |

```
HTTP/1.1 200 OK
{
  "customer_id":1872797,
  "order_id":2666930,
  "access_token":"e95a8cc87027ec3c303e904d2ea69dd8e0ad0acf",
  "access_token_secret":"f71287fdce053102c71536b1648f27657e8be912",
  "site_id":42506
}
```