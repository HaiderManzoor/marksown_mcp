# markdown-mcp

An MCP server that converts web pages to clean markdown — optimized for LLM context efficiency.

## Tools

| Tool | Description | Token Cost |
|------|-------------|------------|
| `web_outline` | Extract heading structure | ~200 tokens |
| `web_section` | Fetch specific sections by heading | Low-medium |
| `web_search` | Search for terms within a page | Low |
| `web_full` | Full page to markdown | High |

## Usage

```bash
npm install
node index.js
```

## MCP Configuration

```json
{
  "mcpServers": {
    "web2md": {
      "type": "stdio",
      "command": "node",
      "args": ["/path/to/markdown-mcp/index.js"]
    }
  }
}
```

## Recommended Workflow

1. Use `web_outline` first to see the page structure (~200 tokens)
2. Use `web_section` to fetch only the sections you need
3. Use `web_search` to find specific terms without loading everything
4. Use `web_full` only when you truly need the entire page

This tiered approach saves ~97% of context tokens compared to always fetching full pages.
