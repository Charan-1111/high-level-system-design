# Pub/Sub
- Publisher-Subscriber is a architectural pattern used to enable asynchronous communication between components in a distributed systems.
- Publishers can publish messages to a topic without needing to know who will consume them. Consumers can subscribe to a topic and consume messages without needing to know about the Publisher.
- ## Components of Pub/Sub
	- **Publishers** 
		- Publishers are the components or services that sends messages or events to a topic.
		- They generate data or events and publish these messages without worrying who will consume them.
	- **Subscriber**
		- Components or services that express interest in certain topics. They receive and process messages that are published to these topics.
	- **Message Broker**
		- Message Broker ( or message queue ) is the core component that manages topics, receives messages from publisher, and distributes them to all subscribers of these topics.
		- It acts as a intermediary to ensure that messages flow efficiently between publishers and subscribers.
- ## Working of Pub/Sub
	1. **Publishers send messages** - A Publisher creates a message and sends it to a specific topic on the message broker.
	2. **Message broker receives ad stores messages** - Broker receives the messages and temporarily stores it in the topic. Depending on the implementation, messages may be persisted to disk for durability.
	3. **Subscribers receive messages** - Subscribers that have subscribed to the topic receive the messages. This can happen in real-time or the subscriber may poll the broker if real-time delivery is not required.
	4. **Processing and Acknowledgment** - Subscribers process the message. In some systems, the subscriber sends the acknowledgment back to the broker to confirm that the message has been processed successfully.

- [ ] Read about the benefits of pub/sub and use cases
