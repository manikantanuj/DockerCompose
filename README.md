# DockerCompose
This is a basic project of installing Kafka using Docker.

Below are the steps to install Kafka using Docker.
1. Install Docker Desktop application.
2. Create a folder e.g "Kafka-installation" and inside that create a docker-compose.yml file.

   Inside that file, write the services which you want to start.
So for using Kafka, the pre-requisite is Zookeeper.
3. Here we will add the details of services. 

Below will be the contents.

   
version: '3.1'

services:
  zookeeper:
    image: wurstmeister/zookeeper
    container_name: zookeeper
    ports:
      - "2181:2181"
  kafka:
    image: wurstmeister/kafka
    container_name: kafka
    ports:
      - "9092:9092"
    environment:
      KAFKA_ADVERTISED_HOST_NAME: localhost
      KAFKA_ZOOKEEPER_CONNECT: zookeeper:2181

4. Now go to the folder and start GitBash, and run the command
   docker compose -f docker-compose.yml up -d
   here -f is for file and -d is for detach.

OUTPUT
---------
---------

Network kafka-installation_default       Created
Container Zookeeper                      Started
Container Kafka                          Started


Now open any terminal and create a topic and then produce a message and consumer will consume the message.
STEP 1. Create a topic
Open a terminal and run the command : docker exec -it kafka /bin/sh
cd opt
cd kafka-2013-2.8.1
cd bin
kafka-topics.sh --bootstarp-server localhost:9092 --create --topic topicTest --partitions 3 --replication-factor 1

Topic with topicTest is created.

Step 2: Produce a message on the topic topicTest
Run the command 
kafka-console-producer.sh --bootstrap-server localhost:9092 --topic topicTest
Write some message and hit enter.

Step 3: Consume the message from the topic topicTest
Run the command
kafka-consome-consumer.sh --bootstrap-server localhost:9092 --topic topicTest --from-beginning
