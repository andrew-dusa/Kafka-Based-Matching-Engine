# Kafka-Based Matching-Engine

The Kafka based matching engine is a high-performance matching engine built with **Apache Kafka** in **Java**, designed to process real-betting and trading transactions. It matches buy and sell orders efficiently and maintains low latency and high throughput.

## Tech Stack

- **Apache Kafka**: Used for real-time data streaming and event-driven architecture.
- **AWS EC2**: Cloud hosting allows for scaling and availability.

## Features

- **Scalable Architecture**: Using Kafka's partitioning and replication to ensure scalability and reliability without ever dropping a message.
- **Custom Serializers/Deserializers**: Custon data handling within Kafka Streams topology allows for improved performance.  
- **Real-Time Order Matching**: Processes thousands of order per second with optimized trade execution algorithms.
- **Deployed on AWS**: Using **AWS EC2**, leveraging load balancing and automatic scaling to support concurrent users.

## How to run it:

First, let's start zookeeper and kafka with Docker:
Run:
```bash
$ docker run --name zookeeper  -p 2181:2181 -d zookeeper
```
Then:
```bash
$ docker run --name kafka -p 9092:9092 \
  -e KAFKA_ZOOKEEPER_CONNECT=$HOSTNAME:2181 \
  -e KAFKA_ADVERTISED_LISTENERS=PLAINTEXT://$HOSTNAME:9092 \
  -e KAFKA_OFFSETS_TOPIC_REPLICATION_FACTOR=1 -d confluentinc/cp-kafka
```    
Next we create the topic:
```bash
$ node topic.js
```  
Then in one terminal start the Test:
```bash
$ node exchange_test.js
```
In a new terminal, start a consumer to simulate real-time trading:
```bash
$ node consumer.js
```
Build using maven or IDE:
```bash
$ mvn install
```
Run:
```bash
$ java -cp target/KProcessor-1.0-SNAPSHOT.jar KProcessor
```
