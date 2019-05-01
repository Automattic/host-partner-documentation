# Package Information

The following endpoints will allow you to retrieve information about all products for a package or a single product from a package. The expected information for a product will look like this:

```json
{
  "name": "Facebook for WooCommerce",
  "type": "plugin",
  "version": "1.9.6",
  "last_updated": "2018-09-21",
  "download_link": "http://woothemes-products.s3.amazonaws.com/plugin-packages/facebook-for-woocommerce/facebook-for-woocommerce.zip?AWSAccessKeyId=AKIAJE6A7GBT4ZRLENMA&Expires=1541139531&Signature=iJMJrkCsUqJNPvctF3HQVZ2ubMI%3D",
  "slug": "facebook-for-woocommerce",
  "homepage": "https://woocommerce.test/products/facebook/",
  "support_documentation": "http://docs.woocommerce.test/document/facebook"

}
```

**Note:** `type` is not supplied in the `/info/<slug>.json` endpoint.

## Table of contents

- [All Products Information](#all-products-information)
- [Single Product Information](#single-product-information)
- [Tips and Tricks](#tips-and-tricks)

## All Products Information

Get information all of the products in a package.

```code
GET /info
```

Example request:

```code
curl -i -X GET 'https://woocommerce.com/wp-json/wccom/host-plan/v1.0/info' \
  -H 'Authorization: Bearer <key>' \
  -H 'Content-Type: application/json'

HTTP/1.1 200 OK
{
  "name": "wpcom_ecommerce",
  "description": "WordPress.com eCommerce Plan",
  "products": [
    {
      "name": "USPS Shipping Method",
      "type": "plugins",
      "version": "4.4.19",
      "last_updated": "2018-10-17",
      "download_link": "http://woothemes-products.s3.amazonaws.com/plugin-packages/woocommerce-shipping-usps/woocommerce-shipping-usps.zip?AWSAccessKeyId=AKIAJE6A7GBT4ZRLENMA&Expires=1544211649&Signature=lbxifNZRLGSresGFSE6wNoVyQ2w%3D",
      "slug": "woocommerce-shipping-usps",
      "homepage": "https://woocommerce.test/products/usps-shipping-method/",
      "support_documentation": "http://docs.woocommerce.test/document/usps"
    },
    {
      "name": "UPS Shipping Method",
      "type": "plugins",
      "version": "3.2.14",
      "last_updated": "2018-10-30",
      "download_link": "http://woothemes-products.s3.amazonaws.com/plugin-packages/woocommerce-shipping-ups/woocommerce-shipping-ups.zip?AWSAccessKeyId=AKIAJE6A7GBT4ZRLENMA&Expires=1544211649&Signature=emYTeJ98l4mVaViKwKQgM2HCuYA%3D",
      "slug": "woocommerce-shipping-ups",
      "homepage": "https://woocommerce.test/products/ups-shipping-method/"
      "support_documentation": "http://docs.woocommerce.test/document/usps"
    },
    {
      "name": "Royal Mail",
      "type": "plugins",
      "version": "2.5.11",
      "last_updated": "2018-10-16",
      "download_link": "http://woothemes-products.s3.amazonaws.com/plugin-packages/woocommerce-shipping-royalmail/woocommerce-shipping-royalmail.zip?AWSAccessKeyId=AKIAJE6A7GBT4ZRLENMA&Expires=1544211649&Signature=tNQDfjKHWLQkE5tyWwxBKCosUaA%3D",
      "slug": "woocommerce-shipping-royalmail",
      "homepage": "https://woocommerce.test/products/royal-mail/"
    },
    {
      "name": "Australia Post Shipping Method",
      "type": "plugins",
      "version": "2.4.7",
      "last_updated": "2018-09-27",
      "download_link": "http://woothemes-products.s3.amazonaws.com/plugin-packages/woocommerce-shipping-australia-post/woocommerce-shipping-australia-post.zip?AWSAccessKeyId=AKIAJE6A7GBT4ZRLENMA&Expires=1544211649&Signature=g%2Fit%2FArPygdkQCf%2FIcN7BVJrHRI%3D",
      "slug": "woocommerce-shipping-australia-post",
      "homepage": "https://woocommerce.test/products/australia-post-shipping-method/",
      "support_documentation": "http://docs.woocommerce.test/document/australia"
    },
    {
      "name": "Canada Post Shipping Method",
      "type": "plugins",
      "version": "2.5.7",
      "last_updated": "2018-10-17",
      "download_link": "http://woothemes-products.s3.amazonaws.com/plugin-packages/woocommerce-shipping-canada-post/woocommerce-shipping-canada-post.zip?AWSAccessKeyId=AKIAJE6A7GBT4ZRLENMA&Expires=1544211649&Signature=%2BgC48cQxXHk9ihjS3YXzH9NeRNA%3D",
      "slug": "woocommerce-shipping-canada-post",
      "homepage": "https://woocommerce.test/products/canada-post-shipping-method/",
      "support_documentation": "http://docs.woocommerce.test/document/candada-post"
    },
    {
      "name": "Facebook for WooCommerce",
      "type": "plugins",
      "version": "1.9.8",
      "last_updated": "2018-11-30",
      "download_link": "http://woothemes-products.s3.amazonaws.com/plugin-packages/facebook-for-woocommerce/facebook-for-woocommerce.zip?AWSAccessKeyId=AKIAJE6A7GBT4ZRLENMA&Expires=1544211649&Signature=lVBd50jPoHZMo7CNFq1P%2BvUiVgs%3D",
      "slug": "facebook-for-woocommerce",
      "homepage": "https://woocommerce.test/products/facebook/",
      "support_documentation": "http://docs.woocommerce.test/document/facebook"
    },
    {
      "name": "Product Add-Ons",
      "type": "plugins",
      "version": "3.0.4",
      "last_updated": "2018-11-21",
      "download_link": "http://woothemes-products.s3.amazonaws.com/plugin-packages/woocommerce-product-addons/woocommerce-product-addons.zip?AWSAccessKeyId=AKIAJE6A7GBT4ZRLENMA&Expires=1544211649&Signature=lIbJCqX6UXRlsBGCmKhBqkF4UGo%3D",
      "slug": "woocommerce-product-addons",
      "homepage": "https://woocommerce.test/products/product-add-ons/",
      "support_documentation": "http://docs.woocommerce.test/document/product-add-ons"
    },
    {
      "name": "Galleria",
      "type": "themes",
      "version": "2.2.17",
      "last_updated": "2018-08-13",
      "download_link": "http://woothemes-products.s3.amazonaws.com/theme-packages/galleria/galleria.zip?AWSAccessKeyId=AKIAJE6A7GBT4ZRLENMA&Expires=1544211649&Signature=i4Tckbs1bLYGcMdei7SEwIkuR%2FA%3D",
      "slug": "galleria",
      "homepage": "https://woocommerce.test/products/galleria/",
      "support_documentation": "http://docs.woocommerce.test/document/galleria"
    }
  ]
}
```

## Single Product Information

Get information about a product in a package.

```code
GET /info/<slug>.json
```

Example request:

```code
curl -i -X GET 'https://woocommerce.com/wp-json/wccom/host-plan/v1.0/info/facebook-for-woocommerce.json' \
  -H 'Authorization: Bearer <key>' \
  -H 'Content-Type: application/json'

HTTP/1.1 200 OK
{
  "name": "Facebook for WooCommerce",
  "version": "1.9.6",
  "last_updated": "2018-09-21",
  "download_link": "http://woothemes-products.s3.amazonaws.com/plugin-packages/facebook-for-woocommerce/facebook-for-woocommerce.zip?AWSAccessKeyId=AKIAJE6A7GBT4ZRLENMA&Expires=1541139531&Signature=iJMJrkCsUqJNPvctF3HQVZ2ubMI%3D",
  "slug": "facebook-for-woocommerce",
  "homepage": "https://woocommerce.test/products/facebook/"
  "support_documentation": "http://docs.woocommerce.test/document/facebook"
}
```

## Tips and Tricks

Using [jq](https://stedolan.github.io/jq/), hosting partners can slice up this data in interesting, useful ways. Below are some examples that hosting partners may find helpful:

### Get all of the slugs

```
curl -s GET 'https://woocommerce.com/wp-json/wccom/host-plan/v1.0/info' \
  -H 'Authorization: Bearer <key>' \
  -H 'Content-Type: application/json' | jq '.products[].slug'
```

**Note:** You can substitute `download_link` or another product field for `slug` above to information for that field. For example:

### Get all products that are themes

```
curl -s GET 'https://woocommerce.com/wp-json/wccom/host-plan/v1.0/info' \
  -H 'Authorization: Bearer <key>' \
  -H 'Content-Type: application/json' | jq '.products[] | select( .type == "theme" )'
```

**Note:** You can substitute `plugin` for `theme` above to get all extensions.

### Get products that were updated on or after a specified day

The following will return all products that were updated on, or after, `2019-02-14`.

```
curl -s GET 'https://woocommerce.com/wp-json/wccom/host-plan/v1.0/info' \
  -H 'Authorization: Bearer <key>' \
  -H 'Content-Type: application/json' | jq '.products[] | select( .last_updated >= "2019-02-14" )'
```

### Combining the above

The following snippet will get the **slug** of all products that are of **theme** type where the theme has been updated after `2019-01-01`.

```
curl -s GET 'https://woocommerce.com/wp-json/wccom/host-plan/v1.0/info' \
  -H 'Authorization: Bearer <key>' \
  -H 'Content-Type: application/json' \
  | jq '.products[] | select( .last_updated >= "2019-01-01" ) | select( .type == "theme" ) | .slug'
```
