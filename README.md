# 🚀 n8n MCP Skills Starter

> **AI-Powered Workflow Automation** — Supercharge Claude Code with intelligent n8n workflow building capabilities

Transform how you build n8n workflows by letting AI do the heavy lifting. This repository provides a curated knowledge base that gives AI agents deep expertise in n8n workflow automation through MCP (Model Context Protocol) tools.

---

## ✨ What is this?

Imagine having an n8n expert sitting beside you that can:

- 🔍 **Find the perfect node** from 2,000+ options in seconds
- ✅ **Validate configurations** before you deploy
- 🏗️ **Build workflows** using proven architectural patterns
- 🐛 **Debug expressions** and code nodes instantly
- 📦 **Deploy templates** from a library of 2,700+ workflows

This repository makes that possible. It's not code—it's **knowledge**, carefully organized as skills that AI agents can use to help you build better n8n workflows, faster.

---

## 🎯 What You Can Do

| Capability                      | How It Works                                                                                         |
| ------------------------------- | ---------------------------------------------------------------------------------------------------- |
| **🔎 Node Discovery**           | Ask: "Find nodes for Slack integration" → AI searches 2,000+ nodes and returns matches with examples |
| **🛠️ Workflow Creation**        | Describe: "Create a workflow that monitors RSS and posts to Discord" → AI builds it step-by-step     |
| **✅ Configuration Validation** | Paste any node config → AI validates required fields, expressions, and connections                   |
| **📚 Pattern Library**          | Ask: "How do I handle webhooks safely?" → AI shows proven patterns from production workflows         |
| **💻 Code Assistance**          | Get help with JavaScript/Python in Code nodes, including n8n-specific APIs                           |
| **🔧 Expression Help**          | Debug `{{ $json.foo }}` expressions with instant error detection                                     |

---

## 📦 What's Inside

### 7 Core Skills (~22,000 lines of documentation)

```
.agents/skills/
├── n8n-code-javascript/      # JavaScript in Code nodes
├── n8n-code-python/          # Python in Code nodes
├── n8n-expression-syntax/    # n8n {{ }} expression language
├── n8n-mcp-tools-expert/     # MCP tool usage guide
├── n8n-node-configuration/   # Node configuration patterns
├── n8n-validation-expert/    # Workflow validation
└── n8n-workflow-patterns/    # Architectural patterns
```

Each skill includes:

- **Quick Start** — Get going immediately
- **Real Examples** — Copy-paste patterns from production workflows
- **Common Errors** — Avoid pitfalls others have hit
- **Best Practices** — Industry-tested approaches
- **Integration Guide** — How skills work together

### Repository Structure

- `.agents/skills/` — Source skill directories
- `.claude/skills/` — Symlinks to `.agents/skills/` for Claude Code
- `.mcp.json.example` — Example MCP configuration for Claude Code
- `opencode.json.example` — Example MCP configuration for OpenCode
- `skills-lock.json` — Skill version tracking from upstream sources

### Ready-to-Use MCP Configuration

The repository includes example configuration files:

- `.mcp.json.example` — For Claude Code
- `opencode.json.example` — For OpenCode

Copy these files and update your n8n API credentials to get started.

---

## 🚀 Quick Start (3 Steps)

### 1️⃣ Get Your n8n API Credentials

```bash
# If you have n8n running locally:
# Your API URL: http://localhost:5678

# Generate an API key in n8n:
# Settings → API → Create API Key
```

### 2️⃣ Configure the MCP Server

```bash
# Copy the example configuration
cp .mcp.json.example .mcp.json

# Edit .mcp.json and update your API credentials
```

```json
{
  "mcpServers": {
    "n8n-mcp": {
      "command": "npx",
      "args": ["n8n-mcp"],
      "env": {
        "N8N_API_URL": "http://localhost:5678",
        "N8N_API_KEY": "your-api-key-here"
      }
    }
  }
}
```

### 3️⃣ Enable in Claude Code

```bash
# Restart Claude Code
# The MCP server will be auto-detected from .mcp.json
```

---

## 🎮 Usage Examples

### Example 1: Finding the Right Node

```
You: "I need to send messages to Microsoft Teams"

AI: Uses search_nodes MCP tool → finds 'n8n-nodes-base.microsoftTeams'
   → shows configuration example → explains required fields
```

### Example 2: Building a Workflow

