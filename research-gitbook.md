# GitBook (API docs)

Researched 2026-11-09. All facts below come from GitBook's own site, docs, changelog, or GitHub repo. Unverified items are marked "not verified".

## Summary

GitBook is a hosted documentation platform for product and API docs [1]. You import an OpenAPI or Swagger spec and GitBook renders an interactive API reference that updates when the spec changes [1][3]. It also publishes normal guide pages in the same site, so API reference and prose live together [1]. It targets developer-relations, docs, and product teams that want a visual editor plus a Git workflow [1][22]. It is a closed-source SaaS with an open-source renderer [17][18].

## Hosting and deployment model

- SaaS. GitBook hosts the editor and the published site; you sign up at `app.gitbook.com` [2].
- Default published URL is `[subdomain].gitbook.io`; a custom domain is available from the Essential plan up [2][9].
- No self-hosted product edition is documented. The docs index has no self-hosting page [19].
- The rendering layer is open source: `GitBookIO/gitbook`, described as "the open source frontend for GitBook doc sites" [17].
- License is GNU GPLv3 [17][18]. To distribute the code you must keep it public; a private fork needs a commercial license [18].
- The README warns that self-hosting is possible but "we do not recommend this", and GitBook gives no support or updates for forks [18].
- The repo is active: last push 2026-11-09, about 29k stars [17].
- Legacy GitBook (the old CLI) is in the same repo's "deprecated" section [18].

## API reference support

- Spec versions accepted for file upload, hosted URL, and CLI: Swagger 2.0, OpenAPI 3.0, OpenAPI 3.1 (including `webhooks`) [3][4].
- Specs can be uploaded, fetched from a URL, or published with `gitbook openapi publish` [4].
- URL-linked specs are re-checked every 6 hours; there is a manual "Check for updates" action [4].
- Imported operations appear as API blocks on a page, or as a full API reference section [3].
- Layout is configurable: one page per tag or one page per operation [3].
- "Test it" endpoint console is built in and powered by Scalar [1][3].
- Code samples: GitBook generates generic examples automatically, and `x-codeSamples` adds custom language- or SDK-specific snippets [5].
- Multiple specs are supported; each spec is named in the OpenAPI panel [4].
- Spec versions are tracked separately through the Platform API (`openapi-spec-versions` endpoints) [19].
- Multiple published API versions use site variants (e.g. v1, v2, v3) [15].
- AsyncAPI: no support documented. Not verified.
- GraphQL: no support documented. Not verified.

## Authoring experience

- Block-based WYSIWYG web editor [22].
- Markdown is supported as an input syntax in the editor, with the usual inline, heading, list, and code-block forms [7].
- Content is stored as GitBook-flavored Markdown with `{% %}` blocks, e.g. `{% openapi %}` [3].
- MDX support is not documented. Not verified.
- Git Sync is a two-way sync with GitHub or GitLab [6].
- Edits in the GitBook editor sync to the repo, and commits in the repo sync back [6].
- Git Sync supports monorepos, content configuration as code, commit autolinks, and GitHub pull-request previews [19].
- Only admins and creators can enable Git Sync [6].
- Branching is built in as change requests, modelled on pull requests [13].
- Change requests have split or inline diff review, optional review requests, merge rules, and full page history with rollback [2][13].
- Imports exist for Markdown, Google Docs, Confluence, Notion, and MS Word [2].
- An official `SKILL.md` and CLI let coding agents work on Git-synced content [19].

## Customization and theming

- Custom domain is available from Essential, and custom subdirectory from Ultimate [2][9].
- Branding options: custom logo, icon style, custom fonts, footer, bold/gradient header themes, semantic colors, code and API block themes [8].
- Customization can be set site-wide, or per section and per variant [8].
- Custom CSS, HTML, or JS cannot be injected [8].
- Page layout cannot be changed [8].
- The "Powered by GitBook" link cannot be removed [8].
- Extensibility is through integrations and custom components, not a plugin API for site code [20].
- Custom integrations are built with the GitBook CLI, ContentKit components, and the Platform API [19][20].
- About 70 built-in integrations are listed, covering Git, analytics, auth, support, and feature flags [20].
- Many embeds (CodePen, Figma, Mermaid, Loom, YouTube, and others) work without installation [20].

## Search, AI, and analytics

- Full-text search is built in and included on all plans [2].
- Search results deep-link to the page section [2].
- AI Assistant Ask (answers in the search box) is on Essential and above at 20 credits per relevant question [2].
- AI Assistant Chat (chat sidebar) is Ultimate and Enterprise only [2].
- GitBook Agent writes and edits docs; Free is limited to 10 messages per week [2].
- Every published site gets an MCP server at `/~gitbook/mcp` [10].
- Every page has a Markdown version via `.md` [10].
- `llms.txt` and `llms-full.txt` are generated automatically on all plans [2][10].
- WebMCP support lets in-browser agents search docs and fetch Markdown [2].
- GitBook MCP (`mcp.gitbook.com/mcp`) lets external agents create sites, draft pages, and open change requests [21].
- Analytics reports: Traffic, Agents & MCP, and AI Assistant insights [11].
- Traffic covers page views, landing pages, searches, and feedback, with filters and period comparisons [11].
- Agents & MCP tracks traffic from LLMs, coding agents, and crawlers [11].
- Extra analytics: search analytics, user feedback, broken links, content gaps [2][11].
- Google Analytics and other analytics integrations are available [20].
- Traffic is never limited or charged by page views [2].

## Collaboration and access control

