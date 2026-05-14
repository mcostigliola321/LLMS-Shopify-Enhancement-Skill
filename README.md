# LLMS.txt Shopify Enhancement Skill

Enhance Shopify's auto-generated `llms.txt` into a richer, agent-ready storefront map.

Shopify can generate basic AI discovery files such as `llms.txt`, `llms-full.txt`, and `agents.md`, but the default output is often thin: it may include general commerce endpoints without enough context about the store's actual categories, collections, guides, customer-care pages, warranties, and canonical shopping paths.

This Codex skill helps turn that default output into a practical AI navigation layer for Shopify stores.

## What It Produces

- `llms.txt`: a curated, high-signal storefront guide.
- `llms-full.txt`: an exhaustive public sitemap index for broad discovery.
- `templates/llms.txt.liquid`: Shopify-ready template content for `/llms.txt`.
- `templates/llms-full.txt.liquid`: Shopify-ready template content for `/llms-full.txt`.

## What It Uses

The skill audits public Shopify discovery sources:

- Existing `/llms.txt`
- Existing `/llms-full.txt`
- `/agents.md`
- `/robots.txt`
- `/sitemap.xml`
- Product, collection, page, blog, and agentic discovery sitemaps
- HTML sitemap, header navigation, footer navigation, and structured data
- Public UCP, MCP, product JSON, and collection JSON endpoints when available

## Shopify Install Pattern

For Shopify stores, the public URL and theme filename are different:

- Public URL: `/llms.txt`
- Theme file: `templates/llms.txt.liquid`

And for the full version:

- Public URL: `/llms-full.txt`
- Theme file: `templates/llms-full.txt.liquid`

Paste the generated Markdown/plain text into those Liquid template files, save the theme, and verify both root URLs in a browser.

Do not upload these files only to Shopify Files or theme assets. Those paths are not served as root storefront URLs.

## When To Use

Use this skill when you want to:

- Improve a Shopify store's default `llms.txt`.
- Generate a fuller `llms-full.txt` from public sitemaps.
- Give AI agents better canonical paths for product discovery.
- Expose support, warranty, return, guide, and brand pages clearly.
- Create Shopify-ready `.liquid` template copies.

## Skill Files

- `SKILL.md`: main skill instructions.
- `references/playbook.md`: supporting reference for URL inventory, scoring, exclusions, and Shopify template outputs.

## Author

Mark Costigliola
