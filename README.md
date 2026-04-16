# Compos

Persistent architectural memory for your codebase — legible to humans, queryable by AI builders.

Compos tracks the **components**, **relationships**, **constraints**, **risks**, and **decisions** that make up your software system. Written by static analysis, updated by AI builders through an MCP server, reviewed by humans. The result: a map that stays in sync with your code, and gives AI tools the architectural context they need to make informed changes.

---

## Free tier (this repo's packages)

- **`compos-cli`** — local static analysis, `.compos/map.json`, CLI commands
- **`compos-mcp`** — MCP server for AI builders (Claude, Cursor, etc.)
- **Claude Code plugin** — bundles the MCP server + workflow skills (`orientation`, `architectural-logging`, `preflight-check`)

## Paid tier *(coming soon)*

- Team webapp — visual map dashboard, version history, collaboration
- `compos push` — sync local map to the team server

---

## Install

### Claude Code plugin (recommended)

```text
/install-plugin github:fer46/compos-plugin
```

This wires up the MCP server (`compos-mcp` via `uvx`, no pre-install) and three workflow skills into Claude Code. Prereq: [`uv`](https://docs.astral.sh/uv/).

### CLI (optional, for local analysis)

```bash
uv tool install compos-cli
# or: pipx install compos-cli
compos --version
```

### MCP server for other clients

```bash
uv tool install compos-mcp
compos-mcp  # stdio transport
```

Wire into your MCP client's config (Cursor, Zed, raw MCP) per their docs.

---

## Quick start

```bash
cd my-project
compos init             # creates .compos/map.json
compos analyze          # populates from static analysis
compos --help
```

Open Claude Code in the project. The plugin auto-discovers `.compos/` and the skills activate on relevant actions.

---

## Concepts

The map (`.compos/map.json`) is a JSON document with five object types:

| Type | Examples |
|------|----------|
| **Component** | services, libraries, databases, frontends |
| **Relationship** | imports, HTTP calls, DB queries, event publishes |
| **Constraint** | invariants the system must preserve |
| **Risk** | known fragilities |
| **Decision** | ADR-style records tied to components |

Each field carries **provenance** (static-analysis / ai-annotated / human-input) and **confidence**. The merge engine enforces a trust hierarchy: human input overrides AI annotation, which overrides static analysis. Deletions are always soft.

---

## Issues

Bugs and feature requests: [open an issue](https://github.com/fer46/compos/issues).

---

## License

MIT. See [LICENSE](LICENSE).
