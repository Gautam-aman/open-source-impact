# InsForge Contribution

## Project
InsForge

## Pull Request
https://github.com/InsForge/InsForge/pull/1858

## Title
feat(dashboard): Remove Direct GitHub Dependency from Dashboard Header

## Problem

The InsForge dashboard header made a direct browser-side call to the public GitHub API to fetch repository star counts for display. This created several risks:

- The GitHub API imposes strict unauthenticated rate limits (60 requests/hour per IP), making the star count display fragile for users behind shared NATs or in CI environments.
- Exposing a direct third-party API call from the frontend made the dashboard unnecessarily coupled to GitHub's API availability and response format.

## Investigation

I traced the GitHub API call to the dashboard header component and confirmed it was triggered on every page load with no caching or fallback. The issue (#1857) documented the rate-limit risk and proposed routing the call through the backend.

## Solution

- Added a backend endpoint that fetches and caches GitHub repository metadata (including star count) server-side.
- Updated the dashboard frontend to call the new internal endpoint instead of the GitHub API directly.
- Eliminated the unauthenticated client-side GitHub API dependency, reducing rate-limit exposure.

## Impact

- Removed the unauthenticated browser-side GitHub API dependency from the dashboard.
- Reduced rate-limit risk for all users by centralizing the GitHub API call on the backend.
- Improved dashboard resilience and decoupled the frontend from third-party API format changes.

## Skills Demonstrated

- TypeScript
- React
- Node.js Backend Development
- REST API Design
- Frontend/Backend Decoupling
- Third-Party API Management

## Key Learning

Direct browser-side calls to third-party APIs with rate limits should be proxied through a backend to centralize caching, authentication, and error handling. Frontend components should consume internal APIs, not external ones directly.
