# Japan Property Research MCP Integration

MCP-first integration for AI agents and proptech workflows.

## Website
- https://japanpropertyresearch.com

## Endpoint
- `https://japanpropertyresearch.com/mcp`

## Transport and Auth
- Transport: HTTP + JSON-RPC 2.0
- Auth header: `Authorization: Bearer jpnr_...`
- API key format: `jpnr_...`

## MCP Server Metadata
- Server name: `japanpropertyresearch-research-mcp-http`
- Version: `0.1.0`
- Supported protocol versions:
  - `2025-06-18`
  - `2025-03-26`
  - `2024-11-05`

## Supported Methods
- `initialize`
- `notifications/initialized`
- `tools/list`
- `tools/call`
- `ping`

## Tool Catalog
- `resolve_location`
- `get_land_price_evidence`
- `get_climate_summary`
- `get_amenities_summary`
- `get_transport_summary`
- `get_zoning_summary`
- `get_designated_schools`
- `get_listings_nearby`
- `get_listing_detail`
- `get_past_transactions`
- `generate_market_insight_brief`

## Client Setup

### Cursor
```json
{
  "mcpServers": {
    "japanpropertyresearch": {
      "url": "https://japanpropertyresearch.com/mcp",
      "headers": {
        "Authorization": "Bearer jpnr_********************************"
      }
    }
  }
}
```

### VS Code
```json
{
  "servers": {
    "japanpropertyresearch": {
      "type": "http",
      "url": "https://japanpropertyresearch.com/mcp",
      "headers": {
        "Authorization": "Bearer jpnr_********************************"
      }
    }
  }
}
```

### Claude Code
```bash
claude mcp add --transport http japanpropertyresearch https://japanpropertyresearch.com/mcp --header "Authorization: Bearer jpnr_********************************"
```

### Generic MCP Client
```json
{
  "japanpropertyresearch": {
    "url": "https://japanpropertyresearch.com/mcp",
    "headers": {
      "Authorization": "Bearer jpnr_********************************"
    }
  }
}
```

## Quick Verification (cURL)

### 1) Discovery
```bash
curl -s https://japanpropertyresearch.com/mcp | jq
```

### 2) Initialize
```bash
curl -s https://japanpropertyresearch.com/mcp \
  -H "Content-Type: application/json" \
  -d '{
    "jsonrpc":"2.0",
    "id":1,
    "method":"initialize",
    "params":{"protocolVersion":"2025-06-18"}
  }' | jq
```

### 3) List Tools
```bash
curl -s https://japanpropertyresearch.com/mcp \
  -H "Content-Type: application/json" \
  -d '{"jsonrpc":"2.0","id":2,"method":"tools/list","params":{}}' | jq
```

### 4) Call Tool (requires API key)
```bash
curl -s https://japanpropertyresearch.com/mcp \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer jpnr_********************************" \
  -d '{
    "jsonrpc":"2.0",
    "id":3,
    "method":"tools/call",
    "params":{
      "name":"resolve_location",
      "arguments":{"address":"Shibuya, Tokyo"}
    }
  }' | jq
```

## Access and Keys
Generate/revoke keys in the Japan Property Research developer dashboard, then pass the key as Bearer auth.

## Troubleshooting
- `-32001 Unauthorized`: missing/invalid Bearer key.
- `-32600 Invalid Request`: malformed JSON-RPC envelope.
- `-32601 Method not found`: method is not supported.
- Tool error in `result.isError=true`: input or upstream data issue; inspect `result.content`.
