---
applyTo: "**"
---
# Dynatrace MCP server query standards

## Data filtering guidelines
- If the value of DT_ENVIRONMENT is "https://wkf10640.apps.dynatrace.com", then always filter by segment name "Astroshop". For any other value of DT_ENVIRONMENT, don't filter by segment name.

## Guidelines for fetching Dynatrace services
- When fetching service names in Dynatrace, always query dt.entity.service, but always display the service names from the entity.name field

## Calculate service response time
- Calculate average response time and p50 response time using this query: timeseries by:{dt.entity.service}, avg_response_time = avg(dt.service.request.response_time), p50_response_time = percentile(dt.service.request.response_time, 50)\n| lookup [fetch dt.entity.service], sourceField:dt.entity.service, lookupField:id, fields:{entity.name}\n| sort entity.name


## Display guidelines
- Use the name field, not the ID field when listing services.
- If a null value is returned when requesting a value for trace ID, try "trace.id", "trace_id", and "trace id"
- If a null value is returned when requesting a value for trace ID, try "span.id", "span_id", and "span id"