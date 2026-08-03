# Armeria (LINE) Contribution

## Project
Armeria — LINE's open-source HTTP/RPC microservice framework (Java)

## Pull Request
https://github.com/line/armeria/pull/6860

## Title
Fix IDN Normalization for Authorities with Ports

## Problem

`IDN.toASCII()` was applied to the entire authority string (e.g., `longhost.example.com:8080`) before host/port parsing.

For authorities containing a long internationalized hostname and a port, this caused `IDN.toASCII()` to fail because the combined host+port string exceeded the per-label or overall length limits enforced by the IDN standard, even though the hostname alone was perfectly valid.

This was tracked as issue #6859.

## Investigation

I reproduced the bug by constructing a long IDN hostname combined with a port and confirmed that `IDN.toASCII()` threw when applied to the full authority string. Reading the Java IDN specification confirmed that normalization must be applied per-hostname, not to a host:port combination.

## Solution

- Refactored the authority normalization flow to split the port from the authority string first.
- Applied `IDN.toASCII()` only to the extracted host portion.
- Reconstructed the full authority string from the normalized host and the original port after normalization.
- Added test cases for long IDN hostnames with various port combinations to prevent regressions.

## Impact

- Fixed request failures for clients using long internationalized hostnames combined with explicit ports.
- Hardened the IDN normalization path in Armeria's authority parsing to be spec-compliant.
- Improved reliability for internationalized deployments using Armeria as their HTTP client.

## Skills Demonstrated

- Java
- Armeria Framework
- HTTP Networking
- IDN (Internationalized Domain Names)
- URI Parsing
- Unit Testing

## Key Learning

Normalization functions that operate on composite strings (like host:port) need to be aware of format constraints. Always decompose composite strings before applying format-sensitive transformations to their parts.
