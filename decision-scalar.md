# Decision: Use Scalar Docs for our API documentation

- **Status:** Decided
- **Date:** 2026-11-09
- **Full comparison:** https://mattmsh.github.io/api-docs-tools-comparison/

## Summary

We will use [Scalar Docs](https://scalar.com/products/docs) for our API documentation.
We compared four tools: Scalar Docs, GitBook, Docusaurus, and Mintlify.
Scalar covers every capability we need, at the lowest price for that set.
It builds API docs from our OpenAPI spec, supports MDX, and syncs with our Git repository.
The same spec also generates our SDKs, a hosted MCP server for AI agents, and API Client collections.
No other tool we compared does all of this from one spec.

## Why we chose Scalar

### 1. API docs come from the spec

- Scalar generates the API reference from our OpenAPI document. The docs stay in step with the API.
- It supports Swagger 2.0, OpenAPI 3.0, 3.1, and 3.2.
- OpenAPI 3.2 support covers nested tags, `querystring` parameters, custom HTTP methods (`additionalOperations`), streaming responses (`itemSchema`), OAuth 2.0 device authorization, and OAuth server metadata.
- The hosted MCP server and the mock server also read OpenAPI 3.2 documents.
- It also supports AsyncAPI, so event-driven APIs get the same treatment.
- Each operation has a **Test Request** button. Readers can call the API from the docs.
- It generates code samples for cURL, JavaScript, Python, Go, and other languages.
- Spectral linting can block a publish when the spec has errors.

### 2. One spec powers docs, SDKs, MCP, and the API client

We keep our OpenAPI document in the Scalar Registry or in our repository.
Every product below reads from it, so docs, SDKs, and AI tools cannot drift from the API.

**SDK generator**

- Generates type-safe SDKs and a CLI from our OpenAPI document.
- TypeScript, Python, Go, Java, Kotlin, Ruby, and CLI targets are generally available. Six more languages are experimental.
- Auth is wired from our security schemes: API keys, Basic, Bearer, OAuth 2.0, and OIDC.
- Supports server-sent events, NDJSON, WebSockets, and multipart uploads.
- Releases arrive as pull requests in our own GitHub repositories. Manual edits to generated code survive each rebuild.
- Each SDK ships with an Agent Skill, so coding agents call our API correctly.

**MCP server (Agent Scalar)**

- Turns our OpenAPI document into a hosted MCP server. There is no server for us to deploy.
- Claude, ChatGPT, and any remote MCP client can call the operations we allow.
- Auth is delegated: OAuth, API keys, or bearer tokens per installation. Agents never see our upstream credentials.
- We choose which APIs and endpoints each installation can call. Servers are private by default.
- It uses three tools and loads operation details only when needed, so it stays small in the model's context.
- Our docs site also gets its own MCP endpoint at `/mcp`, plus `llms.txt` and Ask AI.

**API Client**

- Free, open-source (MIT) client for the browser and for macOS, Windows, and Linux.
- Imports our OpenAPI document as a ready-made collection and updates when the file changes.
- Supports environments, pre-request scripts, and response tests with the Postman-compatible `pm` API.
- It is the same client that opens when a reader clicks **Test Request** in our docs.

**Registry**

- Stores and versions our OpenAPI and AsyncAPI documents, shared JSON Schemas, and Spectral rules.
- Publishes a new spec version from GitHub Actions on every merge.
- A new spec version updates the docs and the SDKs from the same source.

### 3. Guides are written in MDX

- We write guides in Markdown or MDX, next to the API reference.
- MDX lets us use JSX, imported components, and shared snippets.
- Built-in components include callouts, tabs, cards, steps, code blocks, and math.
- People who do not use Git can edit pages in the web editor at `docs.scalar.com`.

### 4. Docs live in our repository

- Content and the `scalar.config.json` file stay in our repository. Docs changes go through the same pull requests as code.
- Our code is on GitHub, and Scalar has a GitHub App for Git Sync. The app only gets access to the repositories we select.
- The app publishes on merge. It builds a preview of every pull request and can post the preview link as a PR comment.
- The `scalar` CLI publishes from any CI. You can also use it to roll back to an earlier build.

### 5. It has the most capabilities for the best price

On Pro ($125/month, billed yearly) we get:

- A custom domain, Git Sync, MDX guides, and up to 15 APIs.
- 1 generated SDK (one language for one API, up to 100 endpoints).
- Hosted MCP servers, with 500 Agent Scalar credits each month (up to 100,000 MCP tool calls).
- 5 editor seats. Readers do not use seats.
- Docs versions with a version selector.
- Private docs, with access by email domain or by email address.
- Built-in search that indexes guides and API fields.
- Ask AI, `llms.txt`, and a hosted MCP server, so AI tools can use our docs.
- Analytics that do not use cookies or third-party scripts.

## How the other tools compare

| Need | Scalar | GitBook | Docusaurus | Mintlify |
| --- | --- | --- | --- | --- |
| API docs generated from OpenAPI | Built in | Built in | Plugin only | Built in |
| MDX | Yes | No | Yes | Yes |
| Git sync with GitHub | Yes | Yes | Repo is the source | Yes |
| Private docs | $125/mo | $309/mo | Build it ourselves | Password only at $450/mo |
| Analytics and AI assistant | $125/mo | $125/mo | Plugins | $450/mo |
| SDK generator | Built in | Not offered | Not offered | Not offered |
| MCP server that calls our API | Built in | Docs search only | Plugin, docs only | Docs search only |
| Free open-source API client | Yes | No | No | No |
| Hosting and search included | Yes | Yes | No | Yes |
| Setup and upkeep | Config file | Low | High: we build and maintain it | Config file |

The prices assume 5 editors, one site, and yearly billing.

- **GitBook** does not support MDX or custom CSS. Private docs cost $309/month.
- **Docusaurus** has no license cost, but it is not free to run. We would have to spend time and effort to set it up and keep it running:
  - Choose, configure, and update a community plugin for the API reference.
  - Set up search (Algolia or a plugin) and the AI features.
  - Build access control for private docs ourselves.
  - Host the site and maintain the build pipeline.
  - Keep up with breaking upgrades, such as the coming v4.
- **Mintlify** is free for a public site. Analytics, preview builds, and the AI assistant cost $450/month. Reader login through our identity provider is Enterprise only.

## Cost

| Plan | Monthly (billed yearly) | Yearly | When we need it |
| --- | --- | --- | --- |
| Pro | $125 | $1,500 | Start here |
| Business | $500 | $6,000 | When we need SAML SSO, subpath hosting, more than 5 editors, or more than 15 APIs |

- Every new team gets a 7-day trial with Pro limits.
- Pro includes 500 AI credits each month. One credit covers 2 Ask AI messages or 200 MCP tool calls. Unused credits do not carry over.
- Pro includes 1 SDK. Each extra SDK costs $150/month for up to 100 endpoints, or $600/month for 101–250 endpoints. A TypeScript SDK and a Python SDK for the same API count as 2 SDKs.

## Trade-offs we accept

- **No documented localization.** We cannot publish the docs in more than one language yet.
- **SaaS only.** Scalar hosts the docs site. The API reference renderer is open source (MIT), so we can self-host the API reference if we leave.
- **No CDN or WAF in front of the custom domain.** The CNAME must point straight to Scalar.
- **SAML SSO starts at Business** ($500/month, billed yearly).
- **Extra SDK languages cost extra.** Each language beyond the first adds $150/month or more.
- **The SDK generator does not cover every OpenAPI 3.2 feature yet.** It reads 3.2 documents and supports the 3.2 OAuth device authorization flow. It does not generate `QUERY` or custom-method operations, or `querystring` parameters. It reports them as diagnostics, so nothing is dropped without warning. This gap was reported in 0.33.2 and is still open in the latest release, 0.39.0 (2026-11-06). It matters only if our API uses these features.

## Next steps

1. Start the 7-day trial at https://dashboard.scalar.com/register.
2. Install the Scalar GitHub App on our docs repository.
3. Add `scalar.config.json` and point it at our OpenAPI document.
4. Move our existing guides into MDX pages.
5. Turn on preview deployments and publish on merge.
6. Set up the custom domain: add a CNAME record for `dns.scalar.com`.
7. Turn on private docs if any content must stay internal.
8. Choose the first SDK language and connect the SDK generator to a GitHub repository.
9. Set up the MCP server and choose which endpoints agents can call.
10. Buy Pro with yearly billing before the trial ends.

## Sources

- Scalar Docs: https://scalar.com/products/docs
- Scalar pricing: https://scalar.com/pricing
- Scalar MDX: https://scalar.com/products/docs/content/mdx
- Scalar GitHub integration: https://scalar.com/products/docs/integrations/github
- Scalar preview deployments: https://scalar.com/products/docs/deployment/preview-deployments
- Scalar OpenAPI support: https://scalar.com/products/api-references/openapi
- API reference changelog (OpenAPI 3.2 features): https://scalar.com/products/api-references/changelog
- SDK generator changelog (0.33.2 to 0.39.0, 3.2 limits): https://scalar.com/resources/changelog/sdk-generator
- Agent release notes (0.12.35, OpenAPI 3.2 `$self`): https://scalar.com/products/agent/release-notes
- Scalar SDK generator: https://scalar.com/products/sdk-generator
- Scalar MCP & Agent: https://scalar.com/products/agent
- Scalar API Client: https://scalar.com/products/api-client
- Scalar Registry: https://scalar.com/products/registry
- Full research reports: https://github.com/MattMsh/api-docs-tools-comparison
