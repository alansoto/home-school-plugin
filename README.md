# Home School plugin

What Ash's Claude installs: the **Home School connector** (our MCP server at `/mcp`) and a stub **skill** that
points Claude at the connector's guide. The house rules themselves live in the connector's tool descriptions
and its `get_guide` tool, so most changes need only a deploy.

This folder is laid out as a plugin marketplace (`.claude-plugin/marketplace.json` → `home-school/`). Claude
syncs plugins from a GitHub repo, and this app's repo is private, so the folder is published as its own
public repo (it holds no secrets: the connector signs each parent in itself). See the main README's
"Connecting Claude" for the steps.

## The pointer line for "Instructions for Claude"

Settings → General → Instructions for Claude, one line:

> For anything about the child's learning, the home-school records or the Knowledge Base, use the Home School connector and call its get_guide tool first.
