# MCP Think Tool Server

[![smithery badge](https://smithery.ai/badge/@cgize/claude-mcp-think-tool)](https://smithery.ai/server/@cgize/claude-mcp-think-tool)

A Model Context Protocol (MCP) server implementing the ["think" tool](https://www.anthropic.com/engineering/claude-think-tool) for improving Claude's complex reasoning capabilities.

## Overview

This MCP server implements Anthropic's "think" tool, which provides Claude with a dedicated space for structured thinking during complex problem-solving tasks. As described in [Anthropic's blog post](https://www.anthropic.com/engineering/claude-think-tool), the think tool has been shown to significantly improve performance in complex tasks requiring policy adherence and reasoning in long chains of tool calls.

## Custom Instructions

Add these custom instructions to Claude to optimize its use of the think tool:

```
You have access to a "think" tool that provides a dedicated space for structured reasoning. Using this tool significantly improves your performance on complex tasks. 

## When to use the think tool 
Before taking any action or responding to the user after receiving tool results, use the think tool as a scratchpad to: 
- List the specific rules that apply to the current request 
- Check if all required information is collected 
- Verify that the planned action complies with all policies 
- Iterate over tool results for correctness 
- Analyze complex information from web searches or other tools 
- Plan multi-step approaches before executing them 

## How to use the think tool effectively 
When using the think tool: 
1. Break down complex problems into clearly defined steps 
2. Identify key facts, constraints, and requirements 
3. Check for gaps in information and plan how to fill them 
4. Evaluate multiple approaches before choosing one 
5. Verify your reasoning for logical errors or biases
```

## Key Use Cases

- **Complex Tool Chains**: When Claude needs to call complex tools and analyze outputs carefully
- **Policy Adherence**: For navigating policy-heavy environments with detailed guidelines
- **Sequential Decision Making**: When each step builds on previous ones and mistakes are costly
- **Multi-step Analysis**: Breaking down complex problems into manageable steps

## Installation

### Installing via Smithery

To install Think Tool Server for Claude Desktop automatically via [Smithery](https://smithery.ai/server/@cgize/claude-mcp-think-tool):

```bash
npx -y @smithery/cli install @cgize/claude-mcp-think-tool --client claude
```

### Manual Installation
```bash
npm install -g @cgize/mcp-think-tool
```

## Configuration

Add this configuration to your MCP configuration file:

```json
{
  "mcpServers": {
    "think-tool": {
      "command": "npx",
      "args": [
        "-y",
        "@cgize/mcp-think-tool"
      ],
      "type": "stdio",
      "pollingInterval": 30000,
      "startupTimeout": 30000,
      "restartOnFailure": true
    }
  }
}
```

Configuration file location:
- `C:\Users\[username]\AppData\Roaming\Claude\claude_desktop_config.json`

If installed globally, you can also use:

```json
{
  "mcpServers": {
    "think-tool": {
      "command": "claude-mcp-think-tool",
      "args": [],
      "type": "stdio",
      "pollingInterval": 30000,
      "startupTimeout": 30000,
      "restartOnFailure": true
    }
  }
}
```

## Available Tools

- **think**: Record structured reasoning during problem-solving
- **get_thoughts**: Retrieve all recorded thoughts 
- **clear_thoughts**: Reset the thinking process
- **get_thought_stats**: Analyze thinking patterns

## Example Prompt

```
Using the think tool, solve this multi-step problem:

A train travels at a constant speed of 60 km/h. It departs from station A at 9:00 AM and arrives at station B at 11:30 AM. What is the distance between stations A and B?
```

## License

MIT