```
You: "Create a workflow that triggers on webhooks, validates data, and saves to PostgreSQL"

AI: Uses n8n-workflow-patterns skill → designs architecture
   → uses n8n-mcp-tools-expert → creates nodes via MCP
   → uses n8n-validation-expert → validates the workflow
```

### Example 3: Debugging Expressions

```
You: "Why isn't {{ $node.Webhook.json.email }} working?"

AI: Uses n8n-expression-syntax skill → checks syntax
   → identifies missing reference → shows correct pattern
```

---

## 🏗️ Architecture

### Documentation-First Design

This is **not** a traditional code repository:

- ❌ No build system
- ❌ No dependencies to install
- ❌ No tests to run
- ✅ Pure knowledge, organized as AI-consumable skills

### Skill Management

Skills are centrally managed in `.agents/skills/` and symlinked to `.claude/skills/`:

- Skills are tracked via `skills-lock.json`
- Source: [czlonkowski/n8n-skills](https://github.com/czlonkowski/n8n-skills)
- Claude Code automatically discovers skills from `.claude/skills/`

### Cross-Referenced Knowledge

Each skill links to others, creating an interconnected graph:

```
n8n-workflow-patterns
    → references n8n-node-configuration
    → references n8n-code-javascript
    → references n8n-validation-expert
```

---

## 🛠️ Available MCP Tools (40+)

The n8n-mcp server provides:

| Category                | Tools                                                                    |
| ----------------------- | ------------------------------------------------------------------------ |
| **Node Discovery**      | `search_nodes`, `get_node`, `validate_node`                              |
| **Workflow Management** | `n8n_create_workflow`, `n8n_update_partial_workflow`, `n8n_get_workflow` |
| **Template Library**    | `search_templates`, `n8n_deploy_template` (2,700+ templates)             |
| **Validation**          | `validate_workflow`, `n8n_validate_workflow`                             |
| **Execution**           | `n8n_test_workflow`, `n8n_executions`                                    |
| **Documentation**       | `tools_documentation`, `get_node` (docs mode)                            |

---

## 📊 Stats

- **7 Core Skills** — JavaScript, Python, Expressions, MCP Tools, Node Config, Validation, Workflow Patterns
- **36 Documentation Files** — ~22,000 lines of n8n expertise
- **40+ MCP Tools** — Full n8n API coverage
- **2,700+ Templates** — Deployable via MCP
- **2,000+ Nodes** — Searchable via AI

---

## 🎯 Who Is This For?

| Role                     | Benefit                                                    |
| ------------------------ | ---------------------------------------------------------- |
| **Automation Engineers** | Accelerate workflow development with AI assistance         |
| **Low-Code Developers**  | Get expert guidance without deep coding knowledge          |
| **DevOps Engineers**     | Build integration workflows with best practices baked in   |
| **API Integrators**      | Find the right nodes and validate configurations instantly |
| **n8n Beginners**        | Learn through AI-guided examples and patterns              |

---

## 🔧 Validation & Testing

```bash
# Verify skill structure
find .agents/skills -name "SKILL.md" | wc -l  # Should output: 7

# Validate JSON configuration
cat .mcp.json.example | jq .
cat opencode.json.example | jq .

# Count documentation
find .agents/skills -name "*.md" | wc -l  # Should output: 36
```

Skills are validated through:

- Claude Code skill activation
- Trigger keyword verification
- Cross-reference link validation
- Markdown syntax verification

---

## 🌟 Best Practices

### When to Use This Repository

✅ **Perfect for:**

- Building new workflows with AI guidance
- Exploring n8n's 2,000+ node ecosystem
- Validating configurations before deployment
- Learning n8n patterns and best practices
- Debugging workflow issues

❌ **Not designed for:**

- Traditional software development (no code to compile)
- Runtime n8n execution (use n8n directly)
- Workflow hosting (this is documentation only)

---

## 🙏 Credits & Inspiration

This repository stands on the shoulders of giants:

- **[n8n MCP Server](https://github.com/czlonkowski/n8n-mcp)** — The MCP implementation that makes this possible
- **[n8n Skills](https://github.com/czlonkowski/n8n-skills)** — Original skill architecture and documentation patterns
- **[n8n](https://n8n.io)** — The incredible workflow automation platform itself

---

## 📝 License

This repository contains documentation and configuration for integrating with n8n and MCP tools. Please refer to the original projects for their respective licenses.

---

**Made with ❤️ for the n8n and AI automation community**

_Ready to supercharge your workflow automation? Start with the [Quick Start](#-quick-start-3-steps) above!_
