# MCP Server Streamable

A Model Context Protocol (MCP) server implementation using FastMCP with streamable HTTP transport.

## Overview

This project demonstrates how to create an MCP server that runs over HTTP with streamable transport. The server provides a simple greeting tool that can be called by MCP clients.

## Features

- **HTTP Transport**: Uses streamable HTTP transport for communication
- **FastMCP Framework**: Built with the FastMCP library for easy server development
- **Simple Tool**: Includes a greeting tool that takes a name parameter

## Prerequisites

- Python 3.8+
- [uv](https://docs.astral.sh/uv/) (recommended for fast package management)

## Installation

1. Clone or navigate to the project directory:
```bash
cd d:\work\projects\mcp-servers-course\mcp-server-streamable
```

2. Install dependencies using uv:
```bash
uv sync
```

This will automatically create a virtual environment and install all dependencies from the `pyproject.toml` file.

3. Activate the virtual environment:
```bash
uv run python server.py
```

Or manually activate:
```bash
.venv\Scripts\activate
```

## Usage

### Running the Server

Start the MCP server:
```bash
python server.py
```

Or using uv:
```bash
uv run python server.py
```

The server will start on the default port and be accessible via HTTP.

### Available Tools

#### greeting
- **Description**: Send a personalized greeting
- **Parameter**: `name` (string) - The name to include in the greeting
- **Returns**: A greeting message

Example usage:
```python
# When called with name="Alice"
# Returns: "Hi Alice"
```

## Configuration for Claude Desktop

To use this server with Claude Desktop, add the following configuration to your `claude_desktop_config.json` file:

```json
{
    "mcpServers": {
        "streamable-server": {
            "command": "python",
            "args": ["d:\\work\\projects\\mcp-servers-course\\mcp-server-streamable\\server.py"]
        }
    }
}
```

Alternatively, if you want to use the remote HTTP endpoint:

```json
{
    "mcpServers": {
        "streamable-server": {
            "command": "npx",
            "args": [
                "mcp-remote",
                "http://127.0.0.1:8000/mcp",
                "--allow-http"
            ]
        }
    }
}
```

## Development

### Project Structure

```
mcp-server-streamable/
├── server.py          # Main server implementation
├── README.md          # This file
└── .venv/            # Virtual environment
```

### Extending the Server

To add new tools, define functions with the `@mcp.tool()` decorator:

```python
@mcp.tool()
def your_tool_name(param: str) -> str:
    """Tool description"""
    # Your implementation here
    return result
```

## Transport Details

This server uses the "streamable-http" transport, which:
- Provides HTTP-based communication
- Supports streaming responses
- Is suitable for web-based integrations
- Allows for remote access over HTTP

## Troubleshooting

1. **Port conflicts**: If the default port is in use, the server will indicate this in the logs
2. **Virtual environment**: Ensure the virtual environment is activated before running
3. **Dependencies**: Make sure all required packages are installed with `uv sync`

## License

This project is part of the MCP servers course and is intended for educational purposes.