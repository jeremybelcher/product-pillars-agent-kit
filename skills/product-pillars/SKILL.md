---
name: product-pillars
description: Create and edit flowcharts, user flows, process maps and decision trees on a shared Product Pillars canvas the user can open, edit by hand and share. Use when the user asks for a flowchart or user flow they want to see visually, edit, share with someone, or keep in sync with code, or when a Mermaid flowchart in the repo should become an editable diagram.
---

# Product Pillars

Product Pillars is a canvas for flowcharts that people and agents edit together. You draw with MCP tools; the person sees the diagram on a canvas, rearranges or relabels it, and you read their changes back. Every diagram exports as Mermaid Markdown.

Use it when someone will look at, edit, or share the diagram. If nobody will ever open it visually, a Mermaid block in a file is enough. It draws flowcharts only; for sequence, class, ER or Gantt diagrams, write Mermaid directly.

## Connect

Check whether the Product Pillars tools are available (`list_diagrams`, `create_diagram`, `edit_diagram`, `get_diagram`, `lint_diagram`, `render_diagram`). If they are, skip this section.

If not, the person needs to connect once. Tell them exactly what to do:

- **Claude Code:** run `claude mcp add --transport http product-pillars https://www.productpillars.com/api/mcp`, then `/mcp`, pick `product-pillars`, choose Authenticate, and sign in in the browser.
- **Claude (web, desktop, mobile):** Settings, Connectors, Add custom connector, paste `https://www.productpillars.com/api/mcp`.
- **Any other client:** setup for Cursor, VS Code, Codex, Gemini CLI and others is at https://www.productpillars.com/agents.
- **No MCP (scripts, CI):** the HTTP API takes an API key from https://www.productpillars.com/settings. See the guide below.

Signing in creates a free account if they don't have one.

## Draw

1. **Already have Mermaid?** Pass it to `create_diagram` as `mermaid` (a flowchart, or Markdown containing one). It is laid out for you, and shapes become node types: `{text}` decision, `([text])` start or end, `[[text]]` system step, `[text]` user step; subgraphs become frames.
2. **Otherwise** plan the steps (start and end, user actions, system actions, decisions with labeled Yes/No branches), call `create_diagram`, then add every node and edge in **one** `edit_diagram` batch ending with `{"op": "auto_layout"}`.
3. Run `lint_diagram` and fix errors and warnings, then look at it with `render_diagram`.
4. **Give the person the link:** `https://www.productpillars.com/editor/{id}`. Tell them in a sentence what you drew and what you weren't sure about.

## Work alongside the person

- They may be editing the same diagram while you work. Read it first (`get_diagram`, format `compact` for big ones) and pass the `version` you read as `expected_version` on every `edit_diagram`. If it changed, nothing is saved and you get what changed: re-read, adjust, retry.
- Don't undo their edits. If you disagree with a change, say so instead of reverting it.
- To review a diagram, report problems and proposed fixes first, and change it only once they agree.

## Reference

The full guide (layout numbers, handles, frames, every tool's schema): https://www.productpillars.com/llms.txt
