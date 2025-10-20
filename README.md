# MCP Playground

This repo is used primarily for experimenting with the Dynatrace MCP server.

You can check out other MCP servers [here](https://github.com/modelcontextprotocol/servers?tab=readme-ov-file).

Check out my blog post on how to use the Dynatrace MCP server [here](https://dt-url.net/mcp-medium).

## Enabling GitHub Copilot

To use [GitHub Copilot as your MCP client](https://code.visualstudio.com/docs/copilot/chat/mcp-servers#_use-mcp-tools-in-agent-mode), you'll have to enable it first. There is a free tier for Copilot that allows:

* 50 agent mode or chat requests per month
* 2,000 completions per month

Learn more [here](https://github.com/features/copilot/plans).

## Advanced use cases with prompt files

I have created prompt files and an instructions file for more detailed interactions with the [OpenTelemetry Demo app](https://github.com/open-telemetry/opentelemetry-demo) (Astroshop) via the Dynatrace MCP server, outside the scope of the original blog post.

The use cases highlighted are as follows:
* How many services are running in Dynatrace astroshop namespace?
* Give me the avg response time per service in the astroshop namespace?
* How many astroshop services have associated logs?
* Show me the last 5 traces, include spand id, trace is, start time, end time and number of associated logs for x service?
* Can you show me the logs associated with Span ID y?

Learn more about prompt files in VSCode:
* [Prompt files overview](https://code.visualstudio.com/docs/copilot/customization/prompt-files)
* [Instructions overview](https://code.visualstudio.com/docs/copilot/customization/custom-instructions)
* [awesome-copilot repo on GitHub](https://github.com/github/awesome-copilot)
* [Instructions and Prompt Files to supercharge VS Code with GitHub Copilot](https://dev.to/pwd9000/supercharge-vscode-github-copilot-using-instructions-and-prompt-files-2p5e)

To run the prompt files, open up Copilot chat, and type in `/<prompt_file_name>`