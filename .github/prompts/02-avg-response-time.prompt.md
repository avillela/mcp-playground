---
mode: 'agent'
model: GPT-4o
tools: ['runCommands', 'npx-dynatrace-mcp-server']
description: 'Print average response time per service'
---
Your goal is to display the average response time for each service in Dynatrace.

Requirements:
* List the name of each service
* Next to each service name, display the average response time for that service