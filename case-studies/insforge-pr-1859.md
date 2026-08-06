# InsForge Contribution

## Project
InsForge

## Pull Request
https://github.com/InsForge/InsForge/pull/1859

## Title
docs(openapi): Add Usage API Specification

## Problem

The InsForge Usage module — responsible for tracking MCP usage events and aggregated statistics — had no OpenAPI specification. This left the three usage endpoints (`POST /api/usage/mcp`, `GET /api/usage/mcp`, `GET /api/usage/stats`) undocumented in the public API reference, making them invisible to API consumers and integration developers.

## Investigation

I reviewed the existing usage module source to understand the endpoint signatures, request/response schemas, authentication requirements, and error conditions. I also studied the project's existing OpenAPI specs (e.g., `openapi/schedules.yaml`) to align formatting, component reuse, and registration conventions.

## Solution

- Created `openapi/usage.yaml` covering all three usage module endpoints.
- Documented `POST /api/usage/mcp` (record a usage event), `GET /api/usage/mcp` (retrieve usage records), and `GET /api/usage/stats` (fetch aggregated statistics) with full request/response schemas.
- Registered the usage API in `docs/docs.json` across language variants to surface it in the generated public API reference.
- Aligned schema definitions and error responses with the project's existing OpenAPI conventions.

## Impact

- Made the Usage module fully discoverable in the public InsForge API reference.
- Enabled API consumers and integration developers to understand and integrate with usage endpoints without reading source code.
- Improved documentation coverage for the InsForge backend platform.

## Skills Demonstrated

- OpenAPI / Swagger
- API Documentation
- TypeScript
- Backend Documentation
- API Schema Design

## Key Learning

API documentation should be written alongside the implementation, not deferred. Undocumented endpoints create invisible functionality that integration developers cannot leverage, even when the backend is correct.
