# InsForge Contribution

## Project
InsForge

## Pull Request
https://github.com/InsForge/InsForge/pull/1827

## Title
Document S3 Proxy Mode Upload and Download Strategies

## Problem

The storage OpenAPI specification did not fully reflect runtime behavior for S3 proxy mode when `S3_USE_PRESIGNED_URLS=false`.

That ambiguity could cause API consumers to infer upload and download behavior from the storage backend instead of the response contract.

## Investigation

I reviewed the storage API contract and aligned the documentation with the actual strategy responses, especially around the returned `method` field, proxy-mode downloads, and upload confirmation behavior.

## Solution

- Clarified how upload strategy changes based on storage backend and `S3_USE_PRESIGNED_URLS`.
- Documented that clients should use the returned `method` field to choose upload and download behavior.
- Added an S3 proxy-mode upload example and clarified the `confirmRequired` / `confirmUrl` contract.

## Impact

- Improved API contract accuracy for storage consumers.
- Reduced integration ambiguity around S3 proxy mode.
- Strengthened developer experience for teams building against InsForge storage APIs.

## Skills Demonstrated

- OpenAPI
- API Documentation
- Storage APIs
- TypeScript Ecosystem
- Documentation Engineering

## Key Learning

Good API documentation needs to describe behavioral contracts precisely enough that clients can make correct decisions without relying on implementation assumptions.
