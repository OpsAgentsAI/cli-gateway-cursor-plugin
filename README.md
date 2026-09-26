# CLI Gateway — Cursor Plugin

Minimal public interface shell for **CLI Gateway**: an authed cloud CLI execution gateway that
lets an agent run `gcloud`, `gh`, `trello`, and dozens of other CLIs through one hosted MCP
server — no local CLI installs, no ambient credentials on the agent's machine, and a
per-tenant audit trail.

This repository is **discovery-only**. Billing, tiers, and account management stay on:
- Product page: https://opsagents.agency/products/cli-gateway
- Self-serve signup / billing portal: https://cli-gateway-portal.web.app
- Google Cloud Marketplace listing (already approved — see the product page for the link)

Nothing in this repo touches the gateway runtime, credentials, Cloud Run, or the audit
backend. Those stay private.

## ⚠️ Status: pre-launch scaffold

The `mcp.json` in this repo points at a **placeholder** URL
(`https://mcp.cli-gateway.invalid/mcp` — the reserved, non-resolving `.invalid` TLD, so it
fails loudly instead of silently connecting to nothing). CLI Gateway does not yet expose a
public, multi-tenant, hosted MCP-over-HTTP endpoint; today it runs as a private gateway
(Cloud Run, both regions) reached via a per-tenant bearer token over a local stdio bridge.
**Do not submit this plugin to the Cursor Marketplace until that endpoint is live** and this
file has been updated to point at it. Track the endpoint's shipment on the `board-cli-gateway`
Trello board (see the Marketplace delivery plan, card `eBF94b9a`).

## Install (once the endpoint above is live)

1. Add this repository as a plugin source in Cursor, or install directly from the Cursor
   Marketplace listing once published.
2. Sign up at the [billing portal](https://cli-gateway-portal.web.app) to get your own
   CLI Gateway instance and credentials (BYO-credential model — CLI Gateway never sees your
   underlying cloud/service credentials in plaintext; see the portal's privacy policy for the
   envelope-encryption details).
3. Cursor will prompt you to authenticate against the hosted MCP endpoint the first time you
   use a `cli-gateway` tool.

## What you get

Once connected, the agent gets a set of `*_exec` tools (one per CLI — `gcloud_exec`,
`gh_exec`, `trello_exec`, and so on), each a thin, authenticated wrapper over the real CLI
running server-side. See `skills/cli-gateway-usage/SKILL.md` in this repo for guidance on
when to reach for a CLI Gateway tool versus a local one.

## Support / links

- Product: https://opsagents.agency/products/cli-gateway
- Support: michal@opsagents.agency
