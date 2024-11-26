# Claude desktop support

## Setup

Update `claude_desktop_config.json` (~/Library/Application Support/Claude/claude_desktop_config.json)

```json
{
  "mcpServers": {
    "wcgw": {
      "command": "uvx",
      "args": ["--from", "wcgw@latest", "wcgw_mcp"]
    }
  }
}
```

Then restart claude app.

## Usage

Wait for a few seconds. You should be able to see this icon if everything goes right.

![mcp icon](https://github.com/rusiaaman/wcgw/blob/main/static/rocket-icon.png?raw=true)
over here

![mcp icon](https://github.com/rusiaaman/wcgw/blob/main/static/claude-ss.jpg?raw=true)

Then ask claude to execute shell commands, read files, edit files, run your code, etc.

## Example

![example](https://github.com/rusiaaman/wcgw/blob/main/static/example.jpg?raw=true)