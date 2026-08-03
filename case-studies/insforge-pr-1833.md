# InsForge Contribution

## Project
InsForge

## Pull Request
https://github.com/InsForge/InsForge/pull/1833

## Title
fix(dashboard): Include Cron Schedule in Schedule Search

## Problem

The schedule search logic in the dashboard checked `functionUrl` twice instead of checking both `functionUrl` and `cronSchedule`.

This meant users could search for schedules by their function URL but not by their cron schedule expression, silently excluding valid results and confusing users who expected schedule-type queries to work.

## Investigation

I traced the search predicate chain in the dashboard's schedule filtering logic and confirmed the duplicated `functionUrl` check was causing cron schedule searches to always miss, regardless of input.

## Solution

- Replaced the second duplicated `functionUrl` predicate with the correct `cronSchedule` predicate.
- Ensured that schedule search now fans out across both `functionUrl` and `cronSchedule` fields.
- Verified the fix restores expected search behavior for cron-based schedule queries.

## Impact

- Restored cron schedule searchability in the dashboard UI.
- Eliminated user confusion caused by silent search misses on valid schedule entries.
- Improved dashboard data discoverability for operations teams.

## Skills Demonstrated

- TypeScript
- React
- Frontend Bug Fixing
- Dashboard Logic
- Predicate / Filter Correctness

## Key Learning

Duplicated field checks in compound search predicates can silently exclude entire categories of valid results. Always verify that each distinct query dimension maps to a distinct and correct field.
