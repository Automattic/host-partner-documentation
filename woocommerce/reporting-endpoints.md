# WooCommerce Reporting Endpoints

The following are endpoints used to retrieve stats for a given host plan, identified by the partner's bearer token.

## List orders

List all host-plan orders created to the authenticated host-plan.

```code
GET /orders
```

### Parameters (/orders)

|  Name | Description |
| ------ | ------------ |
| `before` | Limit response to host-plan orders created before a given ISO8601 compliant date. |
| `after` | Limit response to host-plan orders created after a given ISO8601 compliant date. |
| `status` | Limit result set to host-plan orders assigned one or more statuses. Default: `completed`. |
| `customer_id` | Limit result set to host-plan orders assigned a specific customer ID. |
| `page` |  Current page of the collection. Default is `1`. |
| `per_page` | Maximum number of items to be returned in result set. Default is `20`. Maximum `100`. |
| `offset` | Offset the result set by a specific number of items. |

### Example request and response (/orders)

```code
curl -i -X  GET \
  --url https://woocommerce.com/wp-json/wccom/host-plan/v2.0/orders \
  --header 'Authorization: Bearer <key>' \
  --header 'cache-control: no-cache'
HTTP/2 200
server: nginx
date: Fri, 14 Jun 2019 14:38:17 GMT
content-type: application/json; charset=UTF-8
content-length: 6667
x-robots-tag: noindex
x-content-type-options: nosniff
access-control-expose-headers: X-WP-Total, X-WP-TotalPages
access-control-allow-headers: Authorization, Content-Type
x-wp-total: 615
x-wp-totalpages: 31
link: <https://woocommerce.com/wp-json/wccom/host-plan/v2.0/orders?page=2>; rel="next"
cache-control: max-age=60
allow: GET
x-rq: dfw1 82 50 3130
age: 0
x-cache: pass
accept-ranges: bytes
[
    {
        "id": 4263050,
        "status": "completed",
        "date_created": "2019-06-12T21:53:45",
        "date_created_gmt": "2019-06-12T19:53:45",
        "date_modified": "2019-06-12T21:53:45",
        "date_modified_gmt": "2019-06-12T19:53:45",
        "customer_id": 123,
        "customer_email": "user@example.com",
        "line_items": [
            {
                "name": "eCommerce Plan"
            },
            {
                "name": "WooCommerce Bookings"
            }
        ]
    },
    {
        "id": 4262968,
        "status": "completed",
        "date_created": "2019-06-12T21:26:56",
        "date_created_gmt": "2019-06-12T19:26:56",
        "date_modified": "2019-06-12T21:26:56",
        "date_modified_gmt": "2019-06-12T19:26:56",
        "customer_id": 124,
        "customer_email": "user@example.com",
        "line_items": [
            {
                "name": "eCommerce Plan"
            },
            {
                "name": "WooCommerce Bookings"
            }
        ]
    },
    {
        "id": 4262918,
        "status": "completed",
        "date_created": "2019-06-12T21:13:26",
        "date_created_gmt": "2019-06-12T19:13:26",
        "date_modified": "2019-06-12T21:13:26",
        "date_modified_gmt": "2019-06-12T19:13:26",
        "customer_id": 125,
        "customer_email": "user@example.com",
        "line_items": [
            {
                "name": "eCommerce Plan"
            },
            {
                "name": "WooCommerce Bookings"
            }
        ]
    },
    ...
]
```

## Get a single order

Get a single host-plan order.

```code
GET /orders/<order_id>
```

### Example request and response (orders/order_id)

```code
curl -i -X  GET \
  --url https://woocommerce.com/wp-json/wccom/host-plan/v2.0/orders/4262918 \
  --header 'Authorization: Bearer <key>' \
  --header 'cache-control: no-cache'
HTTP/2 200
server: nginx
date: Fri, 14 Jun 2019 14:36:31 GMT
content-type: application/json; charset=UTF-8
content-length: 344
x-robots-tag: noindex
link: <https://woocommerce.com/wp-json/>; rel="https://api.w.org/"
x-content-type-options: nosniff
access-control-expose-headers: X-WP-Total, X-WP-TotalPages
access-control-allow-headers: Authorization, Content-Type
cache-control: max-age=60
allow: GET
x-rq: dfw2 87 152 3154
age: 0
x-cache: pass
accept-ranges: bytes

{
    "id": 4262918,
    "status": "completed",
    "date_created": "2019-06-12T21:13:26",
    "date_created_gmt": "2019-06-12T19:13:26",
    "date_modified": "2019-06-12T21:13:26",
    "date_modified_gmt": "2019-06-12T19:13:26",
    "customer_id": 2442392,
    "customer_email": "user@example.com",
    "line_items": [
        {
            "name": "eCommerce Plan"
        },
        {
            "name": "WooCommerce Bookings"
        }
    ],
    "metadata": []
}
```

