# markdown_mcp

A [Model Context Protocol](https://modelcontextprotocol.io) (MCP) server that combines:

- **Web → markdown** — token-efficient fetching (`web_outline`, `web_section`, `web_content`, `web_search`)
- **TechFlow docs** — search and browse embedded documentation (`search_docs`, `get_doc`, `list_categories`)

Everything runs from a **single entry file**: `index.js`.

## Installation

```bash
git clone <repo-url>
cd markdown_mcp
npm install
npx playwright install chromium
```

## Usage

Point your MCP client at `index.js` (use an **absolute path** on your machine).

### Claude Code

Add to your project's `.mcp.json`:

```json
{
  "mcpServers": {
    "markdown_mcp": {
      "type": "stdio",
      "command": "node",
      "args": ["/path/to/markdown_mcp/index.js"]
    }
  }
}
```

### Cursor

Add to `.cursor/mcp.json` in your project root:

```json
{
  "mcpServers": {
    "markdown_mcp": {
      "command": "node",
      "args": ["/path/to/markdown_mcp/index.js"]
    }
  }
}
```

### Windsurf

Add to `~/.codeium/windsurf/mcp_config.json`:

```json
{
  "mcpServers": {
    "markdown_mcp": {
      "command": "node",
      "args": ["/path/to/markdown_mcp/index.js"]
    }
  }
}
```

### Claude Desktop

Add to your Claude Desktop config:

```json
{
  "mcpServers": {
    "markdown_mcp": {
      "command": "node",
      "args": ["/path/to/markdown_mcp/index.js"]
    }
  }
}
```

The `web2md` npm binary (if linked from this package) also runs `index.js`.

## Available Tools

### Web fetching

| Tool | Description |
|------|-------------|
| `web_outline` | Get page structure with heading tree and token counts. **Use this first.** (~200 tokens) |
| `web_section` | Fetch specific section(s) by heading name. Supports partial matches. |
| `web_content` | Get full page as markdown with configurable token cap. |
| `web_search` | Search for a term within a page. Returns matching sections with context excerpts. |

### Documentation

| Tool | Description |
|------|-------------|
| `search_docs` | Full-text search over embedded TechFlow documentation. |
| `get_doc` | Load a document by ID (e.g. `DOC-001`). |
| `list_categories` | List documentation categories and counts. |

## Recommended workflow (web)

```
# Step 1: Get the outline (cheap, ~200 tokens)
web_outline url="https://docs.example.com/api"

# Step 2: Fetch only the sections you need
web_section url="https://docs.example.com/api" headings="Authentication"

# Step 3: Or search for a specific term
web_search url="https://docs.example.com/api" query="rate limit"
```

This tiered approach saves a large share of tokens compared to fetching full pages.

## Features

- Playwright rendering for JavaScript-heavy sites (SPAs)
- Automatic fallback to simple fetch if Playwright fails
- 24-hour local disk cache (`~/.cache/web2md/`)
- External web content wrapped with security tags to reduce prompt-injection risk
- Token estimation for web tool outputs

## Requirements

- Node.js 18+
- Playwright Chromium (`npx playwright install chromium`)

## License

MIT
