# InsForge Contribution

## Project
InsForge

## Pull Request
https://github.com/InsForge/InsForge/pull/1875

## Title
ci: SHA-pin tj-actions/changed-files

## Problem

The InsForge lint-and-format workflow depended on the floating `tj-actions/changed-files@v45` tag.

Using a moving tag can introduce supply-chain risk and make CI behavior less reproducible over time, especially for workflows that gate formatting and lint checks on changed files.

## Investigation

I reviewed the existing GitHub Actions workflow to confirm where `tj-actions/changed-files` was used and verified that the action version could be pinned to a specific commit SHA without changing the workflow logic.

## Solution

- Replaced the floating `tj-actions/changed-files@v45` reference with the pinned commit SHA `48d8f15b2aaa3d255ca5af3eba4870f807ce6b3c`.
- Kept the `# v45` inline comment to preserve readability and make the pinned release easy to identify.
- Applied the SHA pin consistently across both changed-files steps in the lint-and-format workflow.

## Impact

- Reduced CI supply-chain risk by removing the floating action tag.
- Improved workflow reproducibility for lint and formatting checks.
- Made the repository automation a bit easier to audit and maintain.

## Skills Demonstrated

- GitHub Actions
- CI/CD
- Supply Chain Security
- YAML

## Key Learning

Pinning third-party workflow actions by commit SHA is a small change that materially improves reproducibility and trust in CI pipelines.
