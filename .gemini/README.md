# Gemini CLI Configuration

This directory contains Gemini CLI configuration and documentation.

## Directory Structure

```
.gemini/
├── README.md                # This file - configuration guide
├── settings.json            # YOUR Gemini CLI settings (version-controlled)
├── extensions.txt           # YOUR extensions to install (version-controlled)
├── .user-settings.json      # Backup during workflow (gitignored)
└── telemetry.log            # Auto-generated debug logs (gitignored)
```

## Overview

**Your Configuration (version-controlled)**:
- **`settings.json`** - Native Gemini CLI settings (MCP servers, model config, etc.)
- **`extensions.txt`** - List of extensions to install (one per line)

**How It Works**:
1. Workflow reads your `settings.json` as the base configuration
2. Adds runtime values (`rootDirectory`, `autoAccept`, optional `telemetry`)
3. Installs extensions from `extensions.txt`
4. Runs Gemini CLI with the merged configuration

**Self-Improvement**:
- The agent can modify `settings.json` and `extensions.txt` to add new capabilities
- Changes to `.gemini/` are committed alongside changes to `memory/`
- Ask the agent: "Add Slack MCP server to our configuration" and it will update `settings.json`

**Note**: The workflow temporarily adds runtime values to `settings.json` (like `rootDirectory`), but extracts any agent changes back to the user settings after execution

## How to Add MCP Servers (Native Gemini CLI Format)

Edit `.gemini/settings.json` to add MCP servers:

```json
{
  "mcpServers": {
    "time": {
      "command": "npx",
      "args": ["-y", "time-node-mcp"]
    },
    "fetch": {
      "command": "npx",
      "args": ["-y", "fetch-mcp"]
    }
  }
}
```

The workflow reads this directly - it's native Gemini CLI configuration!

## How to Add Extensions (Declarative)

Edit `.gemini/extensions.txt` to list extensions (one per line):

```txt
# Gemini CLI Extensions
# GitHub URLs or package names

https://github.com/username/my-extension
@scope/package-name
```

The workflow automatically installs these before running the agent.

## Example MCP Servers

**Note**: Gemini CLI already has **native Google Search and filesystem access**. Use MCP servers for capabilities beyond those.

### Time/Date MCP Server
Timezone-aware date and time operations:
```json
{
  "mcpServers": {
    "time": {
      "command": "npx",
      "args": ["-y", "time-node-mcp"]
    }
  }
}
```

### Fetch Data MCP Server
Fetch JSON, text, and HTML data:
```json
{
  "mcpServers": {
    "fetch": {
      "command": "npx",
      "args": ["-y", "fetch-mcp"]
    }
  }
}
```

### Calculator MCP Server
Mathematical computations and calculations:
```json
{
  "mcpServers": {
    "calculator": {
      "command": "npx",
      "args": ["-y", "calculator-server"]
    }
  }
}
```

### Text Editor MCP Server
Line-oriented text file editor optimized for LLMs:
```json
{
  "mcpServers": {
    "text-editor": {
      "command": "npx",
      "args": ["-y", "mcp-text-editor"]
    }
  }
}
```

### Slack MCP Server
Slack workspace integration (example with environment variables):
```json
{
  "mcpServers": {
    "slack": {
      "command": "npx",
      "args": ["-y", "slack-mcp-server@latest", "--transport", "stdio"],
      "env": {
        "SLACK_MCP_XOXP_TOKEN": "$SLACK_MCP_XOXP_TOKEN"
      }
    }
  }
}
```

**To find more working MCP servers:**
- Browse the curated list: https://raw.githubusercontent.com/punkpeye/awesome-mcp-servers/refs/heads/main/README.md
- Official servers: https://github.com/modelcontextprotocol/servers
- Search npm: https://www.npmjs.com/search?q=mcp-server

**Always verify packages exist before adding them** - check npm or the server's GitHub repository first.

## Environment Variables

MCP servers can reference environment variables using `$VAR_NAME` syntax.

**Add secrets via GitHub:**
```bash
gh secret set BRAVE_API_KEY
gh secret set DATABASE_URL
```

**Reference in workflow:**
```yaml
env:
  BRAVE_API_KEY: ${{ secrets.BRAVE_API_KEY }}
  DATABASE_URL: ${{ secrets.DATABASE_URL }}
```

## MCP Server Configuration Options

Each MCP server supports these properties:

**Required (choose one)**:
- `command`: Path to executable (for stdio transport)
- `url`: SSE endpoint URL
- `httpUrl`: HTTP streaming endpoint URL

**Optional**:
- `args`: Command-line arguments (array)
- `env`: Environment variables (object)
- `cwd`: Working directory (string)
- `timeout`: Request timeout in milliseconds (number)
- `trust`: Bypass tool call confirmations (boolean)
- `includeTools`: Allowlist specific tools (array)
- `excludeTools`: Blocklist specific tools (array)
- `headers`: Custom HTTP headers (object, for HTTP/SSE)

## Finding More MCP Servers

**IMPORTANT - For Agents Adding MCP Servers:**

Before adding a new MCP server, you **MUST**:

1. **Browse available MCP servers:**
   - **Community servers**: https://raw.githubusercontent.com/punkpeye/awesome-mcp-servers/refs/heads/main/README.md (curated list of working servers)
   - **Official servers**: https://github.com/modelcontextprotocol/servers
   - Use Google Search: "MCP server [capability needed]" (e.g., "MCP server database", "MCP server api")

2. **Verify the package exists** by searching:
   - Check the server's GitHub repository for installation instructions
   - Verify on npm: Search "npm [package-name]" to confirm it exists
   - **DO NOT guess package names** - always verify first

3. **Get the correct configuration:**
   - Read the server's documentation for the exact `command`, `args`, and `env` values
   - Many servers use `npx -y [package-name]` but some have different formats
   - Copy the configuration exactly as documented

**Browse MCP servers:**
- https://raw.githubusercontent.com/punkpeye/awesome-mcp-servers/refs/heads/main/README.md (recommended - curated working servers)
- https://github.com/modelcontextprotocol/servers (official reference servers)
- https://www.npmjs.com/search?q=mcp-server (search npm for community servers)

## Resources

- [Gemini CLI Documentation](https://github.com/google-gemini/gemini-cli)
- [MCP Server Integration Guide](https://github.com/google-gemini/gemini-cli/blob/main/docs/tools/mcp-server.md)
- [Model Context Protocol](https://modelcontextprotocol.io/)
