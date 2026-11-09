Q. What is Kafka and why is it used?
>>Apache Kafka is a distributed event-streaming platform used for building real-time data pipelines and event-driven applications. 

>It acts as a highly scalable, fault-tolerant, and durable messaging system where producers publish messages to topics and consumers subscribe to those topics. 

>Kafka is widely used for microservice communication, real-time analytics, log aggregation, transaction processing, and event streaming because it provides high throughput, horizontal scalability, message persistence, and fault tolerance


Q. What is the difference between Kafka and RabbitMQ?
>>Kafka is a distributed event-streaming platform designed for high-throughput, scalable, and fault-tolerant data streaming, whereas RabbitMQ is a traditional message broker designed for reliable message delivery, routing, and complex messaging patterns. Kafka is generally preferred for handling massive event streams and real-time data pipelines, while RabbitMQ is better suited for task queues, request-reply communication, and complex routing requirements.


Q. What are Topics, Partitions, and Offsets?
>>Topic

>A Topic in Kafka is a logical channel or category used to store and organize messages. Producers publish messages to a topic, and consumers subscribe to that topic to read the messages. Topics help separate different types of data, such as orders, payments, and user events, and can be divided into partitions for scalability and parallel processing.

>>Partitions

>A Partition is a smaller part of a Kafka Topic. Kafka divides a topic into multiple partitions so that messages can be stored and processed in parallel. Partitions improve performance, scalability, and fault tolerance. Kafka also guarantees the order of messages within a partition.

>>Offsets

>An Offset is a unique sequence number assigned to each message within a Kafka partition. It represents the position of the message in that partition. Consumers use offsets to track which messages have been processed and to resume reading from the correct position in case of failures or restarts

Q. How does Kafka achieve high throughput?
>>High throughput means Kafka can handle and process millions of messages per second with very low latency

>Kafka achieves high throughput through partitioning, parallel processing, sequential disk writes, batch processing, zero-copy transfer, and consumer groups. By distributing data across partitions and allowing multiple consumers to process messages concurrently, Kafka can efficiently handle millions of events per second while maintaining scalability and reliability.

Q. Why is Kafka better than traditional messaging systems?
>>Kafka is better than traditional messaging systems because it provides very high throughput, horizontal scalability, fault tolerance, message retention, and event streaming capabilities. 

>Unlike traditional queues where messages are typically removed after consumption, Kafka stores messages for a configurable retention period and uses offsets to track consumer progress. 

>These features make Kafka an ideal choice for real-time data pipelines, microservices communication, and large-scale event-driven applications

Q. what is Broker?
>>A Broker is a Kafka server responsible for storing messages, managing topics and partitions, and serving producer and consumer requests. 

>A Kafka cluster typically consists of multiple brokers to provide scalability, fault tolerance, and high availability. Messages are distributed across brokers using partitions, and data replication ensures reliability in case of broker failures

>Broker = Kafka server that stores and manages messages

