# Queue

- Market Rates (messages) --> Queues --> Computing Cloud(mathematical model to calculate recommendations) --> Queues --> Clients (buy/sell recommendation)
- Single Data Responsibility Principle (System Component Reliability)

## Use cases of Queues

- Decompose two systems (Integrate systems with two different technologies)

- Estimate desired performance( You can speed up or throttle based on the traffic load)

- Persistent Queues( Single Data Responsibility Principle): Fault Tolerance

- Increases loose coupling among services and scaling (Horizontal Scaling and loose coupling)

- Increase system inbound queue: (Asynchronous Messaging)

- Buffer System outbound bytes( Video Streaming, Payperview data streaming, notification)

# RabbitMQ (Supports Advanced Messaging Queue Protocol(AMQP))

- Supports Plugins for **STOMP** (Streaming Text Oriented Messaging Protocol) and **MQTT**(Messaging Queue Telemetry Transport).

- Written in Erlang(Functional Language): Lightweight, Can be started fast and operate in isolation and scheduled by Erlang Virtual Machine.

- Kafka-Message bus with a typical implementation of log data and where as RabbitMQ is a message Broker.  
- Kafka can store data for n number of hours while message replay is not allowed in RabbitMQ

- RabbitMQ pushes message to the consumer while Kafka has to pull the messages from the RabbitMQ.

- Kafka Kinesis don't support so many acknowledgements, routing patterns and data safety features.  

| Kafka | RabbitMQ |
| --- | --- |
| Consumers are distributed as per Kafka Topic Partitions. Many consumers per queue and can consume the messages. | Many consumers per queue. Messages can be consumed only once. | 
| Highly Available but Zookeeper/Kraft is needed to maintain it | Highly Available |
|Queues are replicated by design | Queues are not replicated by design |
| Binary Serialized data | STOMP, AMQP, MQTT and HTTP |
| Logs | Queues |
| Basic | Sophisticated |
| Message is sent to topic by key | Very flexible | 

- AMQP operates on Application layer(OSI Model) work with many applications

## OSI MODEL

| OSI Model | TCP/IP Layer |
|---|---|
|Application layer | Appliation |
|Presentation layer | Application |
|Session layer | Application & Transport |
| Network | Network |
| Data Link | Network Interface |
| Physical | Network Interface |

## AMQP Message Structure 

- Header : Metadata ( Key/Value pairs) ( As per AMQP Specification )

- Properties: Metadata ( Key/Value pairs ), Application-Specific Information holder

- Payload: ( Message content -> In bytes, Max limit is 2 GB)



