# RabbitMQ vs Kafka

## RabbitMQ
- **Nickname**
  - Message Broker
  - In-Memory Message Broker
  - Message Queuing System
  - Traditional Message Queue
  - Message Queue Model-Based

- **Protocols**
  - **AMQP (Advanced Message Queuing Protocol)**: The primary protocol RabbitMQ is built on.
  - **MQTT (Message Queuing Telemetry Transport)**: A lightweight messaging protocol designed for low-bandwidth and IoT applications.
  - **STOMP (Simple/Streaming Text Oriented Messaging Protocol)**: A simple text-based protocol often used for integrating RabbitMQ with web applications.
  - **HTTP**: RabbitMQ offers an HTTP API for publishing and managing messages, making it accessible to web applications.
  - **WebSocket**: Enables bi-directional real-time messaging between web clients and RabbitMQ, suitable for real-time dashboards or chat systems.

- **Save Data**
  - **Queue**
    - RabbitMQ uses a **smart broker, dumb consumer** model:
      - Messages are stored in queues and deleted after being acknowledged by the consumer.
    - Messages are kept in memory for faster performance but can also be persisted to disk for reliability.
    - RabbitMQ uses **Work Queues** to distribute messages among multiple consumers, balancing the workload.
    - Producers can send messages to specific queues or broadcast them to multiple queues using exchanges and routing keys.
    - **Priority queues** and **TTL (Time-To-Live)** features allow fine-grained control over message delivery.
    - Messages remain in the queue until consumed and acknowledged, ensuring reliability.

- **How to Process Messages**
  1. **Producer sends a message to an Exchange**:
     - Producers send messages to an exchange, which determines where the message should go.
     - Types of exchanges include:
       - **Direct Exchange**: Routes messages to queues matching a routing key.
       - **Fanout Exchange**: Broadcasts messages to all bound queues.
       - **Topic Exchange**: Routes messages based on wildcard patterns in routing keys.
       - **Header Exchange**: Routes messages based on headers rather than routing keys.
  2. **Exchange routes the message to Queues**:
     - Based on the type of exchange and binding rules, messages are routed to one or more queues.
  3. **Broker stores the message in the Queue**:
     - Messages are stored temporarily until consumed. While stored, they are hidden from other consumers until acknowledged.
  4. **Consumer retrieves and processes the message**:
     - Consumers subscribe to queues, receive messages, and process them in real time using RabbitMQ’s push-based delivery.
  5. **Consumer acknowledges the message**:
     - After successful processing, the consumer sends an acknowledgment (`ACK`) to the broker.
     - If the acknowledgment is not received within a configured timeout, the message is re-delivered to the same or another consumer.
  6. **Message deletion**:
     - Once the broker receives an acknowledgment, it deletes the message from the queue.
     - Unacknowledged messages remain in the queue and are re-delivered.

- **Examples of Usage**
  - Task distribution
  - Real-time notifications
  - Event-driven microservices
  - Reliable messaging for moderate workloads

---

## Kafka
- **Nickname**
  - Event Broker
  - Log-Based Message Broker
  - Streaming Processing System
  - Distributed Streaming Platform
  - Publish-Subscribe Model-Based

- **Protocols**
  - **Kafka's Proprietary Protocol**: A custom TCP-based protocol optimized for high throughput and low latency.
  - **HTTP/REST**: Tools like Confluent REST Proxy provide HTTP-based integration for Kafka, making it accessible to RESTful clients.
  - **gRPC**: Supported through extensions or third-party libraries, allowing high-performance communication.
  - **WebSocket**: Connectors enable real-time WebSocket streaming.

- **Save Data**
  - **Log**
    - Kafka uses a **dumb broker, smart consumer** model:
      - Messages are stored in an append-only log and not deleted after consumption.
      - Retention policies control how long or how much data is kept:
        - **Time-based Retention**: Deletes messages older than a configured time.
        - **Size-based Retention**: Deletes older messages when the log exceeds a size limit.
    - Consumers track offsets, allowing message replay or resumption from a failure.
    - Topics are divided into **partitions**, allowing for parallelism and scalability.

- **How to Process Messages**
  1. **Producer sends a message to a Topic**:
     - Producers send messages to topics, which are logical categories for messages.
     - Messages are distributed across partitions based on a key or in a round-robin manner.
  2. **Broker stores the message in a Partition Log**:
     - Messages are appended to the log in the appropriate partition.
     - Each message is assigned an offset for easy tracking.
  3. **Consumers subscribe to the Topic**:
     - Consumers join a **Consumer Group** and subscribe to topics.
     - Kafka assigns partitions to consumers in the same group to ensure each partition is processed by only one consumer in the group.
  4. **Consumers poll messages from the Broker**:
     - Consumers fetch messages by requesting specific offsets, enabling them to replay or resume processing as needed.
  5. **Message retention and deletion**:
     - Messages are retained on disk even after consumption. Deletion is controlled by:
       - **Time-based Retention**: Configured duration for message retention (e.g., 7 days).
       - **Size-based Retention**: Configured maximum size of a partition log, beyond which older messages are deleted.
       - **Compaction**: Optionally keeps only the latest version of messages with the same key.

- **Examples of Usage**
  - Real-time data streaming (e.g., log aggregation, metrics collection)
  - Event sourcing in microservices
  - High-throughput data pipelines
  - Streaming ETL (Extract, Transform, Load)

---

### Key Differences

