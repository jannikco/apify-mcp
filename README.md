# Apify MCP server

Review account identity and existing Actors before deciding which existing automation to inspect.

A direct-provider MCP server with useful local execution. No PipMCP account is required for local use. Provider API access and any provider charges are your responsibility.

## Quick start

Requires Node.js22+. Clone this repository, then run:

```sh
npm ci --ignore-scripts
npm test
npm start
```

The default command inspects the tools offline. Configure your own credentials in your environment:

- `APIFY_TOKEN`



Credential help: https://docs.apify.com/api/openapi.json

## Execute a real read

Replace example record IDs with records you are authorized to access.

```sh
npm start -- --call get_current_user '{}'
```

## Use with an MCP client

Launch `node /absolute/path/apify-mcp/server.mjs` using stdio transport; pass credentials through the client environment. Stdout is reserved for JSON-RPC.

## Tools

| Tool | Effect | Purpose |
| --- | --- | --- |
| get_current_user | Read | Read your Apify account identity. |
| list_actors | Read | List Actors owned by your account; does not run them or incur Actor execution charges. |

## Concrete workflow

Review account identity and existing Actors before deciding which existing automation to inspect.

1. get_current_user
2. list_actors

## Optional writes

Writes are disabled by default. Set CONNECTOR_ALLOW_WRITES=true and supply `_approval: {approved:true,idempotencyKey:"unique-request-id"}` on the specific call. Do not reuse a key for a different request. Uncertain outcomes are never automatically replayed; inspect the provider before another attempt.

## Capability evidence

Local: **Tested — HTTP fixtures and real stdio tools/call**. Managed: **Documented**. Provider authentication and live operations have not been established by these fixture tests. Evidence applies per operation and execution mode; setup discovery does not imply provider execution.

## Managed production

[Activate with PipMCP](https://pipmcp.com/github/start?app=apify&integration=apify-mcp&utm_source=github&utm_campaign=github-apify-mcp&utm_content=readme) when you want the hosted service.  Local credentials are not uploaded by this code. Review provider permissions in the managed onboarding. [Directory and related projects](https://jannikco.github.io/pipmcp-connectors/integrations/apify/).

## Provenance and maintenance

- https://docs.apify.com/api/openapi.json

Maintainer:jannikco. MIT license for this code. See connector.json for selected operations and integration.json for evidence. Runtime dependencies retain their own licenses. Report sensitive issues through https://pipmcp.com/contact; do not post credentials or customer data in public issues.
