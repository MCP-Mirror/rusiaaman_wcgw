# Shell and Coding agent for Claude and Chatgpt

- Claude - An MCP server on claude desktop for autonomous shell and coding agent. (mac only)
- Chatgpt - Allows custom gpt to talk to your shell via a relay server. (linux or mac)


⚠️ Warning: do not use this repo if you aren't scared of "Autonomous shell command execution"

[![Tests](https://github.com/rusiaaman/wcgw/actions/workflows/python-tests.yml/badge.svg?branch=main)](https://github.com/rusiaaman/wcgw/actions/workflows/python-tests.yml)
[![Mypy strict](https://github.com/rusiaaman/wcgw/actions/workflows/python-types.yml/badge.svg?branch=main)](https://github.com/rusiaaman/wcgw/actions/workflows/python-types.yml)
[![Build](https://github.com/rusiaaman/wcgw/actions/workflows/python-publish.yml/badge.svg)](https://github.com/rusiaaman/wcgw/actions/workflows/python-publish.yml)
[![codecov](https://codecov.io/gh/rusiaaman/wcgw/graph/badge.svg)](https://codecov.io/gh/rusiaaman/wcgw)

## Updates

- [9 Dec 2024] [Vscode extension to paste context on Claude app](https://marketplace.visualstudio.com/items?itemName=AmanRusia.wcgw)  

- [01 Dec 2024] Removed author hosted relay server for chatgpt.

- [26 Nov 2024] Introduced claude desktop support through mcp

## 🚀 Highlights

- ⚡ **Create, Execute, Iterate**: Ask claude to keep running compiler checks till all errors are fixed, or ask it to keep checking for the status of a long running command till it's done.
- ⚡ **Large file edit**: Supports large file incremental edits to avoid token limit issues. Faster than full file write.
- ⚡ **Syntax checking on edits**: Reports feedback to the LLM if its edits have any syntax errors, so that it can redo it.
- ⚡ **Interactive Command Handling**: Supports interactive commands using arrow keys, interrupt, and ansi escape sequences.
- ⚡ **Full Shell Access**: No restrictions, complete control.

## Top use cases examples

- Solve problem X using python, create and run test cases and fix any issues. Do it in a temporary directory
- Find instances of code with X behavior in my repository
- Git clone https://github.com/my/repo in my home directory, then understand the project, set up the environment and build
- Create a golang htmx tailwind webapp, then open browser to see if it works (use with puppeteer mcp)
- Edit or update a large file
- In a separate branch create feature Y, then use github cli to create a PR to original branch
- Command X is failing in Y directory, please run and fix issues
- Using X virtual environment run Y command
- Using cli tools, create build and test an android app. Finally run it using emulator for me to use
- Fix all mypy issues in my repo at X path.
- Using 'screen' run my server in background instead, then run another api server in bg, finally run the frontend build. Keep checking logs for any issues in all three
- Create repo wide unittest cases. Keep iterating through files and creating cases. Also keep running the tests after each update. Do not modify original code.

## Claude Setup

First install `uv` using homebrew `brew install uv`

(**Important:** use homebrew to install uv. Otherwise make sure `uv` is present in a global location like /usr/bin/)

Then update `claude_desktop_config.json` (~/Library/Application Support/Claude/claude_desktop_config.json)

```json
{
  "mcpServers": {
    "wcgw": {
      "command": "uv",
      "args": [
        "tool",
        "run",
        "--from",
        "wcgw@latest",
        "--python",
        "3.12",
        "wcgw_mcp"
      ]
    }
  }
}
```

Then restart claude app.

_If there's an error in setting up_

- If there's an error like "uv ENOENT", make sure `uv` is installed. Then run 'which uv' in the terminal, and use its output in place of "uv" in the configuration.
- If there's still an issue, check that `uv tool run --from wcgw@latest --python 3.12 wcgw_mcp` runs in your terminal. It should have no output and shouldn't exit.
- Debug the mcp server using `npx @modelcontextprotocol/inspector@0.1.7 uv tool run --from wcgw@latest --python 3.12 wcgw_mcp`


### Usage

Wait for a few seconds. You should be able to see this icon if everything goes right.

![mcp icon](https://github.com/rusiaaman/wcgw/blob/main/static/rocket-icon.png?raw=true)
over here

![mcp icon](https://github.com/rusiaaman/wcgw/blob/main/static/claude-ss.jpg?raw=true)

Then ask claude to execute shell commands, read files, edit files, run your code, etc.


### [Optional] Vs code extension 
https://marketplace.visualstudio.com/items?itemName=AmanRusia.wcgw

Commands: 
- Select a text and press `cmd+'` and then enter instructions. This will switch the app to Claude and paste a text containing your instructions, file path, workspace dir, and the selected text.

## Chatgpt Setup

Read here: https://github.com/rusiaaman/wcgw/blob/main/openai.md

## Examples

![example](https://github.com/rusiaaman/wcgw/blob/main/static/example.jpg?raw=true)

## [Optional] Local shell access with openai API key or anthropic API key

### Openai

Add `OPENAI_API_KEY` and `OPENAI_ORG_ID` env variables.

Then run

`uvx --from wcgw@latest wcgw_local  --limit 0.1` # Cost limit $0.1

You can now directly write messages or press enter key to open vim for multiline message and text pasting.

### Anthropic

Add `ANTHROPIC_API_KEY` env variable.

Then run

`uvx --from wcgw@latest wcgw_local --claude`

You can now directly write messages or press enter key to open vim for multiline message and text pasting.
