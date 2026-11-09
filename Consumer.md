Q. What is a Kafka Consumer?
>>A Kafka Consumer is an application that reads and processes messages from Kafka topics.

>It subscribes to topics, consumes records, tracks offsets to maintain progress, and can be part of a consumer group for parallel message processing and scalability.

Q. What is a Consumer Group?
>>A Consumer Group is a collection of consumers that work together to consume messages from a Kafka topic. Kafka distributes the topic's partitions among the consumers in the group, allowing messages to be processed in parallel and improving scalability and throughput. 

>Within a consumer group, a partition can be assigned to only one consumer at a time, ensuring that messages are not processed multiple times by the same group.

Q. What happens when there are more consumers than partitions?
>>If there are more consumers than partitions in a consumer group, the extra consumers remain idle because Kafka assigns each partition to only one consumer within the group.

>The maximum level of parallelism is limited by the number of partitions. Therefore, to fully utilize more consumers, the topic must have at least the same number of partitions as the consumers.

Q. What is Consumer Rebalancing?
>>Consumer Rebalancing is the process in Kafka where partitions are automatically redistributed among consumers within a consumer group whenever a consumer joins, leaves, fails, or when the partition count changes. During rebalancing, Kafka temporarily pauses consumption, reassigns partitions, and then resumes processing.

>Rebalancing ensures load balancing, scalability, and fault tolerance within the consumer group.

Q. What is Consumer Lag?
>>Consumer Lag is the difference between the latest offset in a Kafka partition and the offset that a consumer group has successfully processed. It represents the number of messages that are yet to be consumed. 

>Consumer lag is an important metric for monitoring consumer performance and identifying bottlenecks. A high lag indicates that consumers are unable to process messages as fast as they are being produced.

Q. Explain how to monitor consumer lag?
>>Consumer Lag is monitored by comparing the consumer group's committed offset with the latest offset available in Kafka. 

>The most common way to check lag is using the kafka-consumer-groups --describe command, which shows the current offset, log-end offset, and lag for each partition.

>In production environments, tools such as Prometheus, Grafana, Confluent Control Center, and Burrow are commonly used to track consumer lag and generate alerts when consumers fall behind message production.

Q. What Happens if a Consumer Fails in Kafka?
>>If a consumer fails, Kafka detects the failure through missing heartbeats and triggers a consumer rebalance. During rebalancing, the partitions assigned to the failed consumer are redistributed among the remaining active consumers in the group. 

>The new consumer resumes processing from the last committed offset, ensuring fault tolerance and minimizing message loss.
