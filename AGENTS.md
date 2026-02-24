# AGENTS.md

Guidance for AI coding agents working in this repository.

## What This Repository Is

This is a **pure documentation/knowledge base** — not a traditional code project. There is no package.json at root, no TypeScript, no build pipeline, and no test runner. It is an **n8n MCP Integration Repository** that provides AI agents with structured skills for building n8n workflows through MCP tools.

---

## Validation Commands

There are no build or test commands. Use these to validate the repo's health:

```bash
# Validate JSON configuration files
cat opencode.json | jq .
cat .mcp.json | jq .

# Verify both skill locations have all 7 skills
find .claude/skills -name "SKILL.md" | wc -l      # must be 7
find .opencode/skills -name "SKILL.md" | wc -l    # must be 7

# Verify YAML frontmatter exists in every SKILL.md
head -5 .claude/skills/*/SKILL.md | grep "^name:"

# Count total markdown files (baseline: 72)
find . -name "*.md" | grep -v node_modules | wc -l

# Verify cross-references resolve (no broken relative links)
grep -r "\[.*\](.*\.md)" .claude/skills/ --include="*.md" -l
```

---

## File Structure

```
/
├── CLAUDE.md               # Primary project guide (read this first)
├── AGENTS.md               # This file
├── opencode.json           # OpenCode MCP plugin config
├── .mcp.json               # Claude Code MCP server config
├── .gitignore
├── .claude/
│   ├── settings.local.json # Bash/tool permissions
│   └── skills/             # 7 skills for Claude Code
│       ├── n8n-code-javascript/
│       ├── n8n-code-python/
│       ├── n8n-expression-syntax/
│       ├── n8n-mcp-tools-expert/
│       ├── n8n-node-configuration/
│       ├── n8n-validation-expert/
│       └── n8n-workflow-patterns/
└── .opencode/
    ├── package.json        # @opencode-ai/plugin dependency
    └── skills/             # Mirror of .claude/skills/ (keep in sync)
```

Each skill directory contains:

- `SKILL.md` — Primary content (400–1100 lines), loaded by agents at runtime
- `README.md` — Metadata and overview
- Supporting files: `ERROR_PATTERNS.md`, `COMMON_PATTERNS.md`, `DATA_ACCESS.md`, etc.

---

## The 7 Core Skills

| Skill                    | Trigger Topics                                                   |
| ------------------------ | ---------------------------------------------------------------- |
| `n8n-code-javascript`    | JS Code nodes, `$input`, `$json`, `$node`, `$helpers`            |
| `n8n-code-python`        | Python Code nodes, `_input`, `_json`                             |
| `n8n-expression-syntax`  | `{{}}` expressions, `$json`, `$node`, expression errors          |
| `n8n-mcp-tools-expert`   | MCP tool selection, search_nodes, validate_workflow              |
| `n8n-node-configuration` | Node config, required fields, operation/resource params          |
| `n8n-validation-expert`  | Validation errors, warnings, false positives                     |
| `n8n-workflow-patterns`  | Workflow architecture, webhooks, HTTP API, AI agents, scheduling |

---

## Markdown Style Guidelines

### Frontmatter (required in every SKILL.md)

```yaml
---
name: n8n-domain-subdomain
description: One-line description. Use when [triggers]. Provides [value].
---
```

### Section Hierarchy

```
## Main Section
### Subsection
#### Sub-subsection
```

### Code Blocks

Always specify the language:

````markdown
````javascript
```json
```bash
```python
```yaml
````
````

### Error Pattern Format

Use the ❌/✅ format for wrong/correct examples:

````markdown
❌ WRONG — explanation of why this fails

```javascript
// bad code
```
````

✅ CORRECT — explanation of why this works

```javascript
// good code
```

````

### Links

- Internal (within same skill): `[ERROR_PATTERNS.md](ERROR_PATTERNS.md)`
- Cross-skill: `[n8n-code-javascript](../n8n-code-javascript/SKILL.md)`
- External: `[n8n Docs](https://docs.n8n.io/)`

### Separators

Use `---` between major sections to aid readability.

---

## Naming Conventions

| Type | Convention | Example |
|---|---|---|
| Skill directories | `n8n-domain-subdomain` (kebab-case) | `n8n-code-javascript` |
| Primary files | UPPERCASE | `SKILL.md`, `README.md`, `ERROR_PATTERNS.md` |
| Supporting files | lowercase with underscores | `webhook_processing.md`, `common_patterns.md` |
| JSON keys | camelCase | `nodeType`, `workflowId` |
| JS variables (in examples) | camelCase | `inputData`, `workflowItems` |
| Python variables (in examples) | snake_case | `input_data`, `workflow_items` |

---

## Dual-Location Sync Rule

**Critical**: Skills must exist in BOTH locations and remain identical:

- `.claude/skills/<skill-name>/` — read by Claude Code
- `.opencode/skills/<skill-name>/` — read by OpenCode

When adding or modifying any skill file, always update both locations. Verify with:

```bash
diff -r .claude/skills/ .opencode/skills/
````

---

## Critical n8n nodeType Format

Two incompatible prefixes are used depending on the MCP tool:

| Context                                             | Format       | Example                |
| --------------------------------------------------- | ------------ | ---------------------- |
| `search_nodes`, `get_node`, `validate_node`         | Short prefix | `nodes-base.slack`     |
| `n8n_create_workflow`, `n8n_update_*` (nodes array) | Full prefix  | `n8n-nodes-base.slack` |

This is the single most common source of errors when creating workflows. Always use the correct prefix for the tool being called.

---

## MCP Workflow: Standard Sequences

### Discover and Configure a Node

```
1. search_nodes({query: "keyword"})
2. get_node({nodeType: "nodes-base.<name>", detail: "standard"})
3. validate_node({nodeType: "nodes-base.<name>", config: {...}})
```

### Create and Deploy a Workflow

```
1. n8n_create_workflow({name, nodes, connections})
2. validate_workflow({workflow: {...}})          # or n8n_validate_workflow({id})
3. n8n_update_partial_workflow({id, operations: [...]})
4. n8n_update_partial_workflow({id, operations: [{type: "activateWorkflow"}]})
```

### Find and Deploy a Template

```
1. search_templates({searchMode: "by_task", task: "webhook_processing"})
2. n8n_get_template({templateId: <id>})
3. n8n_deploy_template({templateId: <id>})
```

---

## Skill Structure Pattern

All SKILL.md files follow this progressive disclosure structure:

1. **Quick Start** — Immediate, copy-paste-ready examples
2. **Core Concepts** — Detailed explanations and syntax
3. **Common Patterns** — Real-world scenarios with full code
4. **Error Patterns** — ❌ wrong vs ✅ correct comparisons
5. **Best Practices** — Production-grade guidance
6. **Integration with Other Skills** — Cross-references

When writing or editing skills, maintain this order. Include concrete statistics where available (e.g., "responsible for 38% of validation failures").

---

## What NOT to Do

- Do not create a `package.json` at the repository root
- Do not add build tooling, linters, or test runners
- Do not modify `.mcp.json` or `opencode.json` MCP server credentials
- Do not create skill files only in one location — always sync both `.claude/skills/` and `.opencode/skills/`
- Do not use vague section headers; be specific (e.g., "HTTP Request Authentication" not "Auth")
- Do not leave SKILL.md files without valid YAML frontmatter
