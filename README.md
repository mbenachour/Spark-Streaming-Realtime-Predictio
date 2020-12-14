# Spark streaming and real-time ML prediction

this is the code repository associated with my blog [article](https://mohamedbenachour.net/2020/12/11/power-generation-prediction-using-realtime-inference-with-spark-structured-streaming-and-kafka/)


## Run Kafka Producer

I used   [confluent cloud](https://pip.pypa.io/en/stable/) to create a kafka cluster, once that is done download your config file and place it in this repo ( I named it config.txt)
once that is done run this command 
```bash
python producer.py -f config.txt -t <topic_name>
```

## Databricks Notebook

I have created my notebook on [databricks](https://community.cloud.databricks.com/), you can import it from this link [here](https://databricks-prod-cloudfront.cloud.databricks.com/public/4027ec902e239c93eaaa8714f173bcfc/7619028303538336/2736564566365094/2061520514314263/latest.html)

Once imported, use your Kafka credentials when initializing the readStream connection :
 

```python
dfs = spark.readStream .format("kafka") .option("includeHeaders", "true") 
.option("kafka.bootstrap.servers", "pkc-onym6.us-east-1.aws.confluent.cloud:9092") 
.option("subscribe", "ccgt_sensors") .option("startingOffsets", "latest") 
.option("kafka.security.protocol","SASL_SSL") .option("kafka.sasl.mechanism", "PLAIN") 
.option("kafka.sasl.jaas.config", "kafkashaded.org.apache.kafka.common.security.plain.PlainLoginModule required username=\"<Kafka_username>\" password=\"<kafka_password>\";") 
.load()
```

