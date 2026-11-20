---
name: onefindme-shopping
description: Find real AliExpress (and eBay) products from a shopper's own words in any language, priced for their delivery country, and answer shopping questions from OneFindMe's guides (clothing and shoe sizes, import tax and customs by country, buying advice). Use when someone wants to buy, find, compare or price something on AliExpress, describes a product without knowing its English name, shops in a language other than English, or asks about sizes, customs or how to choose a product.
---

# OneFindMe: shopping search and guides in any language

The plugin connects the OneFindMe MCP server (`https://onefindme.com/mcp`, read-only, no account). Its tools:

| Tool | Use it for |
|---|---|
| `search_products(query, country, language, max_results, min_price, max_price, free_shipping)` | Real AliExpress listings (plus a separate eBay list when eBay has items that ship there), priced for the delivery country |
| `build_basket(need, budget, country, language, priority, recipient, free_shipping_only)` | A set of complementary products for one need whose total stays within a budget |
| `search_guides(query, language, max_results)` | OneFindMe's ~1,200 guides in 21 languages: sizes, customs and import tax, buying guides, home problems, gifts |
| `get_guide(url, max_chars)` | The full text of one guide as Markdown, by a URL that `search_guides` returned |

## How to use it well

1. **Ask for the delivery country if you don't know it.** It changes the price, the currency and what can be shipped. Don't guess it from the language.
2. **Pass the shopper's own words** to `search_products`; the server turns them into the terms sellers use. Your own translation often loses detail ("for running", "for a toddler").
3. **Put budgets into `max_price`** (or use `build_basket` for a whole set) in the delivery country's currency.
4. **For "which one / which size / will I pay tax" questions, read the guide first:** `search_guides`, then `get_guide` on the best match, and answer from it with its link.
5. **If results look off-topic, search again with a more specific phrase.** Don't present unrelated listings as matches.
6. **Present a short comparison:** name, price, rating, orders, link. Three to five options beat twenty.
7. **Say plainly** that prices come from marketplace sellers and can change, and that product links are affiliate links (OneFindMe may earn a commission; the price is the same for the buyer).

## Shoppers who use a screen reader

Keep each product to one sentence (name, price, rating, orders) instead of a wide table, and say how many results you found.

## What not to do

- Don't recommend marketplace items where a failure is dangerous or certification matters: helmets, brakes, car seats, medical measuring devices, lithium e-bike batteries.
- Don't invent prices, delivery times or customs rules. Prices come from the tool; for customs, quote the guide and point to the official customs authority.
- Don't call a listing a genuine branded product unless it says it is sold by the brand's official store.
