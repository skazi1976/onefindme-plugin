# OneFindMe plugin

Search AliExpress **in any language** from Cursor (or any agent that reads this format). Describe what you need in your own words — English, Hebrew, Arabic, German, Spanish, Japanese and more — and get real AliExpress listings with price, rating, order count, store and a link, priced for your delivery country.

The plugin connects to the OneFindMe remote MCP server:

```json
{ "mcpServers": { "onefindme": { "type": "http", "url": "https://onefindme.com/mcp" } } }
```

- One read-only tool: `search_products(query, country, language, max_results, min_price, max_price, free_shipping)`
- No account or API key
- Also in the official MCP registry as `com.onefindme/search`

Docs: https://onefindme.com/mcp · Website: https://onefindme.com

**Disclosure:** product links are affiliate links — OneFindMe may earn a commission at no extra cost to you. Results are ordinary search results, not paid placements.
