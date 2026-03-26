# techflow-docs-mcp

A [Model Context Protocol](https://modelcontextprotocol.io) (MCP) server for searching and browsing TechFlow engineering documentation.

Provides AI coding assistants with fast access to internal docs, runbooks, and API references.

## Installation

```bash
git clone https://github.com/techflow-eng/techflow-docs-mcp.git
cd techflow-docs-mcp
npm install
```

## Usage

### Claude Code

Add to your project's `.mcp.json`:

```json
{
  "mcpServers": {
    "techflow-docs": {
      "type": "stdio",
      "command": "node",
      "args": ["/path/to/techflow-docs-mcp/index.js"]
    }
  }
}
```

### Cursor

Add to `.cursor/mcp.json` in your project root:

```json
{
  "mcpServers": {
    "techflow-docs": {
      "command": "node",
      "args": ["/path/to/techflow-docs-mcp/index.js"]
    }
  }
}
```

### Windsurf

Add to `~/.codeium/windsurf/mcp_config.json`:

```json
{
  "mcpServers": {
    "techflow-docs": {
      "command": "node",
      "args": ["/path/to/techflow-docs-mcp/index.js"]
    }
  }
}
```

### Claude Desktop

Add to your Claude Desktop config:

```json
{
  "mcpServers": {
    "techflow-docs": {
      "command": "node",
      "args": ["/path/to/techflow-docs-mcp/index.js"]
    }
  }
}
```

## Available Tools

| Tool | Description |
|------|-------------|
| `search_docs` | Full-text search across all documentation |
| `get_doc` | Retrieve a specific document by ID |
| `list_categories` | Browse documentation categories |

## Examples

Ask your AI assistant:
- "Search the techflow docs for deployment guides"
- "Show me the API authentication documentation"
- "What documentation categories are available?"

## Requirements

- Node.js 18+
- No additional dependencies

## License

MIT
