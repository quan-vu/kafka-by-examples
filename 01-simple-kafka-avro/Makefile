start: # step 1
	docker-compose up -d 

stop:
	docker-compose down

clean:
	docker-compose down -v

create-topic: # step 2
	docker-compose exec broker kafka-topics --create --topic example-topic-avro --bootstrap-server broker:9092 --replication-factor 1 --partitions 1

create-avro-schema: # step 3
	sudo chmod -R 777 ./schema
	cp ./demodata/order_detail.avsc ./schema/order_detail.avsc

start-avro-consumer: # step 4
	docker-compose exec schema-registry bash -c "kafka-avro-console-consumer --topic example-topic-avro --bootstrap-server broker:9092"

produce-avro-record: # step 5:
	docker-compose exec schema-registry bash -c 'kafka-avro-console-producer --topic example-topic-avro --bootstrap-server broker:9092 --property value.schema="$(< /opt/app/schema/order_detail.avsc)"'
