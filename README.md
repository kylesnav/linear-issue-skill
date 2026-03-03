# linear-issue-skill

Full Linear issue lifecycle in Claude Code — read, create, update, comment, and hand off issues without leaving your terminal.

## What it does

- **Read** — Agent-briefing format: status, description, checklist progress, sub-issues, comments, relations
- **Create** — Single issue from a one-liner, with label and project inference
- **Batch create** — Multiple issues with dependency tracking; shows a summary table before creating
- **Update** — Status transitions, priority, labels, assignee via shorthand syntax
- **Comment** — Add comments or handoff notes to any issue
- **Checklist** — Check/uncheck individual items in an issue's description checklist
- **Sub-issue** — Create child issues inheriting team and project from the parent
- **Compound handoff** — Close one issue and leave a handoff note on the next in one command

## Prerequisites

The [Linear MCP plugin](https://linear.app/docs/mcp) must be installed and authenticated in Claude Code. The skill uses `mcp__plugin_linear_linear__*` tools.

## Installation

Copy `SKILL.md` into your Claude skills directory:

```sh
mkdir -p ~/.claude/skills/linear-issue
cp SKILL.md ~/.claude/skills/linear-issue/SKILL.md
```

That's it. Claude Code loads skills automatically from `~/.claude/skills/`.

## Usage

| Invocation | Mode |
|---|---|
| `/linear-issue` | Ask what to do |
| `/linear-issue PROJ-42` | Read issue |
| `/linear-issue PROJ-42 status:done` | Update status |
| `/linear-issue PROJ-42 priority:urgent` | Update priority |
| `/linear-issue comment PROJ-42 "note here"` | Add comment |
| `/linear-issue handoff PROJ-42 "message"` | Add handoff note |
| `/linear-issue handoff PROJ-42 -> PROJ-43 "message"` | Close and hand off |
| `/linear-issue check PROJ-42 2` | Check off item 2 |
| `/linear-issue sub PROJ-42 Fix the thing` | Create sub-issue |
| `/linear-issue Add health check endpoint` | Create issue |
| `/linear-issue` + multiline list | Batch create |

## Modes reference

**Read** — Fetches issue, comments, and sub-issues. Renders a structured briefing: status, priority, labels, project, description, checklist progress, sub-issues, relations, and recent comments.

**Create** — Parses title from arguments. Resolves team automatically (auto-selects if only one team exists; asks if multiple). Infers labels from keywords (bug, feature, improvement, etc.) and project from context.

**Batch create** — Parses a list of issues, infers labels and dependencies, presents a confirmation table, then creates in dependency order.

**Update** — Reads the issue first, applies changes, reports the transition (e.g., `PROJ-42: In Progress → Done`). Supports status shorthands: `todo`, `progress`/`wip`, `done`/`close`, `blocked`, `backlog`, `canceled`.

**Comment** — Adds a comment to an existing issue. `handoff` keyword prefixes the body with a **Handoff Note** marker.

**Checklist** — Reads and writes the checklist embedded in an issue's description. Supports check, uncheck, and check-all.

**Sub-issue** — Creates a child issue inheriting team and project from the parent.

**Compound handoff** — Sets the source issue to Done and leaves a handoff comment on the target issue in one step.

## License

MIT
