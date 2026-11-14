# OneFindMe — AliExpress search for AI agents (remote MCP server)

Search AliExpress **in any language** from Claude, ChatGPT, Cursor, VS Code, Cline, Kilo, Gemini CLI or any MCP client. Describe what you need in your own words — English, Hebrew, Arabic, German, Spanish, Japanese and more — and get real AliExpress listings with price, rating, order count, store and a link, priced for your delivery country. When eBay has matching listings that ship to that country, they come back as a separate list.

- **Endpoint:** `https://onefindme.com/mcp` (Streamable HTTP)
- **No install, no account, no API key** — it is a hosted, read-only server
- **Official MCP Registry:** `com.onefindme/search`
- **Docs:** https://onefindme.com/mcp · **Website:** https://onefindme.com

## Connect

Most clients accept this config:

```json
{
  "mcpServers": {
    "onefindme": {
      "type": "http",
      "url": "https://onefindme.com/mcp"
    }
  }
}
```

| Client | How |
|---|---|
| Claude (web / desktop) | Settings → Connectors → Add custom connector → URL `https://onefindme.com/mcp` |
| Claude Code | `claude mcp add --transport http onefindme https://onefindme.com/mcp` |
| Cursor | Install this plugin, or add the JSON above to `~/.cursor/mcp.json` |
| VS Code | Command Palette → *MCP: Add Server* → HTTP → `https://onefindme.com/mcp` |
| Cline / Kilo / Windsurf | Add a remote server with type `streamableHttp` and the URL above |
| Clients without HTTP support | `npx -y mcp-remote https://onefindme.com/mcp` |

See [llms-install.md](llms-install.md) for step-by-step instructions an AI agent can follow.

## Tools

Both tools are read-only.

### `search_products`
Search AliExpress in the shopper's own words.

| Parameter | Type | Notes |
|---|---|---|
| `query` | string, **required** | What the shopper wants, in any language |
| `country` | string | ISO 3166-1 alpha-2 delivery country (`US`, `GB`, `DE`, `IL`, `SA`…). Default `US` |
| `language` | string | ISO 639-1 language of the query and returned titles. Default: detected |
| `max_results` | integer | 1–20, default 8 |
| `min_price` / `max_price` | number | In the delivery country's currency |
| `free_shipping` | boolean | Only free-shipping listings |

Returns listings with title, price and currency, rating, order count, store, delivery estimate, images and link. eBay listings, when present, are returned as a separate list.

### `build_basket`
Turn one need ("home gym starter set", "kit to start baking bread", a gift) into a set of complementary real listings whose total stays within a budget.

| Parameter | Type | Notes |
|---|---|---|
| `need` | string, **required** | What the basket is for, in any language |
| `budget` | number, **required** | Total budget in the delivery country's currency |
| `country` | string | Delivery country, default `US` |
| `language` | string | Language for role names, default detected |
| `priority` | string | What to favour, default quality |
| `recipient` | string | Who it is for, if relevant |
| `free_shipping_only` | boolean | Default `true` |

## Prompts

`find_product` · `compare_options` · `plan_basket` · `gift_ideas`

## Example requests

- "Find a waterproof phone holder for a bike under $15, shipping to Germany"
- "מצא לי מעיל גשם לילדה בת 6, משלוח לישראל"
- "Build me a home-gym starter set for £80, delivered to the UK"
- "ابحث عن سماعات بلوتوث رياضية، الشحن إلى السعودية"

## Disclosure

Product links are affiliate links — OneFindMe may earn a commission at no extra cost to you. Results are ordinary search results, not paid placements. OneFindMe is not affiliated with AliExpress or eBay.

## License

MIT — see [LICENSE](LICENSE).
