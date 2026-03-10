# What is MCP? (Model Context Protocol)

## Simple Explanation

Think of MCP as a **universal adapter** for AI assistants like GitHub Copilot.

Just like a USB port lets you plug different devices into your computer, MCP lets AI assistants plug into different tools, databases, and services — all using the same standard connection.

## Why Does MCP Exist?

Without MCP, every AI tool needs a **custom integration** for each service it talks to. That means:

- Copilot needs its own code to talk to GitHub
- Copilot needs its own code to talk to Jira
- Copilot needs its own code to talk to your database
- ...and so on for every service

This doesn't scale. MCP fixes this by creating **one standard way** for AI to connect to anything.

## How Does It Work?

MCP has three parts:

| Part | Role | Example |
|------|------|---------|
| **Host** | The AI app you're using | VS Code with GitHub Copilot |
| **Client** | The connector inside the host | Built into Copilot |
| **Server** | The tool/service being connected to | A GitHub MCP server, a database MCP server, etc. |

The flow looks like this:

```
You (ask Copilot something)
  → Copilot (Host + Client)
    → MCP Server (connects to the actual tool)
      → Tool / Service (GitHub, DB, API, etc.)
```

## Real-World Example

Say you ask Copilot: *"Create a GitHub issue for the login bug"*

1. Copilot understands your request
2. Copilot calls the **GitHub MCP Server**
3. The MCP server uses the GitHub API to create the issue
4. Copilot confirms: *"Done! Issue #42 created."*

You never left your editor. Copilot handled everything through MCP.

## How to Use MCP in VS Code

You configure MCP servers in a settings file (`.vscode/mcp.json`):

```json
{
  "servers": {
    "github": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-github"],
      "env": {
        "GITHUB_TOKEN": "your-token-here"
      }
    }
  }
}
```

Once configured, Copilot can automatically discover and use the tools provided by that MCP server.

## Key Benefits

- **One protocol, many tools** — connect to anything without custom code
- **Works inside your editor** — no need to switch between apps
- **Open standard** — anyone can build an MCP server for their service
- **Secure** — you control which servers are connected and what permissions they have

## TL;DR

> MCP is a universal plug-and-play standard that lets GitHub Copilot talk to external tools (GitHub, databases, APIs, etc.) so it can do real things for you — not just generate code.