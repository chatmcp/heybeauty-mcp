[![MseeP.ai Security Assessment Badge](https://mseep.net/pr/chatmcp-heybeauty-mcp-badge.png)](https://mseep.ai/app/chatmcp-heybeauty-mcp)

# HeyBeauty MCP Server

HeyBeauty Virtual TryOn

This is a TypeScript-based MCP server that implements virtual tryon using HeyBeauty API. It demonstrates core MCP concepts by providing:

- Resources representing clothes with URIs and metadata
- Tools for submit tryon task and query task info.
- Prompts for tryon cloth.

## Quick Start

1. apply for [HeyBeauty API Key](https://doc.heybeauty.ai/try-on)

2. add the server config to MCP Client config file

```json
{
  "mcpServers": {
    "heybeauty-mcp": {
      "command": "npx",
      "args": ["-y", "heybeauty-mcp"],
      "env": {
        "HEYBEAUTY_API_KEY": "your_heybeauty_api_key"
      }
    }
  }
}
```

### Resources

- List and access clothes via `cloth://` URIs
- Each cloth has a id, name, description, image url and metadata
- Plain text mime type for simple content access

### Tools

- `submit_tryon_task` - Submit a tryon task
  - Takes user image url, cloth image url, cloth id and cloth description as required parameters
  - Stores tryon task in server state
- `query_tryon_task` - Query a tryon task
  - Takes task id as required parameter
  - Returns tryon task info

### Prompts

- `tryon_cloth` - Tryon cloth
  - Takes user image url, cloth image url, cloth id and cloth description as required parameters
  - Returns structured prompt for LLM tryon

### Resources

- `cloth://` - URI for clothes
  - Each cloth has a id, name, description, image url and metadata

## Development

Install dependencies:

```bash
npm install
```

Build the server:

```bash
npm run build
```

For development with auto-rebuild:

```bash
npm run watch
```

## Installation

To use with Claude Desktop, add the server config:

On MacOS: `~/Library/Application Support/Claude/claude_desktop_config.json`
On Windows: `%APPDATA%/Claude/claude_desktop_config.json`

```json
{
  "mcpServers": {
    "heybeauty-mcp": {
      "command": "node",
      "args": ["/path/to/heybeauty-mcp/build/index.js"]
    },
    "env": {
      "HEYBEAUTY_API_KEY": "your_heybeauty_api_key"
    }
  }
}
```

Follow this document to [get HeyBeauty API Key](https://doc.heybeauty.ai/try-on).

### Debugging

Since MCP servers communicate over stdio, debugging can be challenging. We recommend using the [MCP Inspector](https://github.com/modelcontextprotocol/inspector), which is available as a package script:

```bash
npm run inspector
```

The Inspector will provide a URL to access debugging tools in your browser.
