# memex-mcp — Claude Code plugin

> Persistent memory for AI coding agents. Inspired by Vannevar Bush's 1945 concept of a machine that remembers everything.

This plugin registers the [memex](https://github.com/STiFLeR7/memex) MCP server with Claude Code. Once installed, every Claude session has 14 tools for reading and writing to a temporal knowledge graph of your codebase.

## What it gives you

| Read tools | When |
|---|---|
| `get_project_context` | At session start — get the lay of the land |
| `get_symbol_context` | Before editing a function or class |
| `get_recent_decisions` | To see what's changed architecturally |
| `get_open_problems` | To find active bugs and tech debt |
| `search_context` | Hybrid search across the whole graph |
| `get_stale_context` | Spot outdated documentation |
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
- **Gemini API key** — for commit-decision synthesis

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
export GEMINI_API_KEY=your-key-here

# 3. Initialize and start the watcher in your project
npx stifler-memex-mcp init --repo .
npx stifler-memex-mcp watch --repo .
```

Your next Claude Code session will see memex's tools in the MCP picker.

## Highlights (v0.3.2)

- **Bitemporal knowledge graph** — every fact has a creation time and an optional invalidation time
- **Two-regime confidence decay** — unvalidated facts cross the staleness threshold at exactly 30 days
- **Human-in-the-loop validation** — `npx stifler-memex-mcp review` opens a TUI for lowest-confidence-first review
- **Hierarchical clusters** — `get_project_context()` stays under 1500 tokens no matter how big the repo
- **Write governance** — per-node-type ACL, intent-confirmation on agent writes, explicit corroborates/supersedes semantics
- **Multi-repo aware** — single watcher and MCP server manages hundreds of repos with zero-config switching

Full docs: <https://github.com/STiFLeR7/memex>
