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
```

### 2) Add server to your MCP client
Use your MCP client config to register the server command.

Example (adapt to your client):
```json
{
  "mcpServers": {
    "jpr": {
      "command": "npx",
      "args": ["-y", "@japan-property-research/mcp-server"],
      "env": {
        "JPR_API_KEY": "YOUR_API_KEY"
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
