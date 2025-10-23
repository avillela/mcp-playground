# MCP Playground

This repo is used primarily for experimenting with the Dynatrace MCP server.

You can check out other MCP servers [here](https://github.com/modelcontextprotocol/servers?tab=readme-ov-file).

Check out my blog post on how to use the Dynatrace MCP server [here](https://dt-url.net/mcp-medium).

## Why use the Dynatrace MCP Server?

This approach makes Dynatrace data accessible to team members who may not be familiar with DQL or APIs, democratizing observability data across your organization.

Key Takeaways:
* Natural Language Queries: Interact with Dynatrace without writing complex API calls or DQL queries
* Reusable Prompts: Save time with pre-built queries stored as files
* AI-Powered Analysis: Let Copilot handle complex, multi-step queries automatically

## Setup

### Step 1: Enable MCP support in VSCode

This tutorial uses the Visual Studio Code (VSCode) [built-in GitHub Copilot chat support](https://code.visualstudio.com/docs/copilot/customization/mcp-servers#_enable-mcp-support-in-vs-code). Copilot supports multiple large language models (LLMs), including GPT-4 and Claude, so feel free to select your favorite. 

Before you can use GitHub Copilot chat, however, you’ll need to [enable MCP support in VSCode](https://code.visualstudio.com/docs/copilot/customization/mcp-servers#_enable-mcp-support-in-vs-code). You can do this by adding “chat.mcp.enabled”: true to your VSCode [`settings.json`](https://code.visualstudio.com/docs/getstarted/settings#_settings-json-file) file. 

### Step 2: Configure Dynatrace MCP server 

The LLM used by GitHub Copilot chat talks to Dynatrace via the [Dynatrace MCP server](https://dt-url.net/mcp). For that to happen, we must make Copilot aware of the Dynatrace MCP server, which I’ll show you below.

If you open up [`.vscode/mcp.json`](.vscode/mcp.json), you'll notice the configureation for the Dynatrace MCP server:

```json
{ 
  "servers": {
    // https://github.com/dynatrace-oss/dynatrace-mcp
    "npx-dynatrace-mcp-server": {
      "type": "stdio",
      "command": "npx",
      "args": ["-y", "@dynatrace-oss/dynatrace-mcp-server@0.10.0"],
      "envFile": "${workspaceFolder}/.env.av"
    },
  }
}
```

Let’s take a closer look at the above JSON:
* `npx-dynatrace-mcp-server`: the name of the MCP server. This name can be anything you want, even Dynatrace MCP server, spaces and all.
* `type`: The connection type. Valid values are: `stdio`, `sse`, and `http`. We’re using `stdio`, which means that a copy of the Dynatrace MCP server runs locally in VSCode. `sse` and `http` are used for accessing remote MCP servers. For more information on remote vs. local MCP servers, check out [this great overview](https://www.apideck.com/blog/understanding-local-and-remote-model-context-protocols).
* `command`: The command to run the MCP server. Since the type is `stdio`, the Dynatrace MCP server will run locally, which requires a command to run the server. The Dynatrace MCP server is available as an executable npm package, so it uses the `npx` command to run it (already installed in this dev container).
* `args`: The arguments passed to the npx command. Here, we have 2 `args`. the `-y` arg tells npx to install dependent packages without prompting, and the second arg includes the package name (`dynatrace-oss/dynatrace-mcp-server`), and version (`v0.10.0`). If you want to use a version other than latest, check out the [list of available versions of the Dynatrace MCP server](https://github.com/dynatrace-oss/dynatrace-mcp/tags).
* `envFile`: Environment variable file. The Dynatrace MCP server requires that you set certain environment variables so that you can interact with Dynatrace. This tells VSCode to look for an .env file in the VSCode workspace root.

Before we can start up the Dynatrace MCP server, we need to a Dynatrace platform token. For this, you will need to create a .env file.:

```bash
cp .env.template .env
```
And then fill in the values for the following environment variables:

* `DT_PLATFORM_TOKEN`: your Dynatrace Platform Token
* `DT_ENVIRONMENT`: "https://<your_dt_tenant>.apps.dynatrace.com"

To create your Dynatrace platform token, follow the instructions [here](https://docs.dynatrace.com/docs/manage/identity-access-management/access-tokens-and-oauth-clients/platform-tokens). Also check out the [Dynatrace MCP server README](https://github.com/dynatrace-oss/dynatrace-mcp?tab=readme-ov-file#scopes-for-authentication) for a list of authentication scopes to include for the platform token.

### Step 3: Start the Dynatrace MCP server

To start the MCP server, open mcp.json in VSCode, and click “Start”, located just above `npx-dynatrace-mcp-server`.

![Start DT MCP server](images/mcp-server-pre-start.png)

Once the MCP server is started, you should see “Running” in place of “Start”:

![Running DT MCP server](images/mcp-server-running.png)

If your MCP server fails to start up, you’ll be able to see error logs in the Output tab in VSCode:

![MCP server startup logs](images/mcp-server-startup-logs.png)

### Step 4: Start up the chatbot

Before we can start talking to Dynatrace, we need to open up the Copilot chat window. to open the chat window, select the on the chat icon just to the right of the [command palette in VSCode](https://code.visualstudio.com/api/ux-guidelines/command-palette), and select “Open Chat”.

![GitHub copilot open chat](images/gh-copilot-open-chat.png)

This will open up a chat window. You will also be prompted to enable GitHub Copilot, if you don’t already have it enabled.

> ✨ **NOTE:** [GitHub copilot includes a free tier](https://github.com/features/copilot/plans), which limits you 50 agent mode or chat requests per month.

Once the chat is enabled, make sure that your chat is set to “Agent” mode. Agent mode allows copilot to do things on your behalf, like modify code and configurations, depending on what MCP servers it’s interacting with. Ask mode is used for lookups and research type tasks. Edit mode lies somewhere in between. Learn more about the modes [here](https://github.blog/ai-and-ml/github-copilot/copilot-ask-edit-and-agent-modes-what-they-do-and-when-to-use-them/).

To switch modes, go to the bottom right-hand side of the chat input box. This will open a list of available chat modes.

![GitHub copilot select chat mode](images/gh-copilot-chat-mode.png)

### Step 5: Talk to Dynatrace!

I have created [prompt files](https://code.visualstudio.com/docs/copilot/customization/prompt-files) and an [instructions file](https://code.visualstudio.com/docs/copilot/customization/custom-instructions) for more detailed interactions with the [OpenTelemetry Demo app](https://github.com/open-telemetry/opentelemetry-demo) (Astroshop) via the Dynatrace MCP server.

To run the prompt files, open up Copilot chat, and type in `/`. This will bring up a list of available prompts. Note that Copilot looks for prompt files in the [`.github/prompts`](.github/prompts/) folder. All prompt files must have a `.prompt.md` extension.

Here are the prompts to execute:
* `/01-num-dynatrace-services.prompt.md` -> How many services are running in Dynatrace astroshop namespace?
* `/02-avg-response-time.prompt.md` -> Give me the avg response time per service in the astroshop namespace?
* `/03-logs-associated-with-services.prompt.md` -> How many astroshop services have associated logs?
* `/04-last-five-traces.prompt.md` -> Show me the last 5 traces, include spand id, trace is, start time, end time and number of associated logs for x service?
* `/05-logs-associated-with-given-span.prompt.md` -> Show me the latest log messages for the most  span in Dynatrace that has associated logs.

## Resources

Learn more about prompt files in VSCode:
* [Prompt files overview](https://code.visualstudio.com/docs/copilot/customization/prompt-files)
* [Instructions overview](https://code.visualstudio.com/docs/copilot/customization/custom-instructions)
* [awesome-copilot repo on GitHub](https://github.com/github/awesome-copilot)
* [Instructions and Prompt Files to supercharge VS Code with GitHub Copilot](https://dev.to/pwd9000/supercharge-vscode-github-copilot-using-instructions-and-prompt-files-2p5e)