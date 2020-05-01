# Kafka	
#kafka #may2020 #posted

---
### Test

```
// Changing Terminal Title on Mac
$ echo -n -e "\033]0;ZOOKEEPER\007"

// Step: 1.	Apache Kafka depends on Zookeeper for cluster management.
$ ~/app/kafka_2.13-2.4.0/bin/zookeeper-server-start.sh ~/app/kafka_2.13-2.4.0/config/zookeeper.properties

// Step: 2.	Start Kafka server.
$ ~/app/kafka_2.13-2.4.0/bin/kafka-server-start.sh ~/app/kafka_2.13-2.4.0/config/server.properties

// Step: 3.	Create Kafka topics.
$ ~/app/kafka_2.13-2.4.0/bin/kafka-topics.sh --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic helloworld-topic
Created topic helloworld-topic.

// Step: 4.	Describe topic.
$ ~/app/kafka_2.13-2.4.0/bin/kafka-topics.sh --describe --zookeeper localhost:2181 --topic helloworld-topic
Topic: helloworld-topic	PartitionCount: 1	ReplicationFactor: 1	Configs: 
	Topic: helloworld-topic	Partition: 0	Leader: 0	Replicas: 0	Isr: 0


// Step: 5.	Creating producer.
$ ~/app/kafka_2.13-2.4.0/bin/kafka-console-producer.sh --broker-list localhost:9092 --topic helloworld-topic
>hello world!!!
>

// Step: 6.	Create consumer.
$ ~/app/kafka_2.13-2.4.0/bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic helloworld-topic --from-beginning
hello world!!!


$ ~/app/kafka_2.13-2.4.0/bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 \
    --topic helloworld-topic \
    --from-beginning \
    --formatter kafka.tools.DefaultMessageFormatter \
    --property print.key=true \
    --property print.value=true \
    --property key.deserializer=org.apache.kafka.common.serialization.StringDeserializer \
    --property value.deserializer= org.apache.kafka.common.serialization.StringDeserializer

```


### Installation

- Download Kafka [2.4.0]:  [https://kafka.apache.org/downloads](https://kafka.apache.org/downloads) 
- [https://www.apache.org/dyn/closer.cgi?path=/kafka/2.4.0/kafka_2.13-2.4.0.tgz](https://www.apache.org/dyn/closer.cgi?path=/kafka/2.4.0/kafka_2.13-2.4.0.tgz) 
- Kafka – Install Apache Kafka on Mac [  [https://www.tutorialkart.com/apache-kafka/install-apache-kafka-on-mac/](https://www.tutorialkart.com/apache-kafka/install-apache-kafka-on-mac/)  ]
