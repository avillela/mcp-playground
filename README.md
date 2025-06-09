# mcp-playground

Playing around with MCP servers to figure out how it works.

Registry of MCP servers can be found [here](https://github.com/modelcontextprotocol/servers?tab=readme-ov-file).

Configure VSCode for MCP.

```bash
mkdir .vscode
touch .vscode/mcp.json
touch .env
```

Where:
* [`mcp.json`] is the MCP configuration file
* [`.env`] is where environment variables used by the MCP servers (e.g. for auth) reside

# Servers

I've configured the following MCP servers:

* [Dynatrace](https://github.com/dynatrace-oss/dynatrace-mcp)
* [Bluesky](https://github.com/brianellin/bsky-mcp-server)
* [GitHub](https://github.com/github/github-mcp-server)
