# OpenRewrite Contribution

## Project
OpenRewrite

## Pull Request
https://github.com/openrewrite/rewrite-spring/pull/885

## Title
Fix JdbcTemplateObjectArrayArgToVarArgs for Object[] Argument Reordering

## Problem

JdbcTemplate migration recipes did not consistently handle deprecated overloads that accepted Object[] arguments.

Certain query variants could produce incorrect transformations.

## Investigation

I reviewed recipe behavior and identified inconsistencies in Object[] argument handling across multiple JdbcTemplate methods.

## Solution

- Improved argument reordering logic.
- Preserved semantic correctness.
- Added support for additional query variants.

## Testing

Added test coverage for:

- query()
- queryForObject()
- queryForList()

Verified both transformation and no-change scenarios.

## Impact

- Improved migration accuracy.
- Reduced risk during Spring modernization.
- Increased confidence in automated refactoring.

## Skills Demonstrated

- Static Analysis
- Automated Refactoring
- Spring Framework
- Testing
- Java Tooling

## Key Learning

Learned how OpenRewrite performs large-scale source code transformations through recipe-based refactoring.