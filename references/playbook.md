# LLMS.txt Shopify Enhancement Reference

This reference supports the LLMS.txt Shopify Enhancement Skill. Use it to expand Shopify's native, auto-generated `llms.txt` into a richer storefront map and optional exhaustive `llms-full.txt`.

The baseline is Shopify's generated agent-discovery output. The enhancement pass should preserve useful Shopify commerce details while adding the canonical pages that agents actually need to answer shopper questions.

## URL Inventory Columns

Recommended CSV fields:

- `url`
- `source`
- `status`
- `canonical`
- `title`
- `h1`
- `meta_description`
- `jsonld_types`
- `lastmod`
- `type`
- `score_intent`
- `score_canonical`
- `score_business`
- `score_stability`
- `score_citation`
- `include_in_llms`
- `include_in_full`
- `notes`

## Shopify Discovery Inputs

Fetch these first:

- `/llms.txt`
- `/llms-full.txt`
- `/agents.md`
- `/robots.txt`
- `/sitemap.xml`
- child sitemaps for products, collections, pages, blogs, and agentic discovery
- HTML sitemap when present
- public UCP, MCP, product JSON, and collection JSON endpoint patterns

## Common Shopify Path Patterns

Storefront:

- `/products/` -> product_or_service
- `/collections/` -> category
- `/pages/*guide*` -> guide
- `/pages/*warranty*`, `/pages/*return*`, `/pages/*faq*`, `/pages/*contact*` -> support
- `/blogs/` -> guide or optional depending on importance
- `/pages/*privacy*`, `/pages/*terms*`, `/pages/*accessibility*` -> legal
- `/.well-known/*`, `/api/ucp/*`, `/agents.md` -> discovery

## Exclusion Patterns

Exclude or demote:

- cart, checkout, account, admin
- login, signup flows unless user intent requires them
- search-result pages
- faceted filters and sorted views
- preview URLs
- campaign landing pages with short shelf life
- tag pages and date archives unless the site is a publisher
- duplicate policy URLs if robots disallows them or canonical pages exist elsewhere

## Scoring Rubric

Score 0-3:

- `0`: omit from short file
- `1`: optional or full file only
- `2`: include if category needs coverage
- `3`: include in short file

Prefer a URL for `llms.txt` when total score is 10 or higher and no exclusion pattern applies.

## Shopify Template Outputs

When installable Shopify files are requested, produce exact text copies:

- `llms.txt` -> `templates/llms.txt.liquid`
- `llms-full.txt` -> `templates/llms-full.txt.liquid`

The `.liquid` copies should contain plain Markdown text unless the user intentionally wants dynamic Liquid rendering. After generation, verify the source files and `.liquid` files match exactly.
