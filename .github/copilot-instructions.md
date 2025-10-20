---
applyTo: "**"
---
# Dynatrace MCP server query standards

## Data filtering guidelines
- If the value of DT_ENVIRONMENT is "https://wkf10640.apps.dynatrace.com", then always filter by segment name "Astroshop". For any other value of DT_ENVIRONMENT, don't filter by segment name.

## Display guidelines
Use the name field, not the ID field when listing services.