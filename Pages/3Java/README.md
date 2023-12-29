
# Creating a producer

To create a producer, we will also need a producer property object, a producer record (which sends the data) and then to send and flush + close the producer.

```
public class ProducerDemo {

    private static Logger log = LoggerFactory.getLogger(ProducerDemo.class.getName());

    public static void main(String[] args) {
        log.info("Testing!");
        // Create producer property
        Properties properties = new Properties();
        properties.setProperty("bootstrap.servers", "localhost:29092");
        properties.setProperty("key.serializer", StringSerializer.class.getName());
        properties.setProperty("value.serializer", StringSerializer.class.getName());

        // Create producer
        KafkaProducer<String,String> kafkaProducer = new KafkaProducer<>(properties);

        // Create a producer record
        ProducerRecord<String,String> producerRecord =
                new ProducerRecord<>("third_topic", "This is from intellij");

        // Send data
        kafkaProducer.send(producerRecord);

        // flush and close the producer
        kafkaProducer.flush();
        kafkaProducer.close();
    }

}
```

## Producer Callback

A producer callback is a mechanism to configure a producer to perform implementations depending upon a successful or failed send.