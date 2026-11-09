Q. What is Replication Factor?
>>Replication Factor is the number of copies of a partition that Kafka maintains across different brokers. It provides fault tolerance and high availability by ensuring that if a broker containing the leader replica fails, one of the follower replicas can take over as the new leader.

>For example, a replication factor of 3 means Kafka stores one leader replica and two follower replicas for each partition. This helps prevent data loss and ensures continuous operation even during broker failures.

Q. Can the replication factor be greater than the number of brokers?
>>No. The replication factor cannot exceed the total number of available brokers because Kafka places each replica on a different broker. For example, if a Kafka cluster has 3 brokers, the maximum replication factor can be 3.

Q. What is Leader and Follower Replica?
>>Leader<br>
>A Leader Replica is the primary replica of a Kafka partition that handles all read and write requests from consumers and producers. 

>>Follower Replicas<br>
>Follower Replicas are backup copies that continuously replicate data from the leader to stay synchronized. 

>If the leader broker fails, Kafka automatically promotes one of the in-sync follower replicas to become the new leader, ensuring high availability and fault tolerance without data loss.

Q. Can producers and consumers communicate directly with follower replicas?
>>No. By default, producers send messages only to the leader replica, and consumers also read messages from the leader replica. Follower replicas are used only for replication and failover purposes.


Q. What is ISR (In-Sync Replica)?
>>ISR (In-Sync Replica) is the set of replicas for a Kafka partition that are fully synchronized with the leader replica.

>It includes the leader and all follower replicas that have replicated the latest data within the configured time limits. 

>Kafka uses the ISR for safe leader election and data consistency. If the leader fails, one of the replicas from the ISR is elected as the new leader to minimize the risk of data loss.

Q. Why does Kafka elect a leader only from the ISR?
>>Kafka elects a new leader from the ISR because replicas in the ISR contain the most up-to-date data. Choosing a leader from outside the ISR could result in missing messages and potential data loss. Therefore, selecting a leader from the ISR ensures better consistency and reliability.

Q. What happens when a Broker fails?
>>When a broker fails, Kafka detects the failure through broker heartbeats. 

>If the failed broker was hosting a leader replica, Kafka automatically elects a new leader from the available In-Sync Replicas (ISR).

>Producers and consumers are redirected to the new leader, ensuring continued availability. If the replication factor is greater than one and replicas are synchronized, Kafka can recover without data loss. If the failed broker was only a follower, Kafka continues operating normally and the follower rejoins the ISR after recovery.

Q. If the leader broker fails, how does Kafka choose the new leader?
>>Kafka elects a new leader from the In-Sync Replicas (ISR) because ISR members have the latest replicated data. This minimizes the risk of data loss and maintains consistency across the cluster.

Q. How does Kafka achieve Fault Tolerance?
>>Kafka achieves fault tolerance using partition replication across multiple brokers. 

>Each partition has one Leader and multiple Follower replicas. Followers continuously replicate data from the Leader and form the In-Sync Replica (ISR) set. If the Leader broker fails, Kafka automatically elects a new Leader from the ISR, ensuring high availability and consistency.

>Additionally, producer acknowledgements (acks=all) ensure messages are replicated across ISR members before being acknowledged, while offset management enables consumers to recover from failures and resume processing. 

>Together, these mechanisms allow Kafka to continue operating reliably even in the event of broker or consumer failures.
