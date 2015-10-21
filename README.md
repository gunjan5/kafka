# Kafka



## Basic setup (single broker)

- Download and unzip http://www.us.apache.org/dist/kafka/0.8.2.2/kafka_2.10-0.8.2.2.tgz
- Start ZooKeeper: `bin/zookeeper-server-start.sh config/zookeeper.properties`
- Start Kafka server: `bin/kafka-server-start.sh config/server.properties`
- Create a topic: `bin/kafka-topics.sh --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic test`
- List topics: `bin/kafka-topics.sh --list --zookeeper localhost:2181`
- Send some messages: ```bin/kafka-console-producer.sh --broker-list localhost:9092 --topic test 
                         Yello
                         World
                         how are yall doin```
- Start a consumer: `bin/kafka-console-consumer.sh --zookeeper localhost:2181 --topic test --from-beginning`