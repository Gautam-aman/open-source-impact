# Spring Kafka Contribution

## Project
Spring Kafka

## Pull Request
https://github.com/spring-projects/spring-kafka/pull/4391

## Title
Ensure Non-String Override Properties Are Consistent

## Problem

DefaultKafkaConsumerFactory used Properties#stringPropertyNames() when merging override properties.

As a result, non-string values such as integers were ignored during property merging, causing inconsistent behavior.

## Investigation

I analyzed the property merge logic and found that only String-based properties were being copied while other valid property types were skipped.

## Solution

- Updated merge logic to iterate through all property entries.
- Preserved existing lifecycle behavior.
- Ensured non-string values are handled consistently.
- Added regression tests.

## Testing

Added tests covering:

- Integer override properties
- Mixed property types
- Existing consumer behavior

All tests passed successfully.

## Impact

- Fixed configuration inconsistencies.
- Prevented silent configuration loss.
- Improved framework reliability.

## Skills Demonstrated

- Spring Framework Internals
- Apache Kafka
- Java Collections
- Unit Testing
- Framework Development

## Key Learning

Learned how Spring Kafka manages consumer configuration and property merging internally.