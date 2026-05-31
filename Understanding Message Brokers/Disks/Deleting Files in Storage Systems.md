So, the journal contains all the messages. When certain message has to be deleted (for instance, in the case of message broker, the message consumed by consumers), instead of deleting the message from the journal directly, there is acknowledgement written in the journal pointing towards the messages that needs to be deleted (uses pointer) and the [[#Index]] is incremented. Later on when the whole section on the journal is consumed, then the whole section is deleted at once. The drawbacks is, if not all messages are consumed, it stays on disks forever which is why setting expiration in messages helps. 

This same logic is implemented in other storage system like Kafka, LevelDB, RocksDB, Cassandra's SSTables, and even filesystems like ZFS.

### Index
A separate data structure (a B-Tree) that tracks the current state — which messages exist, where they are in the journal, which have been acknowledged.