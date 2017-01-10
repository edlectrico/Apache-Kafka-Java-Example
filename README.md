# Apache-Kafka-SimpleProducer-Example
A simple Java example of how Apache Kafka works sending integer messages to a topic.

Requisites: 
  1. Zookeeper must be installed in your system
  2. Kafka must be also installed (too obvious)

Before executing this class we must:

  1. Launch Zookeeper: 
```{r, engine='bash', launch_zookeeper}
./path_to_kafka/bin/zookeeper-server-start.sh path_to_kafka/config/zookeeper.properties 
```  
  2. Launch a Kafka broker: 
```{r, engine='bash', launch_kafka_broker}
./path_to_kafka/bin/kafka-server-start.sh path_to_kafka/config/server.properties 
``` 
  3. Create a topic: 
```{r, engine='bash', launch_kafka_broker}
./path_to_kafka/bin/kafka-topic.sh --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic <topic_name>
```
Execution steps:
```{r, engine='bash', javac}
javac -cp "path_to_kafka/libs/*" path_to_class/SimpleProducer.java
```  
```{r, engine='bash', java}
java -cp .:"path_to_kafka/libs/*" path_to_class/SimpleProducer <topic_name>
```  

Execution example:
```{r, engine='bash', javac}
javac -cp "path_to_kafka/libs/*" SimpleProducer.java
```  
```{r, engine='bash', java}
java -cp .:"path_to_kafka/libs/*" SimpleProducer KafkaJavaTopic
```  

To check that it's actually working:
  1. We should see a console output message: "Message sent successfully"
  2. We register a Consumer in a new Terminal to receive the messages sent by the Producer:
```{r, engine='bash', check}
./path_to_kafka/bin/kafka-console-consumer.sh --zookeeper localhost:2181 --topic <topic_name> --from-beginning
```
Then the ouput should be:
1
2
3... etc

Some of this work comes from the Kafka Introduction in https://www.tutorialspoint.com/apache_kafka/apache_kafka_quick_guide.htm
