# Example: Log Collector with Fluent Bit
To play around with you have to start all services with docker compose.

```
docker compose up
```

## Services: (Mapped Docker Ports)

- Fluent Bit
    - HTTP INPUT (http://localhost:8888)
    - Health, Metrics, etc. (http://localhost:8080)
- Elasticsearch (http://localhost:9200)
- Kafka UI (http://localhost:8082)

## Fluent Bit configurtaion:

Fluent Bit HTTP INPUT (http://localhost:8888)
    - OUTPUT Kafka -> tag = kafka.* 
    - OUTPUT Elasticsearch -> tag = es.*
    - OUTPUT stdout -> tag = stdout.*



## Collect Events with Fluent Bit

This will log events to stdout.

```
curl -d @logs/events.json -XPOST -H "content-type: application/json" http://localhost:8888/stdout.log
```

This will log events to kafka topics. You can checkout all the kafka message with the kafka ui (http://localhost:8082/).

```
curl -d @logs/events.json -XPOST -H "content-type: application/json" http://localhost:8888/kafka.log
```

The following will log to elasticsearch, you can checkout out the entries in elasticsearch (http://localhost:9200/my_index/_search?pretty)

```
curl -d @logs/events.json -XPOST -H "content-type: application/json" http://localhost:8888/es.log
```