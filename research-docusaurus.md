# Docusaurus

Research date: 2026-11-09. Current stable release: 3.10.2 (2026-07-10) [1][19].

## Summary

Docusaurus is an open-source static site generator for documentation sites, built with React and MDX [2]. You write Markdown or MDX files, and it builds a single-page React application with static HTML for every route [2]. It ships documentation features out of the box: sidebar navigation, docs versioning, blog, i18n, and search integration [2]. It targets open-source projects and engineering teams that want docs-as-code, hosted on their own infrastructure or a Jamstack provider [2][5]. Meta (Facebook) maintains it, with a large community of contributors [20][18].

## Hosting and deployment model

- **Type:** static site generator. It outputs static HTML/JS assets that you host yourself or on a static host [2].
- **Not SaaS.** There is no Docusaurus cloud, no hosted editor, and no hosted docs product. No pricing page exists; https://docusaurus.io/pricing returns HTTP 404 [16].
- **Deployment targets:** self-hosting behind Nginx/Apache, Jamstack providers such as Netlify and Vercel, and GitHub Pages [5].
- **Local check:** `docusaurus serve` serves the production build locally before you deploy [5].
- **License:** code is MIT, copyright Facebook/Meta [3]. Website documentation content is CC-BY-4.0 [4].
- **Version 4 status:** on `main`, `@docusaurus/core` is at 4.0.0 and npm publishes `4.0.0-canary-*` builds. No stable v4 release exists yet [1][21].

## API reference support

Docusaurus has **no built-in API reference renderer**. The options below come from community plugins, listed on the official resources page [6].

- **OpenAPI/Swagger:** no official plugin. Community options include `docusaurus-openapi-docs` ("a plugin and theme for generating interactive OpenAPI docs") and `redocusaurus` ("a preset for integrating OpenAPI documentation into your docs with Redoc") [6].
- **OpenAPI version coverage (Swagger 2.0, 3.0, 3.1):** not verified. The Docusaurus site makes no claim; each plugin's own repo would need checking.
- **AsyncAPI:** not verified. No AsyncAPI plugin appears in the official community resources list [6].
- **GraphQL:** no built-in support. Community plugin `@graphql-markdown/docusaurus` generates docs from GraphQL schemas [6]. The same list has a Protobuf toolset, `docusaurus-protobuffet` [6].
- **Interactive "try it" console:** not part of core. It depends on the chosen OpenAPI plugin and its renderer [6].
- **Code samples / SDK snippets:** core Markdown handles code blocks, syntax highlighting, and code tabs. `@docusaurus/theme-live-codeblock` adds live editable blocks [7][12].
- **Multiple API versions:** core docs versioning covers this. The versioning CLI snapshots `docs` into `versioned_docs`, with per-version sidebars and a version dropdown [10]. Multi-instance docs (several content-plugin instances with different `id`s) let you run separate doc sets, for example one per API product [13][14].

## Authoring experience

- **Markdown and MDX:** both supported. Files compile through the MDX compiler, so you can embed JSX and React components in Markdown [7]. Docusaurus v3 uses the MDX format by default, with experimental CommonMark support via `markdown.format` [7].
- **Markdown features:** YAML front matter, admonitions, tabs, code blocks with highlighting, images, and MDX components [7].
- **WYSIWYG editor:** none. There is no official visual editor. A community plugin (`docusaurus-plugin-dhub`) opens pages in an external visual MDX editor [6].
- **Git sync:** no built-in GitHub/GitLab integration and no two-way sync. Content lives in your repo, so Git is the sync mechanism [2].
- **Docs-as-code:** this is the core model. Content is files in your repo, built by CLI commands (`docusaurus start`, `docusaurus build`) with hot reload [2][5].
- **Edit links:** the docs plugin `editUrl` option (string or function) adds an "Edit this page" link to the source file on GitHub or GitLab. `editLocalizedFiles` and `editCurrentVersion` control which file the link targets [13].
- **Last-update metadata:** `showLastUpdateAuthor` and `showLastUpdateTime` derive author and timestamp from Git history [13].
- **Branching and review:** handled by Git and your CI, not by Docusaurus. Pull requests, CODEOWNERS, and preview deploys are host/CI concerns [20][5].

## Customization and theming

- **React components:** you own the layout code and can write your own React components for any part of the site [2].
- **Swizzling:** the supported way to override theme components. Ejecting copies a theme component for full customization; wrapping adds behavior around the original [8].
- **Styling:** global CSS via `customCss`, Infima CSS variables, CSS modules, and a documented set of stable theme class names for safe selectors [9].
- **Theming system:** dark mode is built in [2]. Themes load like plugins and can be swapped [14].
- **Plugins and presets:** `plugins` and `themes` arrays in `docusaurus.config.js`, Babel-style options tuples, local plugin paths, and presets such as `@docusaurus/preset-classic` [14].
- **Official plugins:** content plugins (docs, blog, pages), plus sitemap, PWA, ideal-image, client-redirects, svgr, debug, rsdoctor, css-cascade-layers, and analytics plugins [12].
- **Custom domain:** supported, but it is a hosting-provider setting. Configure `url`, `baseUrl`, and `trailingSlash` in `docusaurus.config.js`, then set DNS and TLS at the host [5].
- **Branding:** logo, favicon, navbar, footer, announcement bar, and color mode are configured in `themeConfig` [5][9].

## Search, AI, and analytics

