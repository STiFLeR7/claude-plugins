# memex-mcp — Claude Code plugin

> Trusted engineering context for AI coding agents.

This plugin registers the [memex](https://github.com/STiFLeR7/memex) MCP server with Claude Code: 14 tools for explicit retrieval and governed writes against a temporal knowledge graph of your repository.

memex v1.0.0 adds **live context**: hooks that keep Claude Code and Codex sessions current as the code changes. See [Live context (v1)](#live-context-v1).

## What it gives you

| Read tools | When |
|---|---|
| `get_project_context` | At session start — get the lay of the land |
| `get_symbol_context` | Before editing a function or class |
| `get_recent_decisions` | To see what's changed architecturally |
| `get_open_problems` | To find active bugs and tech debt |
| `search_context` | Hybrid search across the whole graph |
| `get_engineering_context` | Retrieve bounded, provenance-aware task context |
| `get_stale_context` | Spot outdated documentation |
| `get_context_briefing` | Compact scoped briefing for a module or the whole repo |

| Analysis tools | When |
|---|---|
| `explain_change` | After a commit — *why* did this happen? |
| `predict_impact` | Before a refactor — *what* might break? |

| Write tools | When |
|---|---|
| `record_decision` | After making a technical choice |
| `record_problem` | When you discover a bug or piece of debt |
| `resolve_problem` | When a tracked problem is fixed |
| `invalidate_edge` | When a fact is no longer true |

## Prerequisites

The plugin only wires up the MCP server config. Memex itself runs locally and needs:

- **Docker** — for the Neo4j knowledge graph
- **Node.js 18+** — to run `npx stifler-memex-mcp`
- **A configured LLM/embedding backend** for ingestion and synthesis; Gemini is
  supported, but is not the only supported backend

## First-time setup (after installing the plugin)

```bash
# 1. Start Neo4j
docker run -d --name memex-neo4j \
  -p 7474:7474 -p 7687:7687 \
  -e NEO4J_AUTH=neo4j/memex-local \
  neo4j:5

# 2. Set environment variables (in your shell or .env in the repo root)
export NEO4J_URI=bolt://localhost:7687
export NEO4J_USER=neo4j
export NEO4J_PASSWORD=memex-local
# Use Gemini, or configure another supported backend through memex's env vars.
export GEMINI_API_KEY=your-key-here

# 3. Initialize and start the watcher in your project
npx stifler-memex-mcp init --repo .
npx stifler-memex-mcp watch --repo .
```

Your next Claude Code session will see memex's tools in the MCP picker. The MCP
path is explicit: Claude invokes context and write operations when needed.
This plugin does not replace Claude's own session memory or persist raw
prompts, transcripts, tool results, or host state.

## Live context (v1)

v1 hooks into the host client so context stays current without the agent asking:

- **Session start:** a bounded working set, with delivery confirmed from the client's own session record.
- **Before each edit:** memex checks whether the context the edit rests on still holds. If not, the edit is held, the agent gets a scoped correction, and it revises.
- **On resume:** if the code changed while the session was away, memex names the files to re-read.
- **Safe to try:** `memex v1 mode shadow` records what would be corrected without changing anything, hooks fail open, and `memex v1 rollback` stops memex at once.

```bash
uv tool install memex-mcp            # installs the `memex` command
cd your-repo
memex v1 doctor                      # what is set up, what is missing
memex v1 install claude              # hooks in .claude/settings.json; global settings untouched
memex v1 install codex --neo4j-uri bolt://localhost:7687   # optional, for Codex
```

Full guide: <https://github.com/STiFLeR7/memex/blob/master/docs/v1/25_ONBOARDING.md>

## Highlights

- **Bitemporal knowledge graph** — every fact has a creation time and an optional invalidation time
- **Confidence and freshness** — validation, corroboration, expiry, and supersession remain visible
- **Bounded context** — `ContextPacket` projections carry scope, provenance, freshness, and selection reasons
- **Hermes-compatible core** — the same context-selection contract can support Hermes automatic read-only prefetch; this Claude plugin uses MCP
- **Fail-open integration** — memex augments the host agent and does not own its session state
- **Human-in-the-loop validation** — `npx stifler-memex-mcp review` opens a TUI for lowest-confidence-first review
- **Hierarchical clusters** — optional summaries compress repository context; budgets remain configurable
- **Write governance** — per-node-type ACL, intent-confirmation on agent writes, explicit corroborates/supersedes semantics
- **Multi-repo aware** — single watcher and MCP server manages hundreds of repos with zero-config switching
- **Per-agent attribution** — every write records which harness (Claude Code, Gemini CLI, …) produced it
- **Team-ready** — RBAC (viewer/contributor/admin), a shared project graph across developers, a browser dashboard for activity/confidence/conflicts, and a self-hosted Docker Compose deployment for shared teams
- **Pluggable dashboard auth** — session login by default, with an `AuthProvider` architecture ready for OIDC/SSO
- **Governance report delivery** — optional weekly Slack and email delivery of the write-governance report, alongside the existing local file

Benchmark evidence and limitations: <https://github.com/STiFLeR7/memex/blob/master/BENCHMARK.md>

Full docs: <https://github.com/STiFLeR7/memex>
