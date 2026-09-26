---
name: cli-gateway-usage
description: Use when deciding whether to run a CLI command through the CLI Gateway MCP tools (e.g. gcloud_exec, gh_exec, trello_exec) versus a local CLI install. Applies whenever the agent needs authenticated cloud/API CLI access and either has no local credentials, is running headless/unattended, or wants every call captured in a shared audit trail.
---

# When to use CLI Gateway

CLI Gateway exposes one MCP tool per underlying CLI (`gcloud_exec`, `gh_exec`, `trello_exec`,
and others depending on what your account has enabled). Each tool runs the real CLI
server-side, authenticated with your own credentials, and returns stdout/stderr/exit code.

**Reach for a CLI Gateway tool when:**
- The session is headless or unattended (no interactive browser/CLI login available).
- The credentials involved should never touch the agent's local machine or disk.
- Multiple agents or sessions need to share one authenticated identity with a single audit
  trail, instead of each holding its own local login.
- You need a CLI that isn't installed locally and shouldn't be — the gateway already has it.

**Prefer a local CLI when:**
- You're doing exploratory, interactive work where round-tripping through a remote gateway
  adds latency for no safety benefit.
- The command reads/writes large local files that would be awkward to shuttle over MCP.
- You already have a working local login and there's no shared-audit or unattended-execution
  requirement.

**Never:**
- Paste a real secret, token, or credential value into a prompt, comment, or file when using
  a CLI Gateway tool — the gateway resolves credentials server-side; it should never need one
  handed to it in plaintext.
- Assume a green/exit-0 result alone proves a tool ran correctly for gateways with known
  launch-guard edge cases — check the actual output, not just the exit code, especially for
  MCP-entrypoint-adjacent changes.
