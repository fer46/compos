# Compos

Persistent architectural memory for your codebase — legible to humans, queryable by AI builders.

Compos tracks the **components**, **relationships**, **constraints**, **risks**, and **decisions** that make up your software system. Written by static analysis, updated by AI builders through an MCP server, reviewed by humans. The result: a map that stays in sync with your code, and gives AI tools the architectural context they need to make informed changes.

> **Status:** Alpha. Free tier live on PyPI + Claude Code plugin marketplace. Actively looking for early testers — if you run it on a real codebase, we want to hear what's missing. See [Feedback](#feedback).

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

In Claude Code, add the marketplace and install the plugin:

```text
/plugin marketplace add fer46/compos-plugin
/plugin install compos@compos-plugin
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

## Feedback

Compos is in alpha. Two things would help enormously:

1. **Try it on a real codebase** — install the plugin, run `compos analyze`, open Claude Code and exercise the MCP tools. Five minutes is enough to form an opinion.
2. **Tell us what broke, what was missing, or what was confusing.** No feedback is too small.

**Channels, in order of preference:**

- **[Early-tester feedback form](https://github.com/fer46/compos/issues/new?template=feedback.yml)** — short structured form, 2 minutes to fill.
- **[Bug report](https://github.com/fer46/compos/issues/new?template=bug.yml)** — for reproducible failures.
- **[General issue](https://github.com/fer46/compos/issues/new)** — anything else.

If you're on LinkedIn or email and prefer to reply there, that also works — everything gets read.

---

## License

MIT. See [LICENSE](LICENSE).
