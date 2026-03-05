# MCP Integration Guide

Connect Japan Property Research data to AI agents through MCP.

## What You Get
- Structured property search and lookup tools
- Agent-friendly JSON responses
- Fast integration path for copilots and proptech workflows

## Quick Setup

### 1) Configure environment
```bash
export JPR_API_KEY="YOUR_API_KEY"
export JPR_API_BASE_URL="https://<your-real-api-host>"
```

### 2) Add server to your MCP client
Use your actual MCP server package/command in client configuration.

Example placeholder (replace with your published package):
```json
{
  "mcpServers": {
    "jpr": {
      "command": "npx",
      "args": ["-y", "<your-real-mcp-server-package>"],
      "env": {
        "JPR_API_KEY": "YOUR_API_KEY",
        "JPR_API_BASE_URL": "https://<your-real-api-host>"
      }
    }
  }
}
```

## Example Agent Prompts
- "Find 3 properties in Tokyo under 80M JPY with nearest station data."
- "Summarize yield and rent trend signals for this listing."

## Tooling Surface (Draft)
- `search_properties`
- `get_property_detail`
- `get_market_snapshot`

## Production Notes
- Rate limits and quotas apply
- Do not expose API keys in client-side code
- Cache read-heavy queries for lower latency and cost
