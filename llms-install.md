# Installing the OneFindMe MCP server (instructions for AI agents)

OneFindMe is a **hosted, remote MCP server**. There is nothing to download, build or run locally, and no API key, account or environment variable is needed.

- Transport: Streamable HTTP
- URL: `https://onefindme.com/mcp`
- Auth: none
- Tools: `search_products`, `build_basket` (both read-only)

## Steps

1. Open the user's MCP settings file for the current client (for Cline: `cline_mcp_settings.json`).
2. Add this entry inside `mcpServers` (keep any existing servers):

```json
"onefindme": {
  "type": "streamableHttp",
  "url": "https://onefindme.com/mcp",
  "disabled": false,
  "autoApprove": []
}
```

   Some clients use `"type": "http"` instead of `"streamableHttp"` — use whichever the client documents for remote HTTP servers.

3. Save the file. The client connects automatically; no restart of any local process is needed.
4. If the client cannot connect to remote HTTP servers, use the stdio bridge instead:

```json
"onefindme": {
  "command": "npx",
  "args": ["-y", "mcp-remote", "https://onefindme.com/mcp"]
}
```

   (requires Node.js 18+)

## Verify

Call `search_products` with:

```json
{ "query": "wireless earbuds", "country": "US", "max_results": 3 }
```

A successful call returns three AliExpress listings with prices in USD and links. If it fails, check that the machine can reach `https://onefindme.com/mcp` over HTTPS.

## Usage notes

- Pass the shopper's own words as `query`, in any language; set `country` to where the item will be delivered so prices and currency are correct.
- Product links are affiliate links; tell the user when you share them.
