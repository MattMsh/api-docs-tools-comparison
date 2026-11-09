# Mintlify research report

Researched 2026-11-09 from vendor sources only. Citation numbers refer to the numbered Sources list at the end.

Circle uses Mintlify for `https://developers.circle.com/crosschain-transfers`. The served HTML loads `mintlify-assets` and `_mintlify` scripts, so the page is Mintlify-hosted ([69](https://developers.circle.com/crosschain-transfers), [1](https://www.mintlify.com/)).

## Summary

Mintlify is a hosted documentation platform. It serves docs sites from Markdown and MDX files kept in Git, and it generates interactive API reference pages from OpenAPI, AsyncAPI, and GraphQL definitions ([1](https://www.mintlify.com/), [5](https://www.mintlify.com/docs/api-playground/overview)).

It targets developer-facing teams: API companies, AI and SaaS startups, and large enterprises. The vendor claims 20,000+ companies, including Circle, Anthropic, and Coinbase ([1](https://www.mintlify.com/)).

The product bundles hosting, search, a browser editor, Git sync, authentication, an MCP server, and an API playground. The free Starter plan includes all of these for up to 5 editors ([2](https://www.mintlify.com/pricing)).

Recent releases push an "agent-native" direction: pages served as Markdown to agents, `llms.txt`, a hosted MCP server, an AI assistant, an AI writing agent, and Autopilot for automatic doc updates ([52](https://www.mintlify.com/docs/ai-native), [1](https://www.mintlify.com/)).

## Hosting and deployment model

- SaaS by default. Mintlify hosts and builds the site. Customers point DNS at Mintlify or proxy traffic to it ([15](https://www.mintlify.com/docs/customize/custom-domain)).
- Sites can also live on a `*.mintlify.site` subdomain, or in a Mintlify-managed Git repository that you later clone to your own account ([16](https://www.mintlify.com/docs/deploy/github)).
- Self-hosting exists on Enterprise only, as a scoped engagement with the account team. It runs on AWS (CDK app) or Kubernetes (Helm) on AKS, GKE, OKE, OpenShift, or any cluster. You operate MongoDB, PostgreSQL, Redis, object storage, and search. Sizing guidance is about 45-60 vCPU, 160-220 GB RAM, and 1 TB SSD ([12](https://www.mintlify.com/docs/deploy/self-host)).
- Air-gapped setups use static export bundles through the REST API. Static export is Enterprise only and not publicly available ([12](https://www.mintlify.com/docs/deploy/self-host), [11](https://www.mintlify.com/docs/api/static-export/overview)).
- Not open source. The platform is closed. The CLI published as npm `mint` (4.3.8) declares license `Elastic-2.0`, which is source-available, not OSI open source ([66](https://registry.npmjs.org/mint/latest)). Public Mintlify repos carry MIT licenses, for example `mintlify/starter` and `mintlify/components` ([67](https://github.com/mintlify/starter), [68](https://github.com/mintlify/components)).
- Subpath hosting is supported. You set a base path (default `/docs`, any path allowed) and either point the whole domain at Mintlify or proxy only the subpath ([13](https://www.mintlify.com/docs/deploy/docs-subpath), [15](https://www.mintlify.com/docs/customize/custom-domain)).
- Reverse proxies are documented. Proxy `/docs`, `/docs/*`, `/docs/_llms/*`, `/_mintlify/*`, `/mintlify-assets/*`, and `/.well-known/vercel/*` to `<subdomain>.mintlify.site`. Guides cover nginx-style configs, Cloudflare Workers, Vercel rewrites, and Route 53 + CloudFront ([14](https://www.mintlify.com/docs/deploy/reverse-proxy), [13](https://www.mintlify.com/docs/deploy/docs-subpath)).
- Limit: subpath hosting is not supported when site authentication is enabled ([15](https://www.mintlify.com/docs/customize/custom-domain), [24](https://www.mintlify.com/docs/deploy/authentication-setup)).

## API reference support

- OpenAPI 3.0, 3.1, and 3.2 in JSON or YAML, from local files or hosted URLs. Multiple specs per site are allowed ([6](https://www.mintlify.com/docs/api-playground/openapi-setup)).
- Swagger 2.0 support is not documented. Docs list only 3.0, 3.1, and 3.2, so Swagger 2.0 support is not verified ([6](https://www.mintlify.com/docs/api-playground/openapi-setup)).
- `$ref` works for internal references only. External references are not supported ([6](https://www.mintlify.com/docs/api-playground/openapi-setup)).
- Overlay Specification 1.0 and 1.1 are supported, applied before validation ([6](https://www.mintlify.com/docs/api-playground/openapi-setup)).
- AsyncAPI 3.0 for WebSocket channels and messages, with a WebSocket playground. Local files, remote URLs, or multiple schemas ([7](https://www.mintlify.com/docs/api-playground/asyncapi-setup)).
- GraphQL SDL schemas generate one page per query, mutation, and named type. Source can be local or an HTTPS URL, with a custom output directory ([8](https://www.mintlify.com/docs/api-playground/graphql-setup)).
- SDK reference pages can be generated from TypeDoc, DocFX, Javadoc, Sphinx, phpDocumentor, and Go extractor artifacts through the `sdk` navigation property ([10](https://www.mintlify.com/docs/api-playground/sdk-reference-setup)).
- Interactive "try it" console: the API playground sends real requests and shows responses, proxied through Mintlify by default. Display modes are `interactive`, `simple`, `none`, and `auth` (logged-in users only) ([5](https://www.mintlify.com/docs/api-playground/overview)).
- Code samples: autogenerated for 18 languages, including cURL, Python, JavaScript, Node.js, PHP, Go, Java, Ruby, PowerShell, Swift, C#, .NET, TypeScript, C, C++, Kotlin, Rust, and Dart. Manual samples come from `x-codeSamples` or `<RequestExample>`; autogeneration can be disabled ([5](https://www.mintlify.com/docs/api-playground/overview), [9](https://www.mintlify.com/docs/api-playground/adding-sdk-examples)).
- Playground options include schema-example prefill, required-only or all parameters, cookie and credential forwarding, and base URL display mode ([5](https://www.mintlify.com/docs/api-playground/overview)).
- Multiple API versions: point navigation `versions` entries at separate specs, or list several specs in one tab ([6](https://www.mintlify.com/docs/api-playground/openapi-setup), [30](https://www.mintlify.com/docs/organize/navigation)).
- Manual API pages are supported when you set a base URL and auth method in `docs.json` ([5](https://www.mintlify.com/docs/api-playground/overview)).
- Visitors can download the spec only when `download-spec` is enabled ([53](https://www.mintlify.com/docs/ai/llmstxt)).

## Authoring experience

- Content is Markdown or MDX, configured by `docs.json`. Pages are MDX files in the repository ([30](https://www.mintlify.com/docs/organize/navigation), [31](https://www.mintlify.com/docs/organize/settings-structure)).
- Browser editor with autosave, live preview without a build step, and publish-to-Git. Publishing to the deployment branch goes live. Publishing to a feature branch commits and opens a pull request ([25](https://www.mintlify.com/docs/editor/index), [26](https://www.mintlify.com/docs/editor/review)).
- Real-time co-editing with live cursors, comments, suggestions, mentions, and page version history. Comments stay in the editor and are never committed to Git ([27](https://www.mintlify.com/docs/editor/collaborate)).
- The editor is a rich block/MDX editor over Git-backed files, not a WYSIWYG tool that hides the Markdown. Local editing with the CLI (`mint dev`, `mint validate`, `mint broken-links`) is first class ([25](https://www.mintlify.com/docs/editor/index), [28](https://www.mintlify.com/docs/cli/commands)).
- Git sync via GitHub App, GitLab, Bitbucket Cloud, Azure Repos, and GitHub Enterprise Server. Bitbucket Cloud requires Enterprise. Self-hosted GitLab OAuth is documented ([16](https://www.mintlify.com/docs/deploy/github), [18](https://www.mintlify.com/docs/deploy/bitbucket), [17](https://www.mintlify.com/docs/deploy/gitlab), [19](https://www.mintlify.com/docs/deploy/azure-repos), [20](https://www.mintlify.com/docs/deploy/ghes)).
- Review workflow: preview deployments at `<subdomain>-<branch>.mintlify.site`, review requests, required approval before publishing to the deployment branch, and merge from the editor ([26](https://www.mintlify.com/docs/editor/review)).
- Docs-as-code extras: reusable snippets, changelog pages with RSS, redirects, hidden pages, `mintignore`, monorepo and multi-repo setups (multi-repo is Enterprise), CI checks, and a VS Code MDX extension ([35](https://www.mintlify.com/docs/create/reusable-snippets), [36](https://www.mintlify.com/docs/create/changelogs), [22](https://www.mintlify.com/docs/deploy/ci), [29](https://www.mintlify.com/docs/cli/mdx-extension)).
- Migrations from 21 sources, including Docusaurus, ReadMe, GitBook, Fern, and Document360, via `mint migrate` ([2](https://www.mintlify.com/pricing)).

## Customization and theming

- Custom domain, subdomain, or subpath, with automatic TLS ([15](https://www.mintlify.com/docs/customize/custom-domain)).
- Named themes: Mint, Maple, Palm, Willow, Linden, and more, set by `theme` in `docs.json` ([37](https://www.mintlify.com/docs/customize/themes)).
- Appearance settings: logo, colors, dark mode, layout, and icons from Font Awesome, Lucide, or Tabler ([32](https://www.mintlify.com/docs/organize/settings-appearance)).
- Built-in components: cards, tabs, accordions, callouts, code groups, steps, columns, frames, fields, responses, mermaid, badges, banners, prompt, tree, tiles, and tooltips ([34](https://www.mintlify.com/docs/components)).
- Custom React components in MDX with hooks and state, on every plan. Components run in a sandboxed MDX environment with named exports only; dynamic imports and JSON imports are not supported ([39](https://www.mintlify.com/docs/customize/react-components), [2](https://www.mintlify.com/pricing)).
- Custom CSS and JS on every plan. Tailwind CSS v3 utility classes work in MDX and through `className` ([38](https://www.mintlify.com/docs/customize/custom-scripts), [2](https://www.mintlify.com/pricing)).
- Third-party npm packages can be imported, but only on Enterprise, and not on sites with authentication or personalization ([40](https://www.mintlify.com/docs/customize/third-party-libraries)).
- No plugin or extension marketplace. Extensibility is custom components, custom scripts, the `docs.json` surface, and an integrations catalog for analytics, support, and privacy tools ([40](https://www.mintlify.com/docs/customize/third-party-libraries), [47](https://www.mintlify.com/docs/integrations/analytics/overview)).
- Fonts, a custom 404 page, and CSP configuration are customizable ([41](https://www.mintlify.com/docs/customize/fonts), [42](https://www.mintlify.com/docs/customize/custom-404-page), [23](https://www.mintlify.com/docs/deploy/csp-configuration)).

## Search, AI, and analytics

- Built-in search on all plans, including free Starter. Ranking can be tuned with per-page and per-group `boost`. Maximum results and full-page results are configurable. Search filters are Enterprise ([43](https://www.mintlify.com/docs/optimize/search), [2](https://www.mintlify.com/pricing)).
- The search API describes semantic plus keyword search with filtering and pagination ([60](https://www.mintlify.com/docs/api/assistant/search)).
- `llms.txt` and `llms-full.txt` are generated automatically at the site root, and also at `/.well-known/llms.txt`. Every page is readable as Markdown by appending `.md`. Discovery headers (`Link`, `X-Llms-Txt`) advertise llms.txt, `llms-full.txt`, the API catalog, MCP server card, agent card, and agent skills index ([53](https://www.mintlify.com/docs/ai/llmstxt), [52](https://www.mintlify.com/docs/ai-native)).
- Hosted search MCP server with three tools: Search, Query docs filesystem, and Submit feedback. Included on Starter. Any MCP client such as Claude, Cursor, or ChatGPT can connect ([54](https://www.mintlify.com/docs/ai/model-context-protocol), [2](https://www.mintlify.com/pricing)).
- A separate admin MCP server lets trusted agents edit content and manage the site ([55](https://www.mintlify.com/docs/ai/mintlify-mcp)).
- AI assistant on Pro and above. It answers with citations, reads page images, returns API details from OpenAPI specs, generates code, and accepts text, image, and file input. It is also embeddable through an API and a widget ([56](https://www.mintlify.com/docs/assistant/index), [57](https://www.mintlify.com/docs/assistant/widget)).
- Writing agent and Autopilot: the agent opens pull requests from prompts, Slack threads, or webhooks. Autopilot runs on a schedule or on push. Automations are Enterprise ([52](https://www.mintlify.com/docs/ai-native), [2](https://www.mintlify.com/pricing)).
- AI translations are available on Pro and above ([2](https://www.mintlify.com/pricing)).
- Built-in analytics on Pro and above: traffic split by human and agent, assistant conversations, search queries with click-through, engagements, and feedback ([44](https://www.mintlify.com/docs/analytics/index), [2](https://www.mintlify.com/pricing)).
- Analytics export to CSV, streaming to S3 (Enterprise), and many third-party analytics integrations such as GA4, GTM, Amplitude, Mixpanel, PostHog, Segment, Heap, Hotjar, Plausible, Fathom, and Adobe ([45](https://www.mintlify.com/docs/analytics/export), [46](https://www.mintlify.com/docs/analytics/streaming), [47](https://www.mintlify.com/docs/integrations/analytics/overview)).
- Analytics REST API covers feedback, assistant conversations, caller stats, searches, views, and unique visitors ([61](https://www.mintlify.com/docs/api/analytics/views)).

## Collaboration and access control

- Default roles: viewer, editor, admin. Expanded roles add publisher and commenter. RBAC is Enterprise only. Without RBAC, every member has full dashboard access and new members join as editors ([48](https://www.mintlify.com/docs/dashboard/roles)).
- Dashboard SSO via SAML, SCIM provisioning, and audit logs are all Enterprise ([49](https://www.mintlify.com/docs/dashboard/sso), [50](https://www.mintlify.com/docs/dashboard/scim), [51](https://www.mintlify.com/docs/dashboard/audit-logs)).
- Private docs authentication: private access for Mintlify org members on all plans, password auth on Pro and Enterprise, OAuth 2.0, JWT, and email auth on Enterprise. Group-based access is Enterprise only ([24](https://www.mintlify.com/docs/deploy/authentication-setup)).
- Partial authentication is supported: public pages plus gated pages or gated API playgrounds ([24](https://www.mintlify.com/docs/deploy/authentication-setup), [5](https://www.mintlify.com/docs/api-playground/overview)).
- Preview deployments are public by default. Preview authentication can restrict them to org members ([21](https://www.mintlify.com/docs/deploy/preview-deployments), [26](https://www.mintlify.com/docs/editor/review)).
- Versioning: `versions` in `docs.json` creates a version switcher, with a configurable default and optional tags such as Latest or Beta ([30](https://www.mintlify.com/docs/organize/navigation)).
- Localization: `languages` in `docs.json` creates a language switcher, with per-language banner, footer, and navbar. About 30 languages plus regional variants such as `en-GB` and `es-419` ([30](https://www.mintlify.com/docs/organize/navigation), [59](https://www.mintlify.com/docs/guides/internationalization)).
- Content personalization, session IP allowlists, BYOK, and PDF export are Enterprise ([2](https://www.mintlify.com/pricing)).

## Pricing

Prices as shown on the pricing page on 2026-11-09 ([2](https://www.mintlify.com/pricing)).

| Plan | Price | Key limits and inclusions |
| --- | --- | --- |
| Starter | $0/mo | 5 editor seats. Custom domain, web editor, Git sync, search, Mintlify-managed authentication, MCP server, API playground, custom components, custom CSS/JS, SEO and GEO. No analytics, no preview deployments, no AI features. |
| Pro | $450/mo billed annually, $540/mo billed monthly | Unlimited editor seats. Everything in Starter plus agent, assistant, Autopilot, preview deployments, analytics, webhooks, developer API, WebMCP, grammar checks, and narration. 10,000 credits per month; overages $0.01 per credit; credit packs available. |
| Enterprise | Contact sales | Everything in Pro plus automations, SSO/SCIM/RBAC, performance SLA, advanced insights, integrations, audit logs, streaming to S3, multi-repo, white labeling, instant rollbacks, password/OAuth/JWT/email auth, self-hosting, EU hosting, custom developer portals, migration services, Slack support, and 24/7 incident monitoring. Custom credit volume. |

- Free tier: Starter is free forever for up to 5 editors, and the vendor says you can stay on it after the Pro trial ends ([2](https://www.mintlify.com/pricing)).
- Trial: 14 days of Pro with 5,000 credits, no credit card ([2](https://www.mintlify.com/pricing)).
- Credit prices: 25 credits per assistant answer, 250 credits per Autopilot or automation update. Failed answers and no-op runs cost nothing. The writing agent is free on Pro and Enterprise ([58](https://www.mintlify.com/docs/credits), [2](https://www.mintlify.com/pricing)).
- Credits pool at the organization level, roll over, and can be capped or have overages turned off ([58](https://www.mintlify.com/docs/credits)).
- Discounts: free Pro for qualifying non-commercial OSS projects; 50% off Pro for 12 months for young venture-backed startups and YC alumni; the current YC batch gets 12 months free ([2](https://www.mintlify.com/pricing)).

## Strengths

- Fast path to a polished docs site: hosting, search, a custom domain, authentication, an MCP server, and an API playground are all in the free tier ([2](https://www.mintlify.com/pricing)).
- Strong OpenAPI coverage: 3.0, 3.1, 3.2, overlays, multiple specs, autogenerated samples in 18 languages, and a real interactive playground ([6](https://www.mintlify.com/docs/api-playground/openapi-setup), [5](https://www.mintlify.com/docs/api-playground/overview)).
- AsyncAPI and GraphQL support in the same tool as REST, which is rare among docs platforms ([7](https://www.mintlify.com/docs/api-playground/asyncapi-setup), [8](https://www.mintlify.com/docs/api-playground/graphql-setup)).
- Content stays in Git as Markdown or MDX, so you can leave and keep the history. No export paywall ([2](https://www.mintlify.com/pricing)).
- Non-engineers can edit in the browser while engineers work locally. The editor commits to Git and opens pull requests on feature branches ([25](https://www.mintlify.com/docs/editor/index)).
- Strong agent readiness: `.md` pages, llms.txt, llms-full.txt, a hosted MCP server, agent card, skills index, and discovery headers, all automatic ([53](https://www.mintlify.com/docs/ai/llmstxt), [52](https://www.mintlify.com/docs/ai-native)).
- Subpath hosting plus documented proxy recipes for nginx, Cloudflare, Vercel, and AWS ([13](https://www.mintlify.com/docs/deploy/docs-subpath), [14](https://www.mintlify.com/docs/deploy/reverse-proxy)).
- Migration tooling from 21 platforms, driven by a coding agent ([2](https://www.mintlify.com/pricing)).

## Weaknesses and limits

- Closed source and vendor-hosted. The CLI is Elastic-2.0 licensed, so it is source-available but not open source ([66](https://registry.npmjs.org/mint/latest)). There is no community fork path for the platform.
- No public self-serve self-hosting. Self-host is an Enterprise engagement that takes weeks, and you operate MongoDB, PostgreSQL, Redis, and object storage ([12](https://www.mintlify.com/docs/deploy/self-host)).
- Subpath hosting and site authentication are mutually exclusive ([15](https://www.mintlify.com/docs/customize/custom-domain)).
- Static export is Enterprise only and described as "not publicly available" ([11](https://www.mintlify.com/docs/api/static-export/overview)).
- Swagger 2.0 is not supported in the docs, which list only OpenAPI 3.x. External `$ref` is not supported ([6](https://www.mintlify.com/docs/api-playground/openapi-setup)).
- AsyncAPI support is limited to version 3.0 ([7](https://www.mintlify.com/docs/api-playground/asyncapi-setup)).
- Key operational features are gated: analytics, preview deployments, and all AI features need Pro at $450+/mo. RBAC, SSO, JWT/OAuth auth, and multi-repo need Enterprise ([2](https://www.mintlify.com/pricing)).
- AI usage is metered in credits, so cost scales with reader questions and doc updates (25 and 250 credits per action) ([58](https://www.mintlify.com/docs/credits)).
- Third-party npm packages require Enterprise and fail on authenticated or personalized sites ([40](https://www.mintlify.com/docs/customize/third-party-libraries)).
- No plugin ecosystem. Extensibility is limited to components, CSS/JS, and config ([40](https://www.mintlify.com/docs/customize/third-party-libraries)).
- Preview deployment URLs are public by default, which is a leak risk for private docs ([21](https://www.mintlify.com/docs/deploy/preview-deployments)).
- Custom components render client-side, so they can flash or be missing from the initial HTML. Tailwind classes do not apply in the editor's live preview ([62](https://www.mintlify.com/docs/help-center/custom-components-flash-or-missing-from-page-source), [63](https://www.mintlify.com/docs/help-center/tailwind-classes-not-applying-in-editor-preview)).
- The default `*.mintlify.site` subdomain stays crawlable after you add a custom domain, which can cause duplicate indexing unless you handle it ([64](https://www.mintlify.com/docs/help-center/default-subdomain-indexed-alongside-custom-domain)).
- There is no public per-seat price for Enterprise, and Pro jumps straight from free to $450/mo, which is steep for a small team that only needs analytics ([2](https://www.mintlify.com/pricing)).

## Sources

1. https://www.mintlify.com/
2. https://www.mintlify.com/pricing
3. https://www.mintlify.com/docs
4. https://www.mintlify.com/docs/llms.txt
5. https://www.mintlify.com/docs/api-playground/overview
6. https://www.mintlify.com/docs/api-playground/openapi-setup
7. https://www.mintlify.com/docs/api-playground/asyncapi-setup
8. https://www.mintlify.com/docs/api-playground/graphql-setup
9. https://www.mintlify.com/docs/api-playground/adding-sdk-examples
10. https://www.mintlify.com/docs/api-playground/sdk-reference-setup
11. https://www.mintlify.com/docs/api/static-export/overview
12. https://www.mintlify.com/docs/deploy/self-host
13. https://www.mintlify.com/docs/deploy/docs-subpath
14. https://www.mintlify.com/docs/deploy/reverse-proxy
15. https://www.mintlify.com/docs/customize/custom-domain
16. https://www.mintlify.com/docs/deploy/github
17. https://www.mintlify.com/docs/deploy/gitlab
18. https://www.mintlify.com/docs/deploy/bitbucket
19. https://www.mintlify.com/docs/deploy/azure-repos
20. https://www.mintlify.com/docs/deploy/ghes
21. https://www.mintlify.com/docs/deploy/preview-deployments
22. https://www.mintlify.com/docs/deploy/ci
23. https://www.mintlify.com/docs/deploy/csp-configuration
24. https://www.mintlify.com/docs/deploy/authentication-setup
25. https://www.mintlify.com/docs/editor/index
26. https://www.mintlify.com/docs/editor/review
27. https://www.mintlify.com/docs/editor/collaborate
28. https://www.mintlify.com/docs/cli/commands
29. https://www.mintlify.com/docs/cli/mdx-extension
30. https://www.mintlify.com/docs/organize/navigation
31. https://www.mintlify.com/docs/organize/settings-structure
32. https://www.mintlify.com/docs/organize/settings-appearance
33. https://www.mintlify.com/docs/organize/settings-seo
34. https://www.mintlify.com/docs/components
35. https://www.mintlify.com/docs/create/reusable-snippets
36. https://www.mintlify.com/docs/create/changelogs
37. https://www.mintlify.com/docs/customize/themes
38. https://www.mintlify.com/docs/customize/custom-scripts
39. https://www.mintlify.com/docs/customize/react-components
40. https://www.mintlify.com/docs/customize/third-party-libraries
41. https://www.mintlify.com/docs/customize/fonts
42. https://www.mintlify.com/docs/customize/custom-404-page
43. https://www.mintlify.com/docs/optimize/search
44. https://www.mintlify.com/docs/analytics/index
45. https://www.mintlify.com/docs/analytics/export
46. https://www.mintlify.com/docs/analytics/streaming
47. https://www.mintlify.com/docs/integrations/analytics/overview
48. https://www.mintlify.com/docs/dashboard/roles
49. https://www.mintlify.com/docs/dashboard/sso
50. https://www.mintlify.com/docs/dashboard/scim
51. https://www.mintlify.com/docs/dashboard/audit-logs
52. https://www.mintlify.com/docs/ai-native
53. https://www.mintlify.com/docs/ai/llmstxt
54. https://www.mintlify.com/docs/ai/model-context-protocol
55. https://www.mintlify.com/docs/ai/mintlify-mcp
56. https://www.mintlify.com/docs/assistant/index
57. https://www.mintlify.com/docs/assistant/widget
58. https://www.mintlify.com/docs/credits
59. https://www.mintlify.com/docs/guides/internationalization
60. https://www.mintlify.com/docs/api/assistant/search
61. https://www.mintlify.com/docs/api/analytics/views
62. https://www.mintlify.com/docs/help-center/custom-components-flash-or-missing-from-page-source
63. https://www.mintlify.com/docs/help-center/tailwind-classes-not-applying-in-editor-preview
64. https://www.mintlify.com/docs/help-center/default-subdomain-indexed-alongside-custom-domain
65. https://www.mintlify.com/docs/changelog
66. https://registry.npmjs.org/mint/latest
67. https://github.com/mintlify/starter
68. https://github.com/mintlify/components
69. https://developers.circle.com/crosschain-transfers
