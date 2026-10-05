# Interact_GW_Weather_MCP_Server

## Overview

This sample project demonstrates an MCP (Model Context Protocol) Server connection on a DataPower Nano Gateway. It provisions an MCP Server that exposes weather data tools backed by the Singapore Weather API.

The MCP Server provides tools to discover weather stations and retrieve real-time air temperature readings from weather stations across Singapore, sourced from the National Environment Agency (NEA). This example shows how to expose any OpenAPI-based service as a set of MCP Server tools.

## MCP Tools

The following tool is exposed by this MCP Server:

### 1. get-air-temperature
Fetches current or historical air temperature readings from weather stations across Singapore. Data is updated approximately every 5 minutes and covers observations from May 2016 to present.

**Optional Parameters:**
- `station_id`: Filter by specific weather station (e.g., "S101").
- `start_time`: Filter readings from this ISO-8601 timestamp (e.g., "2025-11-11T00:00:00+08:00")
- `end_time`: Filter readings up to this ISO-8601 timestamp (e.g., "2025-11-11T12:00:00+08:00")

**Returns:** Temperature readings with station_id, timestamp, and temperature in Celsius

## Components

- **weather-api-spec.json**: OpenAPI 3.0.3 specification for the Singapore Weather API with the endpoint:
  - `/air-temperature` - Retrieves temperature readings
- **DPNano_MCPServer.yml**: MCP Server configuration that defines the server capabilities and references the tools
- **DPNano_MCPTools.yml**: Defines the MCP tools that map to the Weather API operations with detailed descriptions
- **DPNano_Invoke.yml**: Invoke policy that routes requests to the backend weather API endpoint
- **DPNano_PolicySequence.yml**: Policy sequence that orchestrates the request flow
- **DPNano_Quota.yml**: Quota configuration limiting requests to 1000 per minute
- **DPNano_Telemetry.yml**: Telemetry configuration for monitoring and metrics collection

## Use Case

This example demonstrates how to:
1. Expose multiple related API endpoints as MCP tools
2. Provide rich, descriptive tool documentation for LLM consumption
3. Create a discoverable API pattern (list stations → query temperature data)
4. Apply gateway policies (quota, telemetry) to MCP Server tools
