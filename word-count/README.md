## Kafka Commands

### Create topic

```
./kafka-topics.sh --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic word-count-input

./kafka-topics.sh --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic word-count-output

```

### Producer
```
./kafka-console-producer.sh --broker-list localhost:9092 --topic word-count-input
```
### Consumer

```
./kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic word-count-output --from-beginning \
--formatter kafka.tools.DefaultMessageFormatter \
--property print.key=true \
--property print.value=true \
--property key.deserializer=org.apache.kafka.common.serialization.StringDeserializer \
--property value.deserializer=org.apache.kafka.common.serialization.LongDeserializer

```

### Log compaction

```
./kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic word-count-output --from-beginning \
--partitions 1 --replication-factor 1 \
--config cleanup.policy=compact \ 
--config min.cleanable.dirty.ration=0.005 \
--config segment.ms=10000
```