## List order connections

List all connected products in an order.

```code
GET /orders/<order_id>/connections
```

### Response (/orders/order_id/connections)

```code
Status: 200 OK

[
  {
    "product_slug": "woocommerce-shipping-usps",
    "url": "https://example.com"
  },
  ...
],
```

## Get a single site

Get a single host-plan site.

```code
GET /sites/<site_id>
```

### Example request and response (/sites/site_id)

```code
curl -i -X GET \
  --url https://woocommerce.com/wp-json/wccom/host-plan/v2.0/sites/196037 \
  --header 'Authorization: Bearer <key>' \
  --header 'Cache-Control: no-cache'
HTTP/2 200
server: nginx
date: Fri, 14 Jun 2019 18:18:27 GMT
content-type: application/json; charset=UTF-8
content-length: 263
x-robots-tag: noindex
link: <https://woocommerce.com/wp-json/>; rel="https://api.w.org/"
x-content-type-options: nosniff
access-control-expose-headers: X-WP-Total, X-WP-TotalPages
access-control-allow-headers: Authorization, Content-Type
cache-control: max-age=60
allow: GET
x-rq: dfw2 91 202 3159
age: 0
x-cache: pass
accept-ranges: bytes

{
    "order_ids": {
        "completed": [],
        "cancelled": []
    },
    "connections": [
        {
            "order_id": "3960664",
            "site_url": "example.com",
            "product_slug": "USPS Shipping Method"
        },
        {
            "order_id": "3960664",
            "site_url": "example.com",
            "product_slug": "WooCommerce Bookings"
        }
    ]
}
```

## Get totals

Get totals of orders and connected products over time.

```code
GET /totals
```

### Example request and response (/totals)

```code
curl -i -X GET \
  --url https://woocommerce.com/wp-json/wccom/host-plan/v2.0/totals \
  --header 'Authorization: Bearer <key>' \
  --header 'Cache-Control: no-cache'
HTTP/2 200
server: nginx
date: Fri, 14 Jun 2019 18:25:10 GMT
content-type: application/json; charset=UTF-8
x-robots-tag: noindex
link: <https://woocommerce.com/wp-json/>; rel="https://api.w.org/"
x-content-type-options: nosniff
access-control-expose-headers: X-WP-Total, X-WP-TotalPages
access-control-allow-headers: Authorization, Content-Type
cache-control: max-age=60
allow: GET
x-rq: dfw2 87 42 3168
age: 0
x-cache: pass
accept-ranges: bytes

{
    "total_orders": {
        "completed": 615,
        "cancelled": 56
    },
    "total_connections": {
        "woocommerce-xero": 1,
        "wooslider": 7,
        "woocommerce-bookings": 13,
        "woocommerce-shipping-usps": 2,
        "woothemes-sensei": 2,
        "woocommerce-eu-vat-number": 1,
        "woocommerce-gateway-paypal-pro": 2,
        "woocommerce-shipping-ups": 1,
        "woocommerce-product-csv-import-suite": 2,
        "woocommerce-software-add-on": 2,
        "woocommerce-table-rate-shipping": 1,
        "woocommerce-product-vendors": 3
    },
    "total_orders_by_month": {
        ...
        "6-2019": {
            "completed": 105,
            "cancelled": 28
        }
    },
    "total_connections_by_month": {
        ...
        "6-2019": {
            "woocommerce-eu-vat-number": 1,
            "woocommerce-gateway-paypal-pro": 2,
            "woocommerce-shipping-usps": 1,
            "woocommerce-shipping-ups": 1,
            "woocommerce-product-csv-import-suite": 2,
            "woocommerce-software-add-on": 2,
            "woocommerce-table-rate-shipping": 1,
            "wooslider": 5,
            "woothemes-sensei": 1,
            "woocommerce-product-vendors": 3,
            "woocommerce-bookings": 8
        }
    }
}
```