- Roles: guest, reader, commenter, editor, reviewer, admin [12].
- Basic roles (admin, creator, editor, reader) are on all plans; reviewer and commenter need Essential or above [2].
- Teams and team owners: teams from Essential, team owners only on Enterprise [2].
- Every member counts toward billing, including readers and guests [12].
- Real-time collaboration, review and approve, and reusable content need Essential or above [2].
- SAML SSO is Enterprise only; Google/email domain SSO is on all plans [2].
- Private share links (revocable unique URL) are available from Essential [2].
- Authenticated access (Okta, Azure, Auth0, or your own auth server) is Ultimate and Enterprise [2][14].
- Auth uses built-in `/~gitbook/auth/login` and `/~gitbook/auth/logout` URLs [14].
- Version history with rollback is on all plans; site variants for releases are on all plans [2][15].
- Localization: AI auto-translations at 30 credits per 1k words, included in Ultimate and Enterprise, paid on Essential [2].
- Translation workflows re-run only for pages that changed in the source [16].
- Sites can also use language variants with localized section titles [15][19].

## Pricing

All prices below are per month with annual billing; annual billing is described as "2 months free" [2].

| Plan | Price | Key limits |
| --- | --- | --- |
| Free | $0 | 1 user; unlimited page views; unlimited sites not stated; LLM optimizations, MCP server, Git Sync, API docs, preview deploys, advanced customization; GitBook Agent limited to 10 messages/week; no custom domain, no AI Assistant, no translations [2] |
| Essential | $65 per site/mo + $12 per user/mo | 2,000 AI credits ($20) per month; AI Assistant Ask; custom domain; analytics, search analytics, user feedback; redirects; reusable content; teams; 14-day trial [2] |
| Ultimate | $249 per site/mo + $12 per user/mo | 10,000 AI credits ($100) per month; AI Assistant Chat; AI insights; GitBook Agent; adaptive content; authenticated access; site sections and groups; channels; content gaps; broken links; priority support [2] |
| Enterprise | Custom | SAML SSO; white-glove migration; custom integrations; 1:1 support; training; custom contract and invoicing; unlimited adaptive content; Git Sync IP allowlisting; team owners [2] |

- Extra AI credits: 5,000 for $47.50, 10,000 for $90, 15,000 for $127.50, 40,000 for $300 [2].
- Example total on the pricing calculator: 1 Ultimate site + 1 user = $261/month, $3,132/year [2].
- Page views and readers are never charged; only members are [2][12].
- Open-source projects can apply for a free Community plan [19].

## Strengths

- OpenAPI 3.1 support, including `webhooks`, is documented explicitly [3].
- Specs auto-update from a URL every 6 hours, or from CI with the CLI [4].
- "Test it" console is on every plan, including Free [2][3].
- `x-codeSamples` gives full control of SDK snippets [5].
- Two-way GitHub/GitLab sync keeps a visual editor and docs-as-code in one workflow [6].
- Change requests mirror pull requests, with diff review and merge rules [13].
- AI-ready output is automatic: `.md` pages, `llms.txt`, `llms-full.txt`, and an MCP server per site [10].
- Auth-endpoint coverage is broad: SAML, OIDC, Okta, Azure, Auth0, or custom [2][20].
- Unlimited page views on every plan, including Free [2].
- Renderer source is public under GPLv3 [17].

## Weaknesses and limits

- No AsyncAPI or GraphQL reference support is documented; only OpenAPI/Swagger [3].
- No self-hosted product. Self-hosting the renderer is unsupported and discouraged [18].
- No custom CSS, JS, or HTML injection [8].
- Page layout is fixed, and the "Powered by GitBook" badge cannot be removed [8].
- Per-site pricing plus per-user pricing makes cost grow fast for several sites or large teams [2].
- Authenticated access, SAML SSO, and site sections need Ultimate or Enterprise [2].
- AI features burn credits; usage auto-pauses when credits run out [2].
- Translate and AI Assistant costs are credit-based on Essential, which is hard to forecast [2].
- Git Sync IP allowlisting is Enterprise only [2][6].
- Self-service trial is 14 days; the Free plan is one user only [2].
- MDX authoring is not documented [7].

## Sources

1. https://www.gitbook.com/solutions/api
2. https://www.gitbook.com/pricing
3. https://gitbook.com/docs/create-content/openapi
4. https://gitbook.com/docs/create-content/openapi/add-an-openapi-specification
5. https://gitbook.com/docs/create-content/openapi/guides/adding-custom-code-samples
6. https://gitbook.com/docs/docs-as-code/git-sync
7. https://gitbook.com/docs/create-content/formatting/markdown
8. https://gitbook.com/docs/manage-your-site/customization
9. https://gitbook.com/docs/publish/custom-domain
10. https://gitbook.com/docs/getting-started/llm-ready-docs
11. https://gitbook.com/docs/analytics/insights
12. https://gitbook.com/docs/collaborate/member-management/roles
13. https://gitbook.com/docs/collaborate/change-requests
14. https://gitbook.com/docs/publish/site-audience/authenticated-access
15. https://gitbook.com/docs/manage-your-site/site-structure/variants
16. https://gitbook.com/docs/gitbook-agent/translations
17. https://github.com/GitBookIO/gitbook
18. https://github.com/GitBookIO/gitbook/blob/main/README.md
19. https://gitbook.com/docs/llms.txt
20. https://www.gitbook.com/integrations
21. https://www.gitbook.com/features/mcp
22. https://www.gitbook.com/features/editor
23. https://changelog.gitbook.com/
