---
name: store-checkup
description: Review how a ShopsBuilder store is doing: sales over the last 7 days, recent orders, what to restock and which products shoppers can't buy. Use when the merchant asks how the shop is doing, for a weekly report, or what needs attention.
---

# Store checkup

Use the ShopsBuilder MCP tools. This skill only reads. Propose changes and make them only after
the merchant approves each one.

## 1. Store

Call `current_store`. If no store is selected, call `list_stores` and `select_store` with the
store's numeric `id` as `shop_id` (ask which one when there are several).

## 2. Sales

Call `sales_summary` with `days=7` (or `30` if the merchant asks for a month). Report the order
count and revenue (per currency) against the previous period, plus the top products.

## 3. Orders

Call `orders` for the most recent orders. Point out orders that are unpaid or unfulfilled.

## 4. Restock

Call `restock_assessment`. Explain the evidence it used (sales window, available stock, days of
cover) and never invent a forecast; when `history.weakEvidence` is true, say the rate rests on
few orders. List the variants flagged `out_of_stock` or `low` with their `suggestedRestock`, and
propose one `set_variant_stock` call per `restockPlan`.

## 5. Products shoppers can't buy

Call `channels`, then `check_channel_readiness` with the slug of each active channel. List every blocker:
unpublished products, variants without a price, zero stock, missing shipping.

## 6. Report

Keep it short: one line each for sales, orders, restock and blockers, then a numbered list of
proposed actions (for example `set_variant_stock`, `set_variant_price`,
`publish_product_to_channel`). Run an action only after the merchant says yes to it.
