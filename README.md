# n8n MCP Skills Starter

A lightweight starter repository to get up and running quickly with MCP-driven n8n skills.

This is a documentation-first knowledge base that provides AI agents with curated skills for building n8n workflows via MCP tools. It is especially well suited for Cloud Code (Claude) and OpenCode environments.

Why this repo

- Fast, minimal setup for MCP + n8n workflow automation
- 7 core skills provided and mirrored for both agent platforms
- Ready MCP configuration (`opencode.json`, `.mcp.json`) to point at your n8n instance

What’s included

- `opencode.json` — OpenCode MCP plugin configuration
- `.mcp.json` — MCP server configuration (Cloud Code / Claude)
- `.claude/skills/` — skills for Cloud Code
- `.opencode/skills/` — mirrored skills for OpenCode

Quick start

1. Run or point to an n8n instance and set `N8N_API_URL` / `N8N_API_KEY` in `opencode.json` and `.mcp.json`.
2. Launch your agent (Cloud Code / OpenCode) and enable the `n8n-mcp` server.
3. Use the bundled skills to search nodes, validate node configs, and create workflows via MCP tools.

Best fit

- Designed for Cloud Code (Claude) and OpenCode usage — small footprint, documentation-driven, no build system.
- Ideal when you want AI-guided workflow construction, node discovery, and validation without extra tooling.

Credits

- n8n MCP: https://github.com/czlonkowski/n8n-mcp
- n8n skills: https://github.com/czlonkowski/n8n-skills
