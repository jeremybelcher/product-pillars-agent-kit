# Product Pillars for agents

[Product Pillars](https://www.productpillars.com) is a canvas for flowcharts that people and AI agents edit together. Your agent draws a user flow, process map or decision tree; you open it on the canvas, move things around, and the agent reads your changes back. Every diagram exports as Mermaid Markdown, so it can live in your repo.

This repo connects agents to it:

- **An Agent Skill** (`skills/product-pillars`) that tells coding agents when a flowchart belongs on the canvas and how to draw one well. Works in Claude Code, Codex, Cursor, Gemini CLI and other agents that read skills.
- **A Claude Code plugin** that bundles the skill with the hosted MCP server.
- **`server.json`**, the listing for the official MCP Registry.

The MCP server itself is hosted at `https://www.productpillars.com/api/mcp`. Nothing here runs locally.

## When to use it

Use Product Pillars when someone wants a flowchart they will look at, edit by hand, or share: user flows, onboarding and checkout flows, process maps, approval flows, decision trees. If nobody will ever open the diagram visually, a Mermaid block in a file is enough. It draws flowcharts only.

## Install

### The skill (any agent)

```bash
npx skills add jeremybelcher/product-pillars-agent-kit
```

The skill tells the agent how to connect if the MCP server isn't set up yet.

### The Claude Code plugin (skill plus MCP server)

In Claude Code:

```text
/plugin marketplace add jeremybelcher/product-pillars-agent-kit
/plugin install product-pillars@product-pillars
```

Then run `/mcp`, pick `product-pillars`, choose Authenticate and sign in. If you already added Product Pillars with `claude mcp add`, remove that entry so you don't have two connections to the same server.

### Just the MCP server

| Client | How |
|---|---|
| Claude (web, desktop, mobile) | Settings, Connectors, Add custom connector, paste `https://www.productpillars.com/api/mcp` |
| Claude Code | `claude mcp add --transport http product-pillars https://www.productpillars.com/api/mcp` |
| Cursor, VS Code, Codex, Gemini CLI | One-click links and commands at [productpillars.com/agents](https://www.productpillars.com/agents) |
| Scripts and CI | An API key from [Settings](https://www.productpillars.com/settings), sent as `Authorization: Bearer mc_live_...` |

Sign-in is OAuth: you approve access once, and the agent can only do what your account can do. Signing in creates a free account if you don't have one.

## What the agent can do

`list_diagrams`, `list_projects`, `get_diagram`, `create_diagram` (empty, or from a Mermaid flowchart), `edit_diagram` (batched, conflict-safe edits plus auto layout), `lint_diagram`, `render_diagram`, `update_diagram` and `share_diagram`. Prompts for clients that show them: `draw_flowchart`, `diagram_from_source`, `review_diagram`.

The full agent guide is at [productpillars.com/llms.txt](https://www.productpillars.com/llms.txt).

## Privacy

Connected agents read and write diagrams through your account. Diagram content an agent reads is sent to that agent's provider under their terms. See the [Privacy Policy](https://www.productpillars.com/privacy) and [Terms](https://www.productpillars.com/terms).

## Support

jeremy@jeremybelcher.net
