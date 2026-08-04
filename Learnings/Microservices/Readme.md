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

1. Database per microservice: Decoupling the data from other services, explicit maintenance in the particular microservice.

2. To access the database from each other, we use API. If we are changing the schema, we can offer two versions of the API (v1 and v2) for months, so that other teams get enough time to retrofit their API.  

3. Downside:
    - Latency and Performance Overhead
    - No more "join" operation. We have to pull data as an object and then do join programmatically.
    - Loss of transactions.

## DRY (Don't Repeat Yourself)

1. Sometimes, lead to tight-coupling
2. Every change requires
    - Rebuild
    - Retest
    - Redeploy

3. Bug/Vulnerability in a shared library impacts all microservices
4. Dependency Hell
    - Missing or incompatible library or the two libraries requiring different versions of the same dependency during build-time
    - Increases the size of binary

5. To solve it (Dependency Hell):  
    - Shared library
    - Code generation tool (Interfaces, gRPC , Data Schema)

### Duplication Options

1. The utility code that changes frequently can be duplicated so that each microservice will have its own implementation

### No duplication

1. Sidecar Pattern: We run this as a helper process on same microservice instance

2. Communication overhead is smaller as compared to other services/hosts, but still higher if we ran it using shared library.  

3. Shared library: Self-contained/independent if we want a utility of logging, retrying or pattern-matching.  

## Duplicating Data

1. Only one microservice should be owner. One owner should have Write/Update/Delete operation, while the cache at one of the microservice will only read it.

2. When we need to ensure *Eventual Consistency* .

## Structured Autonomy

1. Tier-1: Fully Restrictive
    - Monitoring and Alerting
    - CI/CD

2. API Guidelines and Best practices

3. Security and data compliance

- Tier-2  Freedom with Boundaries (Programming Languages, Database technologies)

- Tier-3 Complete Autonomy

## Microfrontends

1. All the bundles of Microfrontend are loaded at the runtime on the Container Application.

2. Render common elements, Common Functionality and when and where the MFAs should be reloaded.

3. Loaded at Runtime

4. Don't share state with each other

5. They communicate through Custom Events, Passing Callback or using BRowser Address bar.

## API Management

- **Problems**

1. Tight coupling of API-Client Side code to the services

2. Different types of API for different type of consumers

3. Different API tiers based on subscription level

- **Solutions**

1. API Gateway for routing purposes, traffic management and throttling.  

2. Authorization and TLS termination

3. Analyze the behaviour of API for different clients making requests to the different microservices and aggragating the results before sending it to clients.

4. Decouples client from the services, especially important from IoT devices and mobile phones because these features affect their battery life as well.

## Difference 

| Load-Balancer | API Gateway |
| --- | --- |
| LB sits in front of a microservice( Different instances of same microservice) | While API Gateway routes traffic not to servers but to services|
| Little performance overhead, Health Checks, Different routing algorithm | Throttling, Monitoring, API versioning and management, Protocol/Data translation |

## Event-Driven Architecture

1. Video-On-Demand: Subscription Request ->Payment request->Recommendation Service and the chain of communication goes through API Gateway

2. Latency issues


### Event

1. Fact, Action and State Change

2. Always immutable

3. Can be stored indefinitely

4. Can be consumed multiple times by different services

- Producer producing events, message broker routing it to consumers

## Event Streaming

- Message Broker works like log. Each consumer has access to the logs and they can replay it anytime from anywhere. 

- Reliable Delivery, Pattern/Anomaly Detection

- Pub/Sub: As soon as all subscriber receives the event, message broker deletes the message from its logs.

- New subscriber only gets notified to new events

### Pub/Sub

- Temporary Storage
- Fire and Forget
- Broadcasting
- Buffering
- Infinite Stream of Events
- Anomaly Detection and Pattern Recognition

## Delivery Semantics

- Issues with Delivery: Sender may have sent it or not sent it or not received any ack, consumer may or may not have received it or not sent any acks to the message broker.

### Atmost once

- Okay losing data, but avoid duplication(Ride Sharing app, Driver Service sharing location)
    1. Data loss is "OK"
    2. Least Overhead/Low latency

### Atleast once (Product Delivery Notification and Product Reviews)

- Data loss is unacceptable
- Data duplication is OK

Downsides

- Increased latency not ideal for high throughput systems due to duplication of records.

### Exactly Once Semantics
---

- Highest Latency/ Most difficult to achieve
- Check for idempotencyId (some messages generate it by themselves while other do it through a separate service)

- We push it to messageBroker, if it exists ok if not we send it again, just like atleast once semantics

- In the case of financial transactions, we will have to manually introduce idempotent Id so that if we ever update or create a new entry in DB through Message Broker, in order to prevent duplication if ack gets lost.

## Event Driven Architecture - Design Patterns

- SAGA
- CQRS
- Event Sourcing

### SAGA
---

- Distributed Transactions across different microservices because once we migrate to microservices, we lose ACID. 

- Sequence of Operations which should be succeeded, if anyone failse then it is rolled back through **Compensating Operation** .

- *Workflow Orchestration*: 
    1. User goes to webapp and steps are displayed to him/her.
    
    2. The request is routed from API gateway to Workflow Orchestration Service
    3. And when every operation in the workflow orchestration completed successfully then only the transaction would be successful, otherwise it would be rolled back and compensating operation would be applied.

- *Event-driven model*

    - Individual Microservices emit events to each of microservice in desired sequence.

    - In case of any one event in the sequence fails, they will perform compensating operation in the form of events being published as a compensating operation


### CQRS Pattern - Command and Query Responsibility Segregation
---

- Action that results in data change

- Only data read, no change(Show all products, filtering or sorting)

- Insert/Update/Delete goes through command service and Read goes through Query Service

- Supports SRP - Command Part supports permissions, input validation and business logic

- High Performance - For Command we can use Relational DB and for query we can rely upon read heavy db like NoSQL Database

- Separation of Concerns but for join operation we need to make two API calls while the answer is returned we do programmatic join

- So, we introduce a new *Query Service* between two Microservices and we connect them through *Message Broker*. So, whenever the data is modified/changed the event is published and is consumed by Query Service

- Eventual Consistency between Write and Read operation

- For example - Restaurant Service and Review Service, each submitting data to Message Broker and each getting collated to a new Service having *Read Text DB*  support.

### Event Sourcing Pattern

- Storage of not only the final states, but the steps also which led to it.  

- Separate DB for storage of events which led to the final state

- We store only changes/facts using events (ways to store it:- Databases and Message Broker)
- Introduction of Message Broker for *Write Contention*, messages go through Message Broker and then are handled otherwise database has high write contention and poor performance

- Strategies
    1. Replaying Events - **Snapshots**
    2. CQRS - For the Insert/Append operation, we can introduce a message broker, Query Service will subcribe to it and publish the data to In-memory DB.
    3. Advantages:  
     We get History and Auditing, fast and efficient writes and fast and efficient reads',
     Auditing, performant writes and Efficient Reads



Notes to care about: Eventual Consistency and Event Sourcing pattern

