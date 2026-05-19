# Prompt Forge Plugin Standards

## Overview
This is a standalone plugin for Claude Code and Gemini CLI that provides the **Prompt Forge** skill.

## Plugin Structure
- `.claude-plugin/`: Claude-specific metadata.
- `skills/`: Core skills (flat namespace).
  - `prompt-forge/`: Main skill and references.
- `hooks/`: Lifecycle hooks for context injection.
- `gemini-extension.json`: Gemini CLI manifest.

## Operating Principles
1. **Zero External Dependencies:** No NPM packages required for core functionality.
2. **Grounding First:** All prompts must be grounded in codebase reality before delivery.
3. **No Implementation:** Prompt Forge writes prompts, not code.
4. **Tool Mapping:** Skills use Claude Code tool names; hooks handle mapping to other platforms.

## Development
- When adding to `references/`, update the main `SKILL.md` to link to it.
- Keep `SKILL.md` focused on triggering and core workflow.
- Use `references/` for detailed blueprints and guides.
