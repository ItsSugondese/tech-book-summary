## Message
The message in ActiveMQ contains 2 properties i.e. Metadata and body. 

### Metadata
The metadata contains 2 properties i.e. headers and properties. 
#### Headers
The headers is set by JMS specification using which, the message can be accessed in API via JMSDestination and JMSTimestamp.

#### Properties
The Properties contains arbitrary (not enforced by any rules) piece of information which can give idea regarding what type of message is being sent without having to look into payload. For instance, message related to orders can be sent with the header orderId.

## Queue
Queue is responsible for  making sure message gets stored, routed and  also dispatching the message to consumer. The place where it doesn't play role is from producer to broker level which in most case is done my network call made by producer's thread.

### Body
It is the actual  content that the consumer wants. It can be in the form of TextMessage for strings and BytesMessage for binary data.
## Actors involved 
There are 4 actors.
1. Producer
2. Consumer
3. Broker
4. Storage

Producer is a client application which produces messages. When sending the message, the  Producer application thread gets triggered during .send(). In that thread, the message created by producer is added with the target destination set to queue. The message is sent to broker using network call made by thread. After the message is received by the broker, either a new queue is created or existing queue is used if avaiable based on the target destination queue sent in the message. The Queue is then responsible for making sure the message is stored in storage media and also letting broker know that the storing process was a success. After that broker sends ack to producer.

Consumer is the one receiving the message. When consumer express the demand for the message (mostly in the case of consumer being available), queue requests the message to the storage medium, put it in queue memory cache and is then responsible for routing and dispatching the message to the consumer. After dispatching, the consumer sends acks, using which the queue sends message to storage medium to delete the message.