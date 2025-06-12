# MCP Playground

Playing around with MCP servers to figure out how it works.

Registry of MCP servers can be found [here](https://github.com/modelcontextprotocol/servers?tab=readme-ov-file).

Configure VSCode for MCP.

```bash
mkdir .vscode
touch .vscode/mcp.json
touch .env
```

Where:
* `mcp.json` is the MCP configuration file
* `.env` is where environment variables used by the MCP servers (e.g. for auth) reside

## Servers Configured

I've configured and played with the following MCP servers:

* [Dynatrace](https://github.com/dynatrace-oss/dynatrace-mcp)
* [Bluesky](https://github.com/brianellin/bsky-mcp-server)
* [GitHub](https://github.com/github/github-mcp-server)

## Enabling GitHub Copilot

If you're using [GitHub Copilot as your MCP client](https://code.visualstudio.com/docs/copilot/chat/mcp-servers#_use-mcp-tools-in-agent-mode), you'll have to enable it first. There is a free tier for Copilot that allows:

* 50 agent mode or chat requests per month
* 2,000 completions per month

Learn more [here](https://github.com/features/copilot/plans).