# Prompt Forge Gemini Context

## Overview
This repository hosts the **Prompt Forge** extension, a specialized skill for the Gemini CLI and Claude Code. It focuses on extracting a developer's real intent from vague requests, grounding the task in codebase reality, and surfacing critical perspectives often missed due to fatigue.

## Directory Structure

*   **`skills/`**: Contains the `prompt-forge` skill definition.
    *   **`SKILL.md`**: The main documentation and instructions for the skill.
    *   **`references/`**: Supporting documentation, templates, and guides for task-specific grounding.
*   **`hooks/`**: Contains the `SessionStart` hook for automatic context injection.
*   **`gemini-extension.json`**: The manifest defining extension metadata.

## Core Capabilities
1.  **Intent Extraction:** Untangles rough, tired prompts into clear technical goals.
2.  **Codebase Grounding:** Uses actual file paths, function names, and patterns.
3.  **Perspective Rotation:** Applies nine analytical lenses (Security, QA, UX, etc.) to surface hidden requirements.
4.  **Plugin Optimization:** Tailors output for seamless handoff to GSD and Superpowers workflows.
