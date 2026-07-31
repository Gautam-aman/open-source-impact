# InsForge Contribution

## Project
InsForge

## Pull Request
https://github.com/InsForge/InsForge/pull/1732

## Title
Add OpenAPI Specification for Schedules API

## Problem

The schedules module did not have a dedicated OpenAPI specification, which made the API harder to discover, validate, and consume from generated documentation.

The API reference navigation also did not expose schedules endpoints alongside the rest of the documented platform APIs.

## Investigation

I verified the documented routes against the schedules router implementation and iterated on review feedback to match actual validator behavior, response shapes, and error cases.

## Solution

- Added `openapi/schedules.yaml` for the schedules module.
- Documented all 8 schedules endpoints, including config and execution log routes.
- Added request and response schemas, authentication details, and error responses.
- Registered the schedules API in `docs/docs.json` across supported language variants.

## Testing

Verified the documented routes against `backend/src/api/routes/schedules/index.routes.ts`.

Validated the OpenAPI specification successfully with `swagger-cli`.

Confirmed the repository build completed successfully.

## Impact

- Improved API discoverability for schedules functionality.
- Increased documentation accuracy for consumers and contributors.
- Strengthened the developer experience around API reference and client generation workflows.

## Skills Demonstrated

- OpenAPI
- API Documentation
- TypeScript Ecosystem
- Documentation Engineering
- Review Iteration

## Key Learning

Accurate API documentation requires close alignment with real route behavior, validators, and error contracts rather than relying only on high-level endpoint intent.
