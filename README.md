# STiFLeR's Claude Code Plugins

A small, opinionated marketplace of Claude Code plugins focused on making agents *remember* and *understand intent*.

```
/plugin marketplace add STiFLeR7/claude-plugins
/plugin install memex-mcp@stifler-marketplace
/plugin install prompt-forge@stifler-marketplace
```

## Plugins

### 🧠 [memex-mcp](./memex-mcp)

Persistent memory for AI coding agents. Builds a temporal knowledge graph of your codebase and serves it through 14 MCP tools — `get_project_context`, `record_decision`, `predict_impact`, `explain_change`, and more.

Every Claude session starts knowing your architecture, your decisions, and your open problems. No more cold starts. No more context pasting.

- Bitemporal facts (every edge knows when it was true)
- Two-regime confidence decay (unvalidated facts cross stale at exactly 30 days)
- Hierarchical clusters (briefing stays under 1500 tokens regardless of repo size)
- Human-in-the-loop validation via `memex review`
- Anthropic memory-tool backend included

Backed by Neo4j + Graphiti + Gemini Flash. MIT licensed. → [github.com/STiFLeR7/memex](https://github.com/STiFLeR7/memex)

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
