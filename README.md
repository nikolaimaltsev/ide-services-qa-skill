# IDE Services QA Agent for Claude Code

A Claude Code agent for reproducing, testing, validating, and reviewing JetBrains **IDE Services** tasks — driving the IDE Services UI, Toolbox App, and IntelliJ IDEA from a single Claude session.

---

## Features

- **Browser automation** — interacts with IDE Services web UI via Playwright or Chrome MCP
- **Screenshots** — captures the screen at key steps during reproduction for traceability
- **Full UI coverage** — uses computer vision to see and interact with any UI element, including Toolbox App and IntelliJ IDEA, not just the browser
- **YouTrack & Notion integration** — reads issues and articles from YouTrack, reads and writes Notion pages
- **Multi-modal interaction** — prefers API where possible, falls back to web UI, falls back to computer vision — in that order
- **Product documentation as a source of truth**
- **Glean MCP** to navigate and use comporate knowledge

---

## Deployment

Tested on **Ubuntu 22.04 x11** (Wayland is not supported). The recommended setup is a virtual machine accessed over SSH, which keeps the display available for computer use tools while allowing unattended operation.

You can also run this on your local machine if you want everything in one place.

Most if not all of features works perfectly on **MacOS**. People report successful use. Please try it and let me know. Thourough testing on Mac will follow, if there will be interest.

> **Container deployment (coming soon):** A pre-packaged Linux container is planned so you can pull and run the agent without any manual setup, freeing up your host machine entirely.

---

## Project Structure

```
.
├── .claude
│   ├── settings.local.json   # MCP configuration (managed by Claude Code)
│   └── skills
│       ├── computer-use.md   # Vision, screenshots, xdotool, coordinate math
│       ├── docker.md         # Demo environment lifecycle
│       ├── ide.md            # IntelliJ IDEA interaction
│       ├── ide-services-ui.md # IDE Services web UI
│       └── toolbox.md        # JetBrains Toolbox App interaction
└── CLAUDE.md                 # Agent instructions and routing
```

---

## Getting Started

### Dependencies

Install the following MCPs before first use:

| MCP | Instructions |
|-----|-------------|
| **Chrome** | Bundled with Claude — no installation needed |
| **Playwright** | Claude Code can install this automatically on first use |
| **YouTrack** | See [JT-A-961](https://youtrack.jetbrains.com/articles/JT-A-961) |
| **Opendesk** (computer vision) | [github.com/vitalops/opendesk#mcp-install-claude-code--claude-desktop](https://github.com/vitalops/opendesk#mcp-install-claude-code--claude-desktop) (*extra step might be needed: sudo apt-get install python3-tk python3-dev)|
| **Notion** | `claude mcp add --transport http notion https://mcp.notion.com/mcp` |
| **Glean** | [IDES-A-589](https://youtrack.jetbrains.com/articles/IDES-A-589/install-Glean-mcp) install Glean mcp |

### Starting the Agent

```bash
cd /path/to/this/project
claude
```

Claude Code picks up `CLAUDE.md` automatically. No additional configuration is required.

---

## Roadmap

- [ ] Test on MacOS (if interested)
- [ ] Pre-packaged container — pull and run, no setup required
- [ ] Central claude memory store — shared across QA engineers to accumulate corner cases and speed up future reproduction
- [ ] Git repo integration — for tracking reproduction artifacts (low priority)
- [ ] Glean MCP — available when needed, omitted for now to keep context lean
- [ ] mcp-steroid — might be useful for selected scenarios

---

## Support

Reach out to **nikolai.maltsev@jetbrains.com** on Slack with any problems, questions, or suggestions.
