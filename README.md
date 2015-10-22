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

## Multi-broker setup (3 nodes)

- Create/copy server config files: `bin/kafka-server-start.sh config/server-1.properties`
- Second broker: `bin/kafka-server-start.sh config/server-1=2.properties`
- Edit the config files with: 
	```bash
	config/server-1.properties:
	    broker.id=1
	    port=9093
	    log.dir=/tmp/kafka-logs-1
	 
	config/server-2.properties:
	    broker.id=2
	    port=9094
	    log.dir=/tmp/kafka-logs-2
	```

- Start Zookeeper: `bin/zookeeper-server-start.sh config/zookeeper.properties`
- Start all 3 brokers: 
	```bash
	 bin/kafka-server-start.sh config/server.properties &
	 bin/kafka-server-start.sh config/server-1.properties &
	 bin/kafka-server-start.sh config/server-2.properties &
	```
- Create a topic: `bin/kafka-topics.sh --create --zookeeper localhost:2181 --replication-factor 3 --partitions 1 --topic my-replicated-topic`
- Describe topic: `bin/kafka-topics.sh --describe --zookeeper localhost:2181 --topic my-replicated-topic`
- Start the consumer and send some messages: 
	```bash
	 bin/kafka-console-producer.sh --broker-list localhost:9092 --topic my-replicated-topic
	 my test message 1
	 my test message 2
	```
- Start the consumer: `bin/kafka-console-consumer.sh --zookeeper localhost:2181 --from-beginning --topic my-replicated-topic`
