Q. Difference between At-Most-Once, At-Least-Once, and Exactly-Once delivery?
>> At-Most-Once

>At-Most-Once is a message delivery guarantee in Kafka where a message is delivered at most one time. 

>This is typically achieved by committing the consumer offset before processing the message. 

>If the consumer crashes after committing the offset but before processing the message, the message is lost and will not be reprocessed. 

>Therefore, At-Most-Once guarantees no duplicate processing but may result in message loss.

>> At-Least-Once

>At-Least-Once is a Kafka delivery guarantee where every message is processed at least once.

>It is achieved by committing the offset only after successful message processing.

>If a consumer crashes before committing the offset, Kafka redelivers the message after restart. This prevents message loss but can result in duplicate processing. 

>Therefore, At-Least-Once provides high reliability and is the most commonly used delivery semantic in production systems.

>>Exactly-Once delivery

>Exactly-Once Delivery Semantics guarantees that each message is processed exactly one time, even in the presence of retries, broker failures, or consumer failures. 

>Kafka achieves this using Idempotent Producers and Transactions. 

>Idempotent producers prevent duplicate writes during retries, while transactions ensure that message production and offset commits occur atomically. As a result, messages are neither lost nor processed multiple times, making Exactly-Once the strongest delivery guarantee in Kafka.
