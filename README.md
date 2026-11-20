<p align="center"><img src="assets/icon.svg" width="96" height="96" alt="FOPilot"></p>

# FOPilot

Nova Poshta waybills, Prom, Rozetka and Horoshop orders, Checkbox receipts and monobank statements for Ukrainian online sellers.

FOPilot is a hosted [Model Context Protocol](https://modelcontextprotocol.io) server. There is nothing to
install: add the URL to your AI client and sign in.

```
https://fopilot.com.ua/mcp
```

- Website: https://fopilot.com.ua/en · Documentation: https://fopilot.com.ua/en/docs
- Transport: Streamable HTTP · Authorization: OAuth 2.1 (dynamic client registration, PKCE)
- Sign-in: e-mail code, Google or GitHub. A free plan is available; plans and limits are on the website.

## Connect

**Claude (web, desktop, mobile).** Settings → Connectors → Add custom connector → paste the URL → Connect.
Step by step: https://fopilot.com.ua/en/docs/connect-claude

**ChatGPT.** Settings → Apps & Connectors → add a connector with the URL (developer mode).
Step by step: https://fopilot.com.ua/en/docs/connect-chatgpt

**Claude Code.**

```bash
claude mcp add --transport http fopilot https://fopilot.com.ua/mcp
```

**Cursor** (`~/.cursor/mcp.json` or `.cursor/mcp.json` in a project):

```json
{
  "mcpServers": {
    "fopilot": { "url": "https://fopilot.com.ua/mcp" }
  }
}
```

**VS Code** (`.vscode/mcp.json`):

```json
{
  "servers": {
    "fopilot": { "type": "http", "url": "https://fopilot.com.ua/mcp" }
  }
}
```

Any other client that supports remote MCP servers with OAuth works the same way: give it the URL. The client
opens a sign-in window on first use.

## Tools

| Tool | Type | What it does |
| --- | --- | --- |
| `get_daily_summary` | read | Orders, payments and parcels of the day in one answer |
| `list_connections` | read | Which services are connected |
| `list_orders` | read | Orders from Prom, Rozetka, Horoshop, KeyCRM |
| `get_order` | read | One order with items and delivery details |
| `update_order_status` | write | Change the status of an order |
| `set_order_waybill` | write | Attach a waybill number to an order |
| `update_product_stock` | write | Change the stock of a product |
| `np_find_city` | read | Find a Nova Poshta city |
| `np_find_warehouse` | read | Find a branch or a parcel locker |
| `np_estimate_delivery` | read | Delivery cost and date |
| `np_create_waybill` | write | Create a waybill |
| `np_create_waybills_bulk` | write | Create waybills in bulk (dry run first) |
| `np_delete_waybill` | write | Delete a waybill |
| `np_list_waybills` | read | Created waybills |
| `np_track_parcels` | read | Tracking status of parcels |
| `checkbox_get_shift` | read | Current Checkbox shift |
| `checkbox_open_shift` | write | Open a shift |
| `checkbox_close_shift` | write | Close a shift (Z-report) |
| `checkbox_create_receipt` | write | Issue a fiscal receipt |
| `checkbox_create_return_receipt` | write | Issue a return receipt |
| `checkbox_list_receipts` | read | Receipts of a period |
| `mono_get_balances` | read | monobank balances (read-only) |
| `mono_get_statement` | read | monobank statement (read-only) |
| `reconcile_payments` | read | Match payments with orders |
| `get_usage` | read | Current plan and remaining actions |

Write tools change only the data of the signed-in account and ask for confirmation in the client.

## Example requests

- "Create waybills for today's paid Prom orders to their Nova Poshta branches"
- "Where are the parcels I sent on Monday?"
- "Which orders were paid but not shipped?"
- "Match yesterday's monobank income with orders"
- "Open the Checkbox shift and issue a receipt for order 1042"

## Safety

FOPilot uses each service's official API with your own keys, stored encrypted. monobank is read-only: money is
never moved. Fiscal receipts, closing a shift and deleting a waybill ask for confirmation first; bulk waybills
start with a dry run. A demo mode lets you try every tool without real accounts.

## What is in this repository

| File | Purpose |
| --- | --- |
| `plugin.json`, `mcp.json` | [Agent Plugins](https://agent-plugins.org) package: listing metadata and the MCP server |
| `skills/get-started/SKILL.md` | onboarding skill for assistants that load skills |
| `server.json` | card of the [official MCP registry](https://registry.modelcontextprotocol.io) |
| `assets/` | icons |

The service itself is a hosted product and its source code is not part of this repository. The manifests and
documentation here are under the MIT license.

## Support and policies

- Support: support@fopilot.com.ua · https://fopilot.com.ua/en/contact
- Privacy policy: https://fopilot.com.ua/en/legal/privacy · Terms: https://fopilot.com.ua/en/legal/terms · Security: https://fopilot.com.ua/en/security
- Questions and bug reports are welcome in the issues of this repository.

## Українською

FOPilot — ТТН Нової пошти, відстеження посилок, замовлення Prom, Rozetka і Хорошоп, чеки Checkbox (ПРРО) та виписка monobank для ФОП прямо в Claude, ChatGPT чи Cursor.

Підключення: додайте адресу `https://fopilot.com.ua/mcp` як власний конектор у своєму ШІ-клієнті та увійдіть в обліковий запис.
Покрокові інструкції — https://fopilot.com.ua/docs.

---

Built by [Bovsanka](https://bovsanka.com/en), a studio that automates business processes with AI.
