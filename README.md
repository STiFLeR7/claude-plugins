# STiFLeR's Claude Code Plugins

[![GitHub stars](https://img.shields.io/github/stars/STiFLeR7/claude-plugins?style=flat)](https://github.com/STiFLeR7/claude-plugins/stargazers)
[![memex-mcp on npm](https://img.shields.io/npm/dm/stifler-memex-mcp?label=memex-mcp%20installs)](https://www.npmjs.com/package/stifler-memex-mcp)
[![memex-mcp on PyPI](https://img.shields.io/pypi/dm/memex-mcp?label=memex-mcp%20pypi)](https://pypistats.org/packages/memex-mcp)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

A small, opinionated marketplace of Claude Code plugins focused on durable engineering context and grounded agent workflows.

```
/plugin marketplace add STiFLeR7/claude-plugins
/plugin install memex-mcp@stifler-marketplace
/plugin install prompt-forge@stifler-marketplace
```

## Plugins

### 🧠 [memex-mcp](./memex-mcp)

Trusted engineering context for AI coding agents. Builds a temporal knowledge graph of your repository and exposes bounded, provenance-aware context through 14 MCP tools — `get_project_context`, `record_decision`, `predict_impact`, `explain_change`, and more.

Claude Code can explicitly recover your architecture, decisions, open problems, and code relationships without treating the plugin as a replacement for Git or Claude's own session memory.

- Bitemporal facts with expiry and supersession
- Confidence decay, validation, corroboration, and stale-context review
- Bounded `ContextPacket` projections with provenance and selection reasons
- Human-in-the-loop validation via `memex review`
- Explicit, governed writes for decisions, problems, resolutions, and invalidation

Backed by Neo4j + Graphiti; optional LLM backends support synthesis and explanation. MIT licensed. → [github.com/STiFLeR7/memex](https://github.com/STiFLeR7/memex)

### ✍️ [prompt-forge](./prompt-forge)

Advanced prompt refinement skill. Extracts your *real* intent, investigates your codebase and ecosystem, applies 9 perspective lenses (Security, QA, UX, Performance, …), and produces a grounded prompt for your execution tool — without ever executing the task itself.

Trigger phrases: *"help me prompt"*, *"improve my prompt"*, *"how to write a prompt for…"*. The skill investigates, asks sharp clarifying questions, then hands you a refined prompt to paste into your next agent.

MIT licensed. → [github.com/STiFLeR7/prompt-forge](https://github.com/STiFLeR7/prompt-forge)

## Local development

```bash
# Clone and link as a local marketplace for testing
git clone https://github.com/STiFLeR7/claude-plugins
/plugin marketplace add /absolute/path/to/claude-plugins
```

## Contributing

Plugins added to this marketplace should be:
- Single-purpose and well-tested
- Documented with clear trigger conditions
- MIT (or compatible) licensed
- Maintained by an active author

Open an issue with a proposal before submitting a PR.

## License

MIT — see individual plugin directories for their respective licenses.
