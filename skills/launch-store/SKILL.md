---
name: launch-store
description: Launch a ShopsBuilder online store and publish its first product with a price, stock and an image, then share the storefront link. Use when the merchant wants to start selling, open a shop, create a store or add their first product.
---

# Launch a store

Use the ShopsBuilder MCP tools. The merchant signs in with OAuth; never ask for passwords, API
keys, secret keys or wallet details in chat.

## 1. Pick or create the store

1. Call `list_stores`.
2. No stores: collect the store name, the owner's email, the currency and the countries it sells
   to. The currency can't change once the store has prices, so confirm it. Call `create_store`
   with `confirmed=false`, show the preview, and call it again with `confirmed=true` only after
   the merchant agrees.
3. One store: it is selected. Several: ask which one, then call `select_store` with its `shop_id`
   (the numeric `id` from `list_stores`).
4. If a tool says provisioning isn't ready, tell the merchant and retry the same tool shortly.

Note the `storefrontUrl` from `list_stores`, `create_store` or `current_store`.

## 2. Publish the first product

Ask for the product name, a short description, the price, the stock and an image URL (or offer
to skip the image). Then run these one at a time, in order, and follow each result's `nextStep`:

`create_product` → `update_product_category` → `create_product_variant` →
`publish_product_to_channel` → `set_variant_price` → `set_variant_stock` →
`add_product_image_from_url`

- `create_product` needs a `product_type_id`. Reuse the product type of a similar product from
  `products`; if the store has none, create one with `create_product_type` (physical goods:
  `is_digital=false`, `is_shipping_required=true`; `has_variants=true` for sizes or colours).
- Use `list_categories` first; create a category with `create_category` only if none fits.
- A product needs a category before it is published.
- Descriptions are Editor.js JSON serialized as a string.
- Before creating variants, call `get_product_variant_options`. If a dimension such as size is
  missing, confirm it with the merchant, then call `create_variant_dimension`.
- Get the channel `id` (for `publish_product_to_channel` and `set_variant_price`) and its slug
  from `channels`.
- `add_product_image_from_url` takes `source_url` and needs a URL that ends in a file extension.
  For any other image, call `create_presigned_upload_urls`, upload the file, then
  `add_product_media_from_upload`.

## 3. Check it can be bought

Call `check_channel_readiness` with the channel slug. If `ready` is false, fix the first blocker
(shipping zone, warehouse, rate, price or stock) with the matching tool, after the merchant
agrees, and check again.

## 4. Hand over

Share the `storefrontUrl` and a one-line summary: product, price, stock. Offer next steps:
connect payments (`payment_methods`, share each `connectUrl`) or add more products.

If no tool does what the merchant asks, say so plainly and call `report_missing_capability` with
a one-sentence summary.
