Q. What is a Kafka Producer?
>>A Kafka Producer is a client application that publishes messages to Kafka topics. 

>It is responsible for creating events and sending them to Kafka. 

>Producers can send messages with or without keys, and Kafka uses these keys to determine the target partition. Producers communicate with Kafka brokers and receive acknowledgments to ensure reliable message delivery

>If a Kafka producer sends messages without a key, Kafka uses its default partitioner to distribute messages across available partitions, typically using a sticky partitioning strategy for better batching and throughput. In this case, messages may go to different partitions, so ordering is guaranteed only within each partition. If message ordering is important, a key should be provided so that related messages are always routed to the same partition

Q. How does Kafka decide the partition for a message?
>>Kafka decides the target partition based on whether a key is provided or not.

>Kafka determines the partition using the message key. When a key is provided, Kafka applies a hash function on the key and calculates hash(key) % number_of_partitions to select the partition. This ensures all messages with the same key are routed to the same partition and their order is preserved. 

>If no key is provided, Kafka uses its default partitioner (Sticky Partitioner) to distribute messages across partitions for better load balancing and throughput.

Q. What is the role of a Message Key?
>>A Message Key in Kafka is used to determine the target partition for a message.

>Kafka applies a hash function on the key and routes all messages with the same key to the same partition.

>This ensures that related messages are processed in order and helps maintain data consistency. Without a key, Kafka distributes messages across partitions using its default partitioning strategy

Q. What are Producer Acknowledgements (acks)?
>>Producer Acknowledgements (acks) determine the level of confirmation a Kafka producer requires before considering a message successfully sent.

>With acks=0, the producer does not wait for any acknowledgment. With acks=1, it waits for confirmation from the leader broker.

>With acks=all (or -1), it waits until the leader and all in-sync replicas have stored the message. Higher acknowledgment levels provide greater reliability but may reduce performance.

Q. What is an Idempotent Producer?
>>An Idempotent Producer is a Kafka producer feature that ensures a message is written only once, even if the producer retries sending the same message due to network issues, broker failures, or timeouts.

>When idempotence is enabled, Kafka uses :- Producer ID (PID) & Sequence Numbers.<br>

>spring.kafka.producer.properties.enable.idempotence=true

>An Idempotent Producer is a Kafka producer configuration that guarantees a message is written to Kafka only once, even if retries occur due to network failures or broker issues. Kafka achieves this by enabling using enable.idempotence=true, & assigning a Producer ID and sequence numbers to messages, allowing brokers to detect and discard duplicate records. This improves reliability and helps provide exactly-once delivery semantics on the producer side.
