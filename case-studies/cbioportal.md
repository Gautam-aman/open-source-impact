# cBioPortal Contribution

## Project
cBioPortal

## Pull Request
https://github.com/cBioPortal/cbioportal/pull/11910

## Title
Return 404 Instead of 500 for Missing Reference Genome Gene

## Problem

Requests for missing reference genome genes returned HTTP 500 instead of HTTP 404.

This exposed an internal server error for a valid client-side condition.

## Investigation

I traced the request flow and found missing null handling within the controller.

## Solution

- Added defensive null checks.
- Returned HTTP 404 when a gene does not exist.
- Preserved existing application behavior.

## Impact

- Improved API correctness.
- Enhanced user experience.
- Prevented unnecessary server exceptions.

## Skills Demonstrated

- Spring MVC
- REST APIs
- Exception Handling
- Defensive Programming

## Key Learning

Learned the importance of mapping domain conditions to appropriate HTTP status codes.