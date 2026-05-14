---
name: llms-shopify-enhancement
description: Enhance Shopify's auto-generated llms.txt and llms-full.txt files by auditing storefront discovery, sitemaps, agent-commerce endpoints, canonical URLs, and customer-care pages, then producing richer Shopify-ready llms.txt.liquid and llms-full.txt.liquid templates.
metadata:
  author: Mark Costigliola
  short-description: Enhance Shopify llms.txt files
---

# LLMS Shopify Enhancement Skill

Use this skill when the user wants to enhance the auto-generated `llms.txt` that exists on a Shopify storefront. The skill starts from Shopify's native agent-discovery files, then adds the missing editorial structure that helps AI agents understand the store: core categories, collections, product-guide pages, support pages, warranty/returns pages, live catalog patterns, and Shopify-ready Liquid template files.

Primary outputs:

- `llms.txt`: curated, high-signal storefront guide.
- `llms-full.txt`: exhaustive public sitemap index for broad discovery.
- `templates/llms.txt.liquid`: Shopify theme override for `/llms.txt`.
- `templates/llms-full.txt.liquid`: Shopify theme override for `/llms-full.txt`.

## Workflow

1. Confirm the Shopify storefront domain and whether the user wants a curated file, a full file, Shopify `.liquid` templates, or all outputs.
2. Fetch Shopify discovery files:
   - `/robots.txt`
   - `/sitemap.xml`
   - child sitemaps
   - existing `/llms.txt`, `/llms-full.txt`, `/agents.md`
   - public `.well-known` or agent-commerce discovery files when present
3. Compare Shopify's auto-generated `llms.txt` against the real storefront shape. Note missing product categories, collections, support pages, guides, and policy/warranty entry points.
4. Build a URL inventory from Shopify sitemaps, HTML sitemap, header navigation, footer navigation, and structured data.
5. Preserve useful Shopify agent-commerce details from the auto-generated file, including UCP/MCP discovery and product/collection JSON patterns when available.
6. Normalize URLs:
   - Remove tracking, sorting, filtering, preview, session, and duplicate query variants.
   - Respect robots directives.
   - Prefer canonical URLs.
7. Classify URLs:
   - discovery
   - brand
   - category
   - product_or_service
   - guide
   - support
   - legal
   - optional
8. Score URLs for intent value, canonical value, business value, stability, and citation value.
9. Draft `llms.txt` with a concise summary, stable headings, and factual one-line descriptions.
10. Put exhaustive products, collections, pages, articles, or location URLs in `llms-full.txt` instead of overloading the short file.
11. Create Shopify-ready copies as `templates/llms.txt.liquid` and `templates/llms-full.txt.liquid` when the user wants installable theme files.
12. Validate links, robots compliance, duplicate URLs, heading coverage, Shopify install instructions, and common shopper/agent questions.

## Output Rules

- Start with `# Site Name`.
- Add a short blockquote summary.
- Use Markdown headings and bullets.
- Use one URL per bullet.
- Keep descriptions factual and concise.
- Avoid unsupported claims.
- Avoid live prices or inventory unless the file will be regenerated frequently.
- Include live data patterns when available, such as product JSON, API, MCP, UCP, RSS, or sitemap endpoints.
- Put volatile promotions, seasonal pages, filtered collections, archives, and exhaustive data under `Optional` or in `llms-full.txt`.
- For Shopify `.liquid` copies, keep the content as plain Markdown text and avoid Liquid delimiters unless dynamic rendering is intentional.
- Treat Shopify's auto-generated `llms.txt` as the baseline, not the final answer. Preserve its valid agent-commerce discovery details while replacing generic store copy with a useful storefront map.

## Shopify Install Guidance

For Shopify merchants:

- The source artifact is `llms.txt`; the theme template file is `templates/llms.txt.liquid`.
- The source artifact is `llms-full.txt`; the theme template file is `templates/llms-full.txt.liquid`.
- Paste the Markdown/plain text content into those theme files.
- Test the root URLs after saving: `/llms.txt` and `/llms-full.txt`.
- Do not rely on Shopify Files or theme assets for root serving.
- If the theme editor does not allow those template names, recommend an app proxy or edge worker fallback.
- After publishing, open both root URLs and confirm the rendered text matches the generated source files.

## Validation Questions

Use these questions before finalizing:

- Can an agent identify what the site is and who it serves?
- Can an agent find the main product, service, content, or documentation categories?
- Can an agent find support, warranty, returns, contact, or legal pages?
- Can an agent cite authoritative comparison or guide pages?
- Can an agent discover live product, API, documentation, or structured data endpoints?
- Are dynamic or risky claims routed to live sources?
- Do the Shopify `.liquid` files exactly mirror the source `llms.txt` and `llms-full.txt` content?

## Reference

For a fuller process, use `references/playbook.md` if present.