| Feature                  | RabbitMQ                                   | Kafka                                      |
|--------------------------|--------------------------------------------|-------------------------------------------|
| **Model**                | Message Queuing                           | Publish-Subscribe, Event Streaming         |
| **Message Storage**      | Memory (default), optional persistence    | Disk-based append-only log                |
| **Message Deletion**     | Deleted after acknowledgment              | Retained until retention policy triggers   |
| **Clustering**           | Complex to manage                         | Built-in support for distributed systems  |
| **Message Routing**      | Flexible exchanges and routing keys       | Partition-based routing                   |
| **Throughput**           | Moderate                                 | Very high (optimized for streaming)       |
| **Replayability**        | Not supported (default)                   | Supported via offsets                     |
| **Protocols**            | AMQP, MQTT, STOMP, HTTP, WebSocket        | Kafka Protocol, REST, gRPC, WebSocket     |
| **Typical Use Cases**    | Task distribution, notifications          | Real-time streaming, data pipelines       |

---

### Summary
RabbitMQ provides reliable message queuing with strong support for multiple protocols, complex routing, and fine-grained message control. Kafka, on the other hand, is optimized for distributed environments, supporting high-throughput, fault-tolerant real-time data pipelines with message replay and retention policies.




---
## Additional Information

### 1. **RabbitMQ and SQS Similarity**

Yes, RabbitMQ behaves similarly to AWS SQS in terms of message visibility. When a **Consumer** retrieves a message, the **Broker** hides the message from other Consumers until it receives an acknowledgment (`ACK`). If no `ACK` is received within a configured time limit, the message becomes visible again and can be re-delivered, potentially to a different Consumer.

| **Feature**           | **RabbitMQ**                                  | **AWS SQS**                                  |
|------------------------|-----------------------------------------------|----------------------------------------------|
| **Message Visibility** | Messages are hidden until acknowledgment.    | Messages are hidden for the visibility timeout. |
| **Re-delivery**        | Unacknowledged messages are re-delivered.    | Messages reappear after the visibility timeout. |

**Follow-up Questions**:
- **Is RabbitMQ like TCP where the Broker sends messages to Consumers (push-based)?**
  - Yes, RabbitMQ operates in a **push-based** manner. The Broker maintains a persistent TCP connection with Consumers via AMQP channels, enabling it to push messages to subscribed Consumers in real time. This can be thought of as a publish/subscribe model where the Broker actively delivers messages to Consumers.

- **What happens if an `ACK` is not received?**
  - If an `ACK` is not received within a defined timeout, RabbitMQ re-delivers the message to the same or another available Consumer. This ensures message delivery but can lead to duplicate processing if the original Consumer partially processed the message before the timeout.

---

### 2. **RabbitMQ Consumer Polling**

RabbitMQ does **not require Consumers to poll** for messages repeatedly. Instead, RabbitMQ **pushes messages** to Consumers over an AMQP channel, which keeps a persistent TCP connection open. This behavior achieves real-time message delivery without the need for webhook-style callbacks or active polling.

---

### 3. **RabbitMQ Clustering and Broadcasting**

RabbitMQ supports clustering but doesn’t natively distribute a single message across multiple queues on different nodes. Instead:
- Each message is routed to a queue bound to an exchange on a specific node.
- If clustering is enabled, metadata and queue definitions are synchronized across nodes, but the actual messages are stored on a single node.
- To broadcast messages across multiple clusters or nodes, **Federation** or **Shovel** plugins are required.

**Follow-up Question**:
- **Does clustering mean a single message is stored in only one queue?**
  - Yes, RabbitMQ ensures that a single message resides in one queue and is not duplicated across multiple queues, even in a clustered setup.

---

### 4. **Does RabbitMQ Have Topics?**

RabbitMQ does not have a "topic" concept similar to Kafka but provides **Topic Exchanges**. A Topic Exchange routes messages to queues based on routing keys and wildcard patterns:
- Example: Routing keys like `order.created` can be matched by a queue with a binding pattern such as `order.*`.
- This allows for flexible message routing but lacks Kafka’s robust Topic-Partition model, where messages are directly tied to partitions within a topic.

---

### 5. **Kafka Message Retention**

Kafka retains messages on disk regardless of whether they have been consumed. Messages are deleted based on **retention policies**:
1. **Time-based Retention**: Messages older than a configured time (e.g., 7 days) are deleted.
2. **Size-based Retention**: When the total log size exceeds a configured limit, older messages are deleted.

Kafka does not have a TTL mechanism for individual messages. Instead:
- Retention policies apply at the Topic level.
- Data can also be compacted to retain only the most recent record for a given key.

**Follow-up Question**:
- **What happens to accumulated data, and is additional logic required?**
  - Retained data is managed by Kafka automatically via retention policies, so no additional logic is needed. However, for use cases like data archival, you can implement custom connectors to offload older data to external storage systems like HDFS or Amazon S3.

---

### 6. **Kafka Topic and Partition**

Kafka distinguishes between **Topics** and **Partitions**:
- **Topics**: Logical channels that group messages. Each Kafka instance can manage multiple topics, and each topic can span across partitions for scalability.
- **Partitions**: Subdivisions of a topic where messages are stored. Messages within a partition are ordered, but there is no ordering guarantee across partitions.
  
**Message Routing**:
- Producers send messages to topics, and Kafka determines which partition to store the message in.
- Partitioning can be based on:
  - A **key**: Ensures messages with the same key go to the same partition.
  - **Round-robin**: Distributes messages evenly across partitions.
  
**Follow-up Questions**:
- **Is a message routed to a topic first, then partitioned?**
  - Yes, messages are sent to a topic first, and Kafka then determines the appropriate partition using the producer's configuration.
  
- **Is there one topic per Kafka instance?**
  - No, a single Kafka instance can handle multiple topics. Each topic can have its own partitions, which are distributed across the Kafka cluster.

- **How are messages distributed within partitions?**
  - Messages are distributed based on the producer's configuration:
    - **Keyed Messages**: Messages with the same key are hashed and sent to the same partition.
    - **Unkeyed Messages**: Distributed evenly across partitions using round-robin.