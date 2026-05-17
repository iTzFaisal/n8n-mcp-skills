# AGENTS.md

## Scope

- This repo exists to help agents interact with a live n8n instance by using the bundled skills together with the local MCP wiring in `opencode.json`.
- This is a documentation/skill repository, not an app repo: there is no root `package.json`, workspace file, CI workflow, test runner, linter, formatter, or build pipeline to run.
- Verify changes with file-level checks, not guessed `npm`/`pnpm` commands.

## Skill Layout

- The real content lives in two committed mirror trees: `.agents/skills/` and `.claude/skills/`.
- The README says `.claude/skills/` is symlinked from `.agents/skills/`, but the checked-in repo currently uses two normal directories. Keep them identical when editing skills.
- `skills-lock.json` is the source-of-truth index for the 7 shipped skills and their upstream hashes from `czlonkowski/n8n-skills`.
- Preserve the frontmatter in every `SKILL.md`; the `description` text is trigger text for agents, not just prose.

## Config Files

- Commit-worthy MCP templates are `.mcp.json.example` and `opencode.json.example`.
- `opencode.json` is the local OpenCode MCP config that points this repo at `n8n-mcp` over stdio; when working here, assume that file is how OpenCode sessions are expected to reach n8n.
- Local `.mcp.json` and `opencode.json` are developer-specific runtime config. In this repo they are untracked and can contain real `N8N_API_KEY` values; do not overwrite, commit, or quote their secrets unless explicitly asked.
- `.gitignore` only ignores `.DS_Store`; do not assume local config files are protected by ignore rules.

## Useful Checks

- Mirror check: `diff -qr .agents/skills .claude/skills`
- Skill count: `find .agents/skills -name "SKILL.md" | wc -l`  → should be `7`
- Markdown doc count: `find .agents/skills -name "*.md" | wc -l`  → should be `36`

## Existing Instructions

- `CLAUDE.md` in `HEAD` is only `@AGENTS.md`. If you touch `CLAUDE.md`, keep it as a pointer instead of duplicating instructions.
- For skill behavior changes, update the skill docs first; only update `README.md` when the repo-level overview also needs to change.
