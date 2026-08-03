# Microservices Architecture

## Migrating to Microservices

1. Cohesion- Elements that are tightly related together, change together should stay together.
2. Single Responsibility Principle- Each microservice should have a single duty and it should be exceptionally well in that
3. Loose Coupling-Little/No Interdependency, minimum communication with other microservices

## Decomposition

1. Business Capabilities
2. Domain/Sub-domain - Developer's understanding
3. Business Capabilities vs Sub-domain

## Patterns for Migration

1. Big Bang Approach - Refactoring of Monolith (Too many cooks in the kitchen)  
2. Hard to estimate effort of large and ambiguous projects
3. High risk of abandonment
4. No business activitys

### Incremental and Continuous development

1. Areas with most **development or frequent Changes** can benefit most from migration
2. Components with high scalability requirements
3. Least technical debt, good logic separation are one of the best candidates

### Preparing for Migration

1. Good code and test coverage
2. Clearly defined APIs
3. Removing Interdependency from rest of the system

## Stranger Fig Pattern

1. Strangler Facade in front of Monolith Application (API Gateway)
2. Once the microservice is deployed, tested and monitored after routing the traffic towards it through API Gateway, the obsolete monolith application is removed. Also, ensure that the application in concern should have good test coverage


## Databases in Microservices

1. 