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

### Response (/orders)

```code
Status: 200 OK
X-WP-Total: 500
X-WP-TotalPages: 5
Link: <https://woocommerce.com/wp-json/wccom/host-plan/v2.0/orders?page=2>; rel="next",
<https://woocommerce.com/wp-json/wccom/host-plan/v2.0/orders?page=5>; rel="last"

[
  {
    "id": 2666760,
    "status": "completed",
    "date_created": "2019-03-20T20:39:38",
    "date_created_gmt": "2019-03-20T18:39:38",
    "date_modified": "2019-03-20T20:39:38",
    "date_modified_gmt": "2019-03-20T18:39:38",
    "customer_id": 1872783,
    "customer_email": "akeda.bagus+wccom-host-plan-001@automattic.com",
    "line_items": [
      {
        "name": "eCommerce Plan",
      }
    ],
  },
  ...
]
```

### Example Request and Response (orders)

```code
curl -i -X GET \
  https://woocommerce.com/wp-json/wccom/host-plan/v2.0/orders \
  -H 'Authorization: Bearer <key>' \
  -H 'cache-control: no-cache'

HTTP/2 200
[
    {
        "id": 3960664,
        "status": "completed",
        "date_created": "2019-03-21T21:05:13",
        "date_created_gmt": "2019-03-21T19:05:13",
        "date_modified": "2019-03-21T21:05:13",
        "date_modified_gmt": "2019-03-21T19:05:13",
        "customer_id": 1208567,
        "customer_email": "user@example.com",
        "line_items": [
            {
                "name": "eCommerce Plan"
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

### Response (orders/<order_id>)

```code
Status: 200 OK

{
  "id": 2666760,
  "status": "completed",
  "date_created": "2019-03-20T20:39:38",
  "date_created_gmt": "2019-03-20T18:39:38",
  "date_modified": "2019-03-20T20:39:38",
  "date_modified_gmt": "2019-03-20T18:39:38",
  "customer_id": 1872783,
  "customer_email": "akeda.bagus+wccom-host-plan-001@automattic.com",
  "line_items": [
    {
      "name": "eCommerce Plan",
    }
  ],
}
```

## List order connections

List all connected products in an order.

```code
GET /orders/<order_id>/connections
```

### Response (/orders/<order_id>/connections)

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

### Response /sites/<site_id>

```code
Status: 200 OK

{
  "order_ids": {
    "completed": [
        123,
        456,
      ],
    "cancelled": [
        234,
        567,
      ]
  },
  "connections": [
    {
      "product_slug": "wocommerce-shipping-ups",
      "order_id": 123
    },
    ...
  ]
}
```

## Get totals

Get totals of orders and connected products over time.

```code
GET /totals
```

### Response (/totals)

```code
Status: 200 OK

{
  "total_orders": {
    "completed": 900,
    "cancelled": 100
  },
  "total_orders_by_month" : {
    "1-2019": {
      "completed": 450,
      "cancelled": 50
    },
    "2-2019": {
      "completed": 450,
      "cancelled": 50
    },
  },
  "total_connections": {
    "woocommerce-shipping-usps": 500,
    "woocommerce-product-addons": 500,
    ...
  },
  "total_connections_by_month": {
    "1-2019": {
      "woocommerce-shipping-usps": 500,
      "woocommerce-product-addons": 500,
      ...
    },
    ...
  }
}
```
