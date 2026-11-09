# API docs tools: Scalar Docs vs GitBook vs Docusaurus vs Mintlify

Researched 2026-11-09. Each claim is cited in the per-tool reports:
[Scalar](research-scalar.md), [GitBook](research-gitbook.md), [Docusaurus](research-docusaurus.md), [Mintlify](research-mintlify.md).
Pricing for Scalar, GitBook, and Mintlify was re-checked against the live pricing pages.

Mintlify is in the list because Circle uses it for
[developers.circle.com](https://developers.circle.com/crosschain-transfers).
The page has `<meta name="generator" content="Mintlify">` and an `x-mintlify-client-version` header.
It is served from `circle-167b8d39.mintlify.site` through a reverse proxy.

## At a glance

| | Scalar Docs | GitBook | Docusaurus | Mintlify |
| --- | --- | --- | --- | --- |
| Type | Hosted SaaS, docs-as-code | Hosted SaaS, visual editor + Git | Open-source static site generator | Hosted SaaS, docs-as-code + browser editor |
| License | SaaS; renderer is MIT | SaaS; renderer is GPLv3 | MIT | Closed; CLI is Elastic-2.0 |
| Self-host | Renderer only | Renderer only, discouraged | Yes, you must host it | Enterprise only |
| OpenAPI | 3.0, 3.1, 3.2; Swagger 2.0 upgraded | Swagger 2.0, 3.0, 3.1 (incl. webhooks) | Community plugins only | 3.0, 3.1, 3.2; no Swagger 2.0 |
| AsyncAPI | Yes | Not documented | Not in core | 3.0, WebSocket playground |
| GraphQL | No ("coming soon" in client) | Not documented | Community plugin | Yes (SDL) |
| "Try it" console | Yes, native | Yes, powered by Scalar | Depends on plugin | Yes, native |
| Authoring | Markdown/MDX + web editor | Block WYSIWYG + Markdown; no MDX | Markdown/MDX + React | Markdown/MDX + browser editor with co-editing |
| Git sync | GitHub, Bitbucket (no GitLab) | Two-way GitHub, GitLab | Git is the source | GitHub, GitLab, Azure Repos, GHES; Bitbucket on Enterprise |
| PR previews | Yes | Yes (GitHub) | Via your host/CI | Pro+ |
| Custom CSS/JS | Yes (Pro+) | No; fixed layout, GitBook badge stays | Full control (swizzling) | Yes, all plans; custom React components |
| Search | Built in, indexes API fields | Built in | Algolia DocSearch or plugin | Built in |
| AI assistant | Ask AI on all sites (credits) | Ask (Essential+), Chat (Ultimate+) | Algolia Ask AI, bring your own LLM | Pro+ (credits) |
| llms.txt / MCP | Automatic; hosted MCP on Pro+ | Automatic on all plans, incl. Free | Community plugins | Automatic on all plans, incl. Free |
| Analytics | First-party, cookieless | Built in, incl. AI/agent traffic | GA/GTM/Vercel plugins | Pro+, incl. human vs agent traffic |
| Versioning | Yes | Site variants | Yes, strong | Yes |
| i18n | Not documented | AI translations (credits), language variants | Yes, strong (Crowdin, RTL) | Yes, ~30 languages; AI translation Pro+ |
| Private docs | Access groups (Pro+) | Share links (Essential+), auth (Ultimate+) | Not native; do it at the host | Org members (Free), password (Pro), OAuth/JWT (Enterprise) |
| SSO for team | SAML on Business+ | SAML on Enterprise | N/A | SAML on Enterprise |
| Free tier | API references only; no Docs publishing after 7-day trial | 1 user, no custom domain, API docs + Git Sync included | Everything; you pay hosting | 5 editors, custom domain, search, MCP, API playground |
| Entry paid price | Pro $150/mo ($125 yearly), 5 editors | Essential $65/site/mo + $12/user (annual) | $0 | Pro $540/mo ($450 yearly), unlimited editors |
| Mid tier | Business $600/mo ($500 yearly), 10 editors | Ultimate $249/site/mo + $12/user | $0 | Enterprise (custom) |

## Cost examples (annual billing)

- **5 editors, 1 public site, custom domain:**
  Scalar Pro $125/mo. GitBook Essential $65 + 5 × $12 = $125/mo. Docusaurus $0 + hosting. Mintlify Starter $0.
- **5 editors, private docs behind login:**
  Scalar Pro $125/mo (email-domain access groups). GitBook Ultimate $249 + $60 = $309/mo.
  Docusaurus needs your own auth proxy. Mintlify Pro $450/mo gives password auth only; OAuth/JWT login needs Enterprise.
- **SAML SSO for the team:** Scalar Business $500/mo. GitBook and Mintlify Enterprise (custom). Docusaurus N/A.
- **Analytics, previews, or AI assistant:** Mintlify jumps from $0 to $450/mo. Scalar includes these at $125/mo.
- **Several sites:** GitBook charges per site. Scalar charges by API count (3 / 15 / 25). Docusaurus and Mintlify have no site limit in their plans.

## Who each tool fits

- **Scalar Docs:** API-first teams with an OpenAPI or AsyncAPI spec that want docs-as-code, a strong native API reference, and AI/MCP output with no setup. Weak spots: no GitLab, no GraphQL, no i18n, and no free Docs publishing.
- **GitBook:** mixed teams where non-developers write content. The WYSIWYG editor with two-way Git sync is the main draw. Weak spots: no custom CSS/JS, fixed layout, per-site plus per-user pricing, and auth/SAML only on high tiers. The API console is Scalar under the hood.
- **Docusaurus:** engineering teams that want full control, zero license cost, and strong versioning and i18n. Weak spots: API reference, search, llms.txt, MCP, and auth all need plugins or your own setup. Writers need Git and Node.js.
- **Mintlify:** API companies that want the widest API coverage (OpenAPI 3.2, AsyncAPI, GraphQL) and a polished site with no setup. It has the strongest free tier: 5 editors, custom domain, search, and MCP. Weak spots: closed source, no Swagger 2.0, and a steep jump to $450/mo for analytics, previews, and AI. Customer login (OAuth/JWT) and SSO need Enterprise.

## Recommendation

- Pick **Mintlify** for a public API docs site with REST, async, and GraphQL APIs. Start free. This is the setup Circle uses.
- Pick **Scalar Docs** when you need private docs, analytics, or AI on a budget. Pro at $125/mo covers what Mintlify charges $450/mo for.
- Pick **GitBook** when writers who do not use Git produce most of the content.
- Pick **Docusaurus** when you need no vendor at all, deep customization, or many locales. Pair it with `docusaurus-openapi-docs`, or embed the MIT Scalar API Reference.
