# Scalar Docs

## Summary

Scalar Docs is a hosted API documentation platform from Scalar. It publishes interactive API references generated from OpenAPI or AsyncAPI documents, next to written guides. Content lives in your Git repository as Markdown or MDX, configured by one `scalar.config.json` file. It is aimed at API teams that already maintain an OpenAPI document and want guides, references, search, AI answers, and access control on one domain. Every API page is rendered by the open-source, MIT-licensed Scalar API Reference ([1](https://scalar.com/products/docs), [19](https://scalar.com/products/api-references)).

## Hosting and deployment model

- SaaS. Sites are built and served by Scalar on its own infrastructure and CDN. You do not run the docs platform yourself ([1](https://scalar.com/products/docs)).
- Publishing needs a paid plan or an active trial. Subdomains use `<subdomain>.apidocumentation.com` ([1](https://scalar.com/products/docs), [6](https://scalar.com/products/docs/configuration/domains)).
- Three content sources: GitHub repository, any local folder or repository through the CLI, or the web editor at `docs.scalar.com` with no Git required ([3](https://scalar.com/products/docs/getting-started)).
- Deployment paths: publish on merge (`publishOnMerge`), preview deployment per pull request, GitHub Actions, or `scalar project publish` from any CI ([4](https://scalar.com/products/docs/configuration/scalar.config.json), [13](https://scalar.com/products/docs/deployment/automatic-deployment), [15](https://scalar.com/products/docs/deployment/cli)).
- The CLI uploads local files, or with `--github` deploys from the linked repo. It also supports preview publishes and rollback to a previous build ([15](https://scalar.com/products/docs/deployment/cli)).
- License: the monorepo `scalar/scalar` is MIT, including the API Reference, API Client, CLI, and integrations ([22](https://github.com/scalar/scalar), [23](https://github.com/scalar/scalar/blob/main/LICENSE)).
- Trust: Scalar reports a SOC 2 Type 1 report and GDPR-compliant privacy practices ([25](https://scalar.com/security)).
- The Docs platform itself is not published as an open-source package; the public repo contains the renderer and tooling, not the hosted Docs service. No self-hosting option for Docs is documented. Not verified: whether the Docs platform source is available under another license.

## API reference support

- OpenAPI 3.0, 3.1, and 3.2 in JSON or YAML. Swagger 2.0 is upgraded on load ([19](https://scalar.com/products/api-references)). OpenAPI 3.2 handling appears in the renderer changelog ([26](https://github.com/scalar/scalar/pull/10489), [27](https://github.com/scalar/scalar/pull/10487)).
- AsyncAPI documents render as channels, operations, and messages instead of paths and responses ([19](https://scalar.com/products/api-references)).
- GraphQL is not supported for docs. The API Client lists a GraphQL client as "Coming Soon" on all plans ([2](https://scalar.com/pricing)).
- Interactive "try it": every operation has a Test Request button that opens the API Client in place, with servers, parameters, and auth prefilled ([1](https://scalar.com/products/docs), [19](https://scalar.com/products/api-references)).
- Code samples are generated for cURL, JavaScript, Python, Go, and many more languages ([19](https://scalar.com/products/api-references)). SDK snippets come from the separate SDK Generator product ([2](https://scalar.com/pricing)).
- A site can host one API or many, each with its own reference page ([1](https://scalar.com/products/docs)).
- Multiple API versions: the `versions` property gives each version its own navigation and a version selector; the `default` key is required ([5](https://scalar.com/products/docs/configuration/versions)).
- OpenAPI documents can come from a file path, a URL, or the Scalar Registry; updating a Registry document republishes the docs ([4](https://scalar.com/products/docs/configuration/scalar.config.json), [13](https://scalar.com/products/docs/deployment/automatic-deployment)).
- Spectral rulesets can lint every OpenAPI route, and can block publishing on a chosen severity ([4](https://scalar.com/products/docs/configuration/scalar.config.json)).

## Authoring experience

- Markdown and MDX, with frontmatter, JSX, JavaScript expressions, imported components, and a project `snippets` folder that is available on every page ([17](https://scalar.com/products/docs/content/mdx)).
- Docs-as-code: content stays in the repo, navigation and site settings in one `scalar.config.json`, with JSON-schema autocomplete in VS Code and Cursor ([4](https://scalar.com/products/docs/configuration/scalar.config.json)).
- Git Sync with GitHub (Scalar GitHub App) and Bitbucket. GitLab is not documented ([4](https://scalar.com/products/docs/configuration/scalar.config.json), [16](https://scalar.com/products/docs/integrations/github)).
- Branching and review: preview deployment per pull request, optional PR comment with the preview link, publish on merge to the tracked branch ([14](https://scalar.com/products/docs/deployment/preview-deployments), [13](https://scalar.com/products/docs/deployment/automatic-deployment)).
- The GitHub App requests Contents, Pull requests, and Metadata on selected repositories only. It cannot read branch protection or repo settings ([16](https://scalar.com/products/docs/integrations/github)).
- Browser editor at `docs.scalar.com` for teams that do not want Git. It previews MDX snippets ([3](https://scalar.com/products/docs/getting-started), [17](https://scalar.com/products/docs/content/mdx)).
- Built-in MDX components: buttons, callouts, cards, code blocks, details, embeds, fields, grids, icons, images, math, tabs, tables, timelines, tooltips, steps ([1](https://scalar.com/products/docs)).
- WYSIWYG rich-text editing: not verified. Official pages describe a Markdown/MDX editor with preview, not a WYSIWYG mode.

## Customization and theming

- Custom domains with auto-provisioned Let's Encrypt TLS. CNAME to `dns.scalar.com`, DNS-only, no proxy or CDN in front. Subpath hosting (several projects on one domain) is Business and above ([6](https://scalar.com/products/docs/configuration/domains), [2](https://scalar.com/pricing)).
- 13 built-in themes, plus a path to your own `.css` file or a team custom theme ([7](https://scalar.com/products/docs/configuration/themes)).
- Branding: light/dark logos, color scheme, announcement banner, custom HTML footer, social card templates in TSX ([8](https://scalar.com/products/docs/configuration/site-config)).
- Custom HTML/CSS/JS: `<head>` meta tags, styles, and scripts with `async`/`defer` and tag position control ([8](https://scalar.com/products/docs/configuration/site-config)). Custom CSS/JS is Pro and above ([2](https://scalar.com/pricing)).
- Layout control per site and per page: table of contents, header, page title, page actions, prev/next, last updated date, search position, color-scheme toggle ([8](https://scalar.com/products/docs/configuration/site-config)).
- RSS feeds for changelog and blog pages ([8](https://scalar.com/products/docs/configuration/site-config)).
- Extensibility is config, MDX components, and custom code. A Docs plugin or extension API is not documented. Not verified.

## Search, AI, and analytics

- Built-in search indexes guide pages and API content: parameter names, request and response fields, models, webhooks, AsyncAPI content. It is on by default, can be placed in header or sidebar, and can be disabled. The index is rebuilt at publish ([8](https://scalar.com/products/docs/configuration/site-config)).
- Ask AI is on by default for every Docs project. It answers from published content across pages and can be turned off in the dashboard ([10](https://scalar.com/products/docs/configuration/ask-ai)).
- Ask AI does not read AsyncAPI documents, so it cannot describe channels or messages ([10](https://scalar.com/products/docs/configuration/ask-ai)).
- Every published site serves `/llms.txt` and `/llms-full.txt` automatically, generated from navigation and content ([9](https://scalar.com/products/docs/configuration/llms-txt)).
- Docs MCP endpoint at `https://<your-domain>/mcp` works with Cursor, Claude Code, and other MCP clients ([10](https://scalar.com/products/docs/configuration/ask-ai)). A hosted MCP server is Pro and above ([2](https://scalar.com/pricing)).
- A reusable Scalar Docs skill installs into coding agents with `npx skills add scalar/scalar --skill scalar-docs` ([12](https://scalar.com/products/docs/configuration/agent-skills)).
- Content Signals let you declare `search`, `ai-input`, and `ai-train` preferences in the generated `robots.txt` ([8](https://scalar.com/products/docs/configuration/site-config), [18](https://scalar.com/products/docs/privacy)).
- Analytics: first-party page views recorded server-side. No third-party scripts, no tracking cookies. Records path, referrer, client family, and whether the visitor is a person, bot, LLM crawler, or MCP client ([18](https://scalar.com/products/docs/privacy)).
- Visitor IDs are a daily-rotating keyed hash of IP and user agent; IP addresses are not stored. Analytics can be turned off per project ([18](https://scalar.com/products/docs/privacy)).
- Page feedback (thumbs up/down with a reason) is off by default and its votes appear under Settings → Analytics ([8](https://scalar.com/products/docs/configuration/site-config), [18](https://scalar.com/products/docs/privacy)).
- Ask AI usage is reported as messages, tokens, and credits under Team → Usage ([10](https://scalar.com/products/docs/configuration/ask-ai)).

## Collaboration and access control

- Team roles: Owner, Admin, Editor. Viewers read docs and do not consume an editor seat ([20](https://scalar.com/resources/user-management)).
- Editors create and edit docs, APIs, SDKs, and themes. Admins manage members, roles below Owner, and billing. Owners add Owners and delete the team ([20](https://scalar.com/resources/user-management)).
- Editor seats: 1 on Free, 5 on Pro, 10 on Business, custom on Enterprise. Viewer seats are included on all plans ([2](https://scalar.com/pricing)).
- SSO/SAML on Business and Enterprise, with guides for Auth0, Google, Microsoft Entra ID, Okta, OneLogin, and Ping Identity. Token encryption is required ([21](https://scalar.com/resources/sso/getting-started)).
- RBAC is Enterprise only; domain restrictions on invites are Enterprise; plain email domain access control is Pro and above ([2](https://scalar.com/pricing), [20](https://scalar.com/resources/user-management)).
- Private docs: turn on `isPrivate`, then allow access groups by email domain, specific email addresses, or both. Access groups are Pro and above; a custom login portal brand the sign-in page ([11](https://scalar.com/products/docs/configuration/private-docs)).
- Versioning covers doc versions through the `versions` config, and deployments can be rolled back to a previous build with the CLI ([5](https://scalar.com/products/docs/configuration/versions), [15](https://scalar.com/products/docs/deployment/cli)).
- Personalization: a signed `userInfoHook` endpoint can return visitor groups and content values to vary what signed-in readers see ([8](https://scalar.com/products/docs/configuration/site-config)).
- Localization / i18n for Docs sites: no official page or config property documents it. Not verified as supported.
- The published site itself is unauthenticated on Free and Pro unless you enable private docs; access groups are the only reader-level gate ([11](https://scalar.com/products/docs/configuration/private-docs)).

## Pricing

Prices from the pricing page ([2](https://scalar.com/pricing)):

- **Free — $0.** Hosted OpenAPI docs, API client, landing pages, themes, API references. Up to 3 APIs, 1 SDK up to 25 endpoints, 50 Agent Scalar credits, 1 editor seat, unlimited viewers. No credit card. Docs publishing is not included after the trial.
- **Pro — $150/month, or $125/month billed yearly ($1,500/year).** Custom domains and subdomains, Git Sync, Markdown + MDX, full developer portal, access groups, hosted MCP servers, version deploys, email domain access control. Up to 15 APIs, 1 SDK up to 100 endpoints, 500 Agent Scalar credits, 5 editor seats.
- **Business — $600/month, or $500/month billed yearly ($6,000/year).** Everything in Pro plus SSO/SAML, subpath hosting, discount on additional SDKs. Up to 25 APIs, 1 SDK up to 250 endpoints, 2,000 Agent Scalar credits, 10 editor seats.
- **Enterprise — custom.** Full developer portals, SSO/SAML and RBAC, unlimited APIs, custom SDK size, priority support and SLAs, migration services, dedicated Slack or Teams channel.
- Every new team starts with a 7-day trial with Pro limits.
- Add-ons: extra SDKs cost $150/month each up to 100 endpoints, or $600/month each for 101–250 endpoints. An SDK is one language target for one API. Volume discounts exist on Business and Enterprise.
- Agent Scalar credits: one credit covers 200 MCP tool calls, 2 Docs chat messages, or 50,000 reference-model tokens. Credits reset each monthly period and do not roll over.
- Free tier bottom line: free hosted API docs exist, but a Docs site with guides, custom domain, and Git Sync needs Pro.

## Strengths

- Interactive references come from the same OpenAPI document, so docs track the spec ([1](https://scalar.com/products/docs)).
- Guides and references share one navigation, one search, and one domain ([1](https://scalar.com/products/docs)).
- The renderer is MIT-licensed and widely adopted; you can self-host it free and upgrade to Docs later ([19](https://scalar.com/products/api-references)).
- Strong docs-as-code loop: Git Sync, PR previews, PR comments, publish on merge, CLI deploy, rollback ([14](https://scalar.com/products/docs/deployment/preview-deployments), [15](https://scalar.com/products/docs/deployment/cli)).
- AI readiness is automatic: `/llms.txt`, `/llms-full.txt`, Ask AI, and an MCP endpoint on every site ([9](https://scalar.com/products/docs/configuration/llms-txt), [10](https://scalar.com/products/docs/configuration/ask-ai)).
- Privacy-first analytics with no third-party trackers, plus Content Signals control for AI crawlers ([18](https://scalar.com/products/docs/privacy)).
- Broad authoring surface: MDX with JSX, snippets, math, tabs, and custom CSS/JS without ejecting ([17](https://scalar.com/products/docs/content/mdx), [8](https://scalar.com/products/docs/configuration/site-config)).
- OpenAPI linting with Spectral can block a bad publish ([4](https://scalar.com/products/docs/configuration/scalar.config.json)).
- Reader-level access groups do not consume editor seats ([20](https://scalar.com/resources/user-management)).

## Weaknesses and limits

- Docs publishing is paid only. The free tier cannot host a Docs site past the trial ([2](https://scalar.com/pricing)).
- No GitLab integration; only GitHub and Bitbucket are documented ([16](https://scalar.com/products/docs/integrations/github)).
- No GraphQL reference support; the client's GraphQL support is "Coming Soon" ([2](https://scalar.com/pricing)).
- Ask AI ignores AsyncAPI content, so event-driven APIs get no AI answers ([10](https://scalar.com/products/docs/configuration/ask-ai)).
- Localization and multi-language sites are not documented. Not verified as supported.
- No WYSIWYG editor is documented; authoring is Markdown/MDX ([17](https://scalar.com/products/docs/content/mdx)).
- The platform is SaaS only. Self-hosting covers the renderer and tooling, not Docs itself ([1](https://scalar.com/products/docs), [22](https://github.com/scalar/scalar)).
- Custom domains cannot sit behind your own CDN or WAF; traffic must reach Scalar directly and CNAMEs must be unproxied ([6](https://scalar.com/products/docs/configuration/domains)).
- Search quality depends on a rebuild: updated API content is only indexed at the next publish ([8](https://scalar.com/products/docs/configuration/site-config)).
- SSO/SAML starts at Business ($600/month), and full RBAC and invite domain restrictions are Enterprise only ([2](https://scalar.com/pricing), [20](https://scalar.com/resources/user-management)).
- Editor seats are low relative to price: 5 on Pro, 10 on Business ([2](https://scalar.com/pricing)).
- Price scales with API count and SDK endpoint count, with per-SDK add-ons up to $600/month each ([2](https://scalar.com/pricing)).
- No Docs entry in the public changelog; only API Client, API Reference, Agent, Mock Server, and SDK Generator have release notes ([24](https://scalar.com/changelog)).
- Agent Scalar credits reset monthly and do not roll over ([2](https://scalar.com/pricing)).

## Sources

1. https://scalar.com/products/docs
2. https://scalar.com/pricing
3. https://scalar.com/products/docs/getting-started
4. https://scalar.com/products/docs/configuration/scalar.config.json
5. https://scalar.com/products/docs/configuration/versions
6. https://scalar.com/products/docs/configuration/domains
7. https://scalar.com/products/docs/configuration/themes
8. https://scalar.com/products/docs/configuration/site-config
9. https://scalar.com/products/docs/configuration/llms-txt
10. https://scalar.com/products/docs/configuration/ask-ai
11. https://scalar.com/products/docs/configuration/private-docs
12. https://scalar.com/products/docs/configuration/agent-skills
13. https://scalar.com/products/docs/deployment/automatic-deployment
14. https://scalar.com/products/docs/deployment/preview-deployments
15. https://scalar.com/products/docs/deployment/cli
16. https://scalar.com/products/docs/integrations/github
17. https://scalar.com/products/docs/content/mdx
18. https://scalar.com/products/docs/privacy
19. https://scalar.com/products/api-references
20. https://scalar.com/resources/user-management
21. https://scalar.com/resources/sso/getting-started
22. https://github.com/scalar/scalar
23. https://github.com/scalar/scalar/blob/main/LICENSE
24. https://scalar.com/changelog
25. https://scalar.com/security
26. https://github.com/scalar/scalar/pull/10489
27. https://github.com/scalar/scalar/pull/10487
