---
name: get-started
description: Get started with FOPilot. Check which seller services are connected and run a first summary of orders, payments and parcels. Use right after FOPilot is connected or when the user asks what FOPilot can do.
---

# Get started with FOPilot

FOPilot works with a Ukrainian online seller's own accounts: Nova Poshta, stores on Prom.ua, Rozetka, Horoshop
and KeyCRM, the Checkbox cash register and monobank (read-only).

## First steps

1. Call `list_connections` to see what is connected. If nothing is, tell the user to add their service keys on
   the Integrations page of their FOPilot account, or to turn on demo data there to try the tools safely.
2. Call `get_daily_summary` for a first overview: new orders, payments, parcels on the way.
3. Offer the next step that fits what is connected: unshipped paid orders (`list_orders`), a delivery
   estimate (`np_estimate_delivery`), tracking (`np_track_parcels`) or payment reconciliation
   (`reconcile_payments`).

## Rules

- Orders are referenced as `<source>:<id>`, for example `prom:312874561`. Never invent one.
- Before any tool that creates, changes or deletes something, show what will happen and wait for a clear yes.
  Fiscal receipts, closing a shift and deleting a waybill cannot be undone.
- `np_create_waybills_bulk` returns a plan first (dry run). Show the plan, then create only after the user
  confirms, passing the plan id.
- Customer phone numbers are masked. Reveal them only when the user asks for the contacts of a specific order.
- FOPilot never moves money. monobank data is read-only; say so when asked for a transfer.
- Results marked `"demo": true` come from demo connections: no real waybills or fiscal documents were made.
- When a limit is reached, tell the user what the limit is and when it resets. Do not advertise plans.
- Answer in the user's language. Ukrainian users usually expect Ukrainian.
