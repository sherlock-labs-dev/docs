---
name: sherlock
description: Use when integrating a service with Sherlock, sending logs, traces, or metrics over OpenTelemetry, instrumenting a Node.js service with @sherlock-labs/otel, or troubleshooting missing telemetry. Also use when a user wants to explore Sherlock data through an AI client.
metadata:
  version: "1.0"
---

# Sherlock

Sherlock stores the logs, traces, and metrics a service sends over OpenTelemetry and links them by trace id. A spike on a chart opens the request behind it, the request opens its trace, and the trace opens its logs.

Documentation: https://sherlock-c8721ead.mintlify.app (page index at /llms.txt; append `.md` to any page URL for Markdown).

## Capabilities

- Send OTLP over HTTP from any OpenTelemetry SDK or an OpenTelemetry Collector to the Sherlock ingest endpoint with a bearer token and an `env` resource attribute.
- Instrument a Node.js service with the Sherlock SDK for Node.js (`@sherlock-labs/otel`): one preload file, automatic HTTP traces and metrics, trace-linked exemplars on every histogram.
- Define custom counters, histograms, and gauges, and record exemplars that carry a trace id.
- Create manual spans around work the automatic instrumentation does not see.
- Ship logs with the trace id stamped, so a trace opens its log lines.
- Query logs, traces, and metrics from an AI client through the Sherlock MCP server.

## Workflows

1. First data: create an organization, copy the collector credentials from Settings → Collector, send OTLP, open the Logs, Traces, and Metrics pages. Page: /get-started/getting-started
2. Node.js service: install the SDK, add the preload file, start with `node --import ./otel.mjs`, set the exporter endpoint and headers, verify data. Pages: /sdk/nodejs/quickstart, /sdk/nodejs/add-telemetry
3. Custom telemetry: /sdk/nodejs/custom-metrics and /sdk/nodejs/manual-spans
4. Missing data: /sdk/nodejs/troubleshooting

## Constraints

- The ingest endpoint and bearer token come from the user's Sherlock organization. Never invent them.
- ESM services must load the SDK through `node --import`, not a top-of-file import, or HTTP spans lose their route names.
- Exemplars appear only on sampled requests.

## MCP servers

- Documentation search: https://sherlock-c8721ead.mintlify.app/mcp (no login)
- User data (logs, traces, metrics): https://mcp.sherlocklabs.dev/mcp (OAuth, see /explore/mcp)
