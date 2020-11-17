# MessageQueue

There are plenty of message queues and there are plenty of message message queue client libaries.
Some of them include:
[RabbitMQ](https://www.rabbitmq.com/), [Kafka](https://kafka.apache.org/), [AWS SQS](https://aws.amazon.com/sqs/).
and
[Rebus](https://github.com/rebus-org/Rebus), [Masstransit](https://masstransit-project.com/), [Nservicebus](https://particular.net/nservicebus)


## The queues

### RabbitMQ

![rabbit mq topic](rabbitmq.png)

![rabbit routing](rmq1.png)

![rabbit routing](rmq2.png)

![rabbit routing](rmq3.png)

### SQS

![queue](sqs.png)

![publish subscribe](sns.png)

### Kafka

Kafka doesn’t implement the notion of a queue. Instead, Kafka stores collections of records in categories called topics.

For each topic, Kafka maintains a partitioned log of messages. Each partition is an ordered, immutable sequence of records, where messages are continually appended.

Kafka appends messages to these partitions as they arrive. By default, it uses a round-robin partitioner to spread messages uniformly across partitions. (But can use keys to keep messages ordered)

Producers can modify this behavior to create logical streams of messages. For example, in a multitenant application, we might want to create logical message streams according to every message’s tenant ID. In an IoT scenario, we might want to have each producer’s identity map to a specific partition constantly. Making sure all messages from the same logical stream map to the same partition guarantees their delivery in order to consumers.

![kafka producers](kafka1.png)

Consumers consume messages by maintaining an offset (or index) to these partitions and reading them sequentially.

![kafka consumers](kafka2.png)

@LinkedIn

Problem:
![LinkedIn before](li1.png)

before vs after

![LinkedIn after](li2.png)

## Compare

![compare](comparequeue.png)

AWS SQS $$$ == Performance. Pay for what you need.




## Client libraries

There are ofcourse the native client libraries that can be used. In some cases it is actually best to use those. Other not. Eg. rabbitmq has alot of awesome routing features, that are entirely ignored by most 3rd party clients. On the other hand Kafka doesn't really have any 3rd party clients, because it's specialized nature.

### Rebus

#### Setup

![rebus](rebus.png)


#### Consumer 

When Rebus handles an incoming message, it constructs a handler pipeline. Why is that?

Well, first of all: Your IHandlerActivator may return multiple handler instances when asked to activate handlers for a particular message type. E.g. you might have two things happening upon receiving a CustomerMoved event:

![consumer](rebusconsumer.png)

![consumer](rebusconsumer2.png)

#### Producer

TODO

### Mass transit

#### Setup and Consumer

![masstransit](masstransit.png)

#### Producer

![masstransit producer](masstransitproducer.png)

### RabbitMQ Native

https://www.rabbitmq.com/tutorials/tutorial-one-dotnet.html

### SQS Native

https://docs.aws.amazon.com/sdk-for-net/v3/developer-guide/sqs-apis-intro.html

### Kafka - Confluent kafka client

https://github.com/gabrielsadaka/dotnet-kafka-sample

Really awesome unknown example




sources:
https://medium.com/better-programming/rabbitmq-vs-kafka-1ef22a041793

https://www.confluent.io/blog/kafka-fastest-messaging-system/

https://eng.uber.com/reliable-reprocessing/

https://engineering.linkedin.com/distributed-systems/log-what-every-software-engineer-should-know-about-real-time-datas-unifying