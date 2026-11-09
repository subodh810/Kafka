Q. What is an Offset?
>>Offset is a unique sequential identifier assigned to each message within a Kafka partition. It represents the position of a message in that partition. 

>Kafka uses offsets to track which messages have been consumed by a consumer. By storing offsets, consumers can resume processing from the correct position after a restart, avoid data loss, and even replay messages when required. Offsets are unique only within a partition, not across the entire topic.

Q. What is Auto Commit?
>>Auto Commit is a Kafka consumer feature in which offsets are automatically committed at fixed intervals, that is controlled by the enable.auto.commit and auto.commit.interval.ms properties. 

>It reduces development effort because Kafka manages offset tracking automatically. However, if a consumer crashes after an offset is committed but before processing the message, data loss can occur.<br>Therefore, for critical applications, Manual Offset Commit is generally preferred to ensure reliable message processing.

Q. What is Manual Commit?
>>Manual Commit is a Kafka offset management mechanism in which the consumer explicitly commits offsets after successfully processing messages.

>It is enabled by setting enable.auto.commit=false. This gives developers full control over when offsets are stored, helping prevent message loss and ensuring reliable processing. 

>Manual commits can be performed synchronously using commitSync() or asynchronously using commitAsync().

>Therefore, Manual Commit is generally preferred in production systems where data consistency and reliability are critical.

Q. Why is Manual Commit preferred in production?
>>Manual Commit is preferred in production because offsets are committed only after successful message processing. This reduces the risk of data loss and provides better control over failure handling, retries, and message delivery guarantees compared to Auto Commit.


Q. What happens if offset is committed before processing?
>>If an offset is committed before the message is processed, Kafka assumes the message has been successfully handled. 

>If the consumer crashes before completing the processing, Kafka will start from the next committed offset after restart, causing the unprocessed message to be skipped and resulting in message loss. 

>Therefore, in production systems, offsets should be committed only after successful message processing.
