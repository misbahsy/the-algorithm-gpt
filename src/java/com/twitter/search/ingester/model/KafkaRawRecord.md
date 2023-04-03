[View code on GitHub](https://github.com/misbahsy/the-algorithm/src/java/com/twitter/search/ingester/model/KafkaRawRecord.java)

The `KafkaRawRecord` class represents the raw data contained in a Kafka record. It has two fields: `data`, which is a byte array containing the actual data, and `readAtTimestampMs`, which is a long representing the timestamp at which the record was read.

This class is likely used in the larger project to handle incoming data from Kafka. When a record is read from Kafka, it is represented as a `KafkaRawRecord` object, which can then be processed further by other parts of the system.

For example, suppose we have a Kafka topic called `tweets` that contains raw tweet data. We could use the `KafkaRawRecord` class to read records from this topic and then pass them to a processing pipeline that extracts relevant information from the tweets and stores it in a database.

Here is an example of how we might use the `KafkaRawRecord` class to read records from a Kafka topic:

```java
import org.apache.kafka.clients.consumer.ConsumerRecord;
import com.twitter.search.ingester.model.KafkaRawRecord;

// create a Kafka consumer
KafkaConsumer<String, byte[]> consumer = new KafkaConsumer<>(props);

// subscribe to the tweets topic
consumer.subscribe(Collections.singletonList("tweets"));

// read records from the topic
while (true) {
  ConsumerRecords<String, byte[]> records = consumer.poll(Duration.ofMillis(100));
  for (ConsumerRecord<String, byte[]> record : records) {
    KafkaRawRecord rawRecord = new KafkaRawRecord(record.value(), record.timestamp());
    // process the raw record further
  }
}
```

In this example, we create a Kafka consumer and subscribe to the `tweets` topic. We then read records from the topic using the `poll` method, and for each record, we create a `KafkaRawRecord` object and pass it to a processing pipeline.
## Questions: 
 1. What is the purpose of this class?
- This class represents the raw data in a Kafka record.

2. What are the parameters of the constructor?
- The constructor takes in two parameters: a byte array representing the data and a long integer representing the timestamp in milliseconds when the data was read.

3. What methods are available in this class?
- This class has two methods: `getData()` which returns the byte array representing the data, and `getReadAtTimestampMs()` which returns the timestamp in milliseconds when the data was read.