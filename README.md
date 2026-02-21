# Weather MCP Server

An [MCP](https://modelcontextprotocol.io/) server that provides weather data for the US via the [National Weather Service API](https://www.weather.gov/documentation/services-web-api). Built with [FastMCP](https://github.com/modelcontextprotocol/python-sdk).

## Tools

| Tool | Description | Parameters |
|------|-------------|------------|
| `get_alerts` | Get active weather alerts for a US state | `state` — two-letter state code (e.g. `CA`, `NY`) |
| `get_forecast` | Get weather forecast for a location | `latitude`, `longitude` — coordinates of the location |

## Prerequisites

- Python 3.12+
- [uv](https://docs.astral.sh/uv/)

## Setup

```bash
# Clone the repository
git clone https://github.com/Javirum/weather-mcp-server.git
cd weather-mcp-server

# Install dependencies
uv sync
```

## Running the server

```bash
# Via entry point
uv run weather

# Or via python -m
uv run python -m weather
```

The server runs over **stdio** transport, designed to be launched by an MCP client (e.g. Claude Desktop).

## Claude Desktop configuration

Add this to your Claude Desktop config (`~/Library/Application Support/Claude/claude_desktop_config.json` on macOS):

```json
{
  "mcpServers": {
    "weather": {
      "command": "uv",
      "args": [
        "--directory",
        "/absolute/path/to/weather-mcp-server",
        "run",
        "weather"
      ]
    }
  }
}
```

## Project structure

```
src/weather/
  __init__.py     Package marker
  __main__.py     python -m weather entry point
  server.py       FastMCP server, constants, and tool definitions
  helpers.py      NWS API client and response formatters
```