- **Search:** no built-in search index. First-class support is for Algolia DocSearch, which is free for public developer docs and technical blogs [15]. Contextual search, which filters results by current version and locale, is on by default [15].
- **Search alternatives:** Typesense DocSearch and local/offline search plugins (Lunr, Pagefind, Orama, Meilisearch) are community-maintained [15][6].
- **AI assistant:** via Algolia's "Ask AI". You set an `askAi` assistant ID in the Algolia config, and the assistant answers from your Algolia index [15]. The integration is free; you pay your LLM provider, and you bring your own LLM [15].
- **llms.txt:** not built in. `https://docusaurus.io/llms.txt` returns HTTP 404, and no official `@docusaurus/plugin-llms` package exists on npm [17][1]. Community plugins `docusaurus-plugin-llms` and `docusaurus-plugin-llms-txt` generate `llms.txt` and `llms-full.txt` [6].
- **MCP server:** no official Docusaurus MCP server. Community options: `@agentreadyweb/docusaurus-plugin` (MCP-queryable index with cited answers) and `Doc Bridge` (indexes docs for coding agents) [6].
- **Analytics:** official plugins for Google Analytics, Google Tag Manager, Google gtag, and Vercel Analytics [12]. PostHog and Yandex Metrika are community plugins [6].
- **SEO:** static HTML per route, per-page SEO metadata, `sitemap.xml` from the sitemap plugin, and `hreflang` tags for locales [2][11][12].

## Collaboration and access control

- **Team roles and permissions:** none. There is no user model, no roles, and no admin UI, because the output is a static site [2].
- **SSO:** none built in. Any SSO must come from the host or a proxy in front of the site. The docs do not describe SSO support.
- **Private/authenticated docs:** no native support. The search docs note that sites behind a firewall cannot use hosted DocSearch and must self-host the crawler, so auth is an external concern [15].
- **Versioning:** built in. CLI-generated version snapshots, `versions.json`, per-version sidebars, a version dropdown, per-version banners (for example `unmaintained`), and `onlyIncludeVersions` to limit the build [10][13].
- **Localization (i18n):** built in. Locale config, `docusaurus write-translations`, per-locale content directories, RTL support, `hreflang` tags, and translation via Git or Crowdin [11].
- **Combining both:** versioning and i18n are orthogonal. You can combine multiple versions with multiple locales, and contextual search filters on both [10][11][15].
- **Review workflow:** Git-based only (pull requests, CI previews). No in-product comments, suggestions, or approvals [2][5].

## Pricing

- **No paid plans.** Docusaurus is free and open source under MIT, with no pricing page and no commercial tier [3][16].
- **Free tier:** the entire product. Unlimited sites, pages, and builds, limited only by your own hosting and CI costs [3].
- **Costs you may still pay:** hosting (Netlify, Vercel, GitHub Pages, or your own servers), Algolia DocSearch (free for eligible public docs), and LLM usage if you enable Ask AI [5][15].
- **Support:** community only, via Stack Overflow, Discord, and GitHub. No paid support plan is listed [18].
- **Optional sponsorship:** GitHub Sponsors and open-source sponsorship fund maintenance. Sponsorship is not a product plan [20].

## Strengths

- Free and MIT-licensed, with no vendor lock-in and no seat pricing [3][2].
- Docs-as-code with Markdown/MDX and full React component power [2][7].
- Strong built-in docs features: versioning, i18n, sidebar generation, edit links, and last-update metadata [10][11][13].
- Deep theming control through swizzling, CSS variables, and stable theme class names [8][9].
- Large plugin ecosystem, including OpenAPI, GraphQL, and Protobuf documentation plugins [6].
- First-class Algolia DocSearch, with free hosted search for public docs and optional Ask AI [15].
- Static output is fast, SEO-friendly, and deployable almost anywhere [2][5].
- Large community and Meta backing, with an active release cadence [1][20].

## Weaknesses and limits

- No API reference renderer in core. OpenAPI, AsyncAPI, and GraphQL support depend on third-party plugins with their own maintenance risk [6].
- No WYSIWYG editor and no visual editing for non-technical writers [6].
- No team roles, SSO, permissions, comments, or review workflow. Collaboration is entirely Git-based [2].
- No native private/authenticated docs. You must add auth at the host, proxy, or CDN layer [15].
- No built-in search index. You must set up Algolia or install a community search plugin [15].
- No official llms.txt or MCP server support. AI-readiness needs community plugins [6][17].
- Requires Node.js, npm, and React/JS knowledge. Non-developers cannot maintain a site alone [2].
- Versioning adds build time and contributor complexity. The docs warn against adopting it early [10].
- Upgrades can be disruptive. The v2 to v3 move changed MDX behavior, and v4 is still canary with future flags [19][21].

## Sources

1. https://registry.npmjs.org/@docusaurus/core
2. https://docusaurus.io/docs
3. https://raw.githubusercontent.com/facebook/docusaurus/main/LICENSE
4. https://raw.githubusercontent.com/facebook/docusaurus/main/LICENSE-docs
5. https://docusaurus.io/docs/deployment
6. https://docusaurus.io/community/resources
7. https://docusaurus.io/docs/markdown-features
8. https://docusaurus.io/docs/swizzling
9. https://docusaurus.io/docs/styling-layout
10. https://docusaurus.io/docs/versioning
11. https://docusaurus.io/docs/i18n/introduction
12. https://docusaurus.io/docs/api/plugins
13. https://docusaurus.io/docs/api/plugins/@docusaurus/plugin-content-docs
14. https://docusaurus.io/docs/using-plugins
15. https://docusaurus.io/docs/search
16. https://docusaurus.io/pricing (HTTP 404)
17. https://docusaurus.io/llms.txt (HTTP 404)
18. https://docusaurus.io/community/support
19. https://raw.githubusercontent.com/facebook/docusaurus/main/CHANGELOG.md
20. https://github.com/facebook/docusaurus
21. https://raw.githubusercontent.com/facebook/docusaurus/main/packages/docusaurus/package.json
