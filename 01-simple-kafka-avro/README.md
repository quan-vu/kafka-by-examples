# LAB01 - Simple Kafka Avro

The first lab for start working with Kafka.

## Techstack

- Docker
- Confluent Kafka 6.1.0

## Quickstart

For speed up development, I use Makefile for manage the commands which is used in this project.

Step 1: Start Kafka infras with docker

```shell
make start
```

Step 2: Create demo topic

```shell
make create-topic
```

Step 3: Start an Avro console consumer

```shell
make start-avro-consumer
```

Step 3: Produce your first Avro records

```shell
# 1. Access inside schema-registry container
docker-compose exec schema-registry bash

# run the following command to start a console producer with the schema you created previously
kafka-avro-console-producer --topic example-topic-avro --bootstrap-server broker:9092 --property value.schema="$(< /opt/app/schema/order_detail.avsc)"

# 2. Copying and pasting one line at a time, hit enter
{"number": 100002, "date": 1596490462, "shipping_address": "456 Everett St, Palo Alto, 94301 CA, USA", "subtotal": 99.0, "shipping_cost": 0.0, "tax": 8.91, "grand_total": 107.91}

# 3. Go back to the Avro console consumer window and look for the output.
# {"number": 100002, "date": 1596490462, "shipping_address": "456 Everett St, Palo Alto, 94301 CA, USA", "subtotal": 99.0, "shipping_cost": 0.0, "tax": 8.91, "grand_total": 107.91}
```

## Reference

- [Console Producer and Consumer for Avro messages
](https://kafka-tutorials.confluent.io/kafka-console-consumer-producer/kafka.html)
