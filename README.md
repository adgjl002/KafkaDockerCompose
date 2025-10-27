# Docker Commands
docker-compose -f docker-compose-cluster.yml down
docker-compose -f docker-compose-cluster.yml up -d
docker-compose -f docker-compose-cluster.yml ps
docker-compose -f docker-compose-cluster.yml logs Kafka00Service
docker stats Kafka00Container Kafka01Container Kafka02Container

# Broker Connect Test
docker exec -it Kafka00Container kafka-broker-api-versions --bootstrap-server Kafka00Service:9092

# Kafka Container Connect
docker ps
docker exec -it [container-id] bash

# Kafka Topic Commands
kafka-topics --create --topic test-topic --bootstrap-server Kafka00Service:9092
kafka-topics --list --bootstrap-server Kafka00Service:9092

# Kafka Producer & Consumer Commands
kafka-console-producer --topic test-topic --bootstrap-server Kafka00Service:9092
kafka-console-consumer --topic test-topic --bootstrap-server Kafka00Service:9092 --from-beginning

# 일회성으로 Kafka 명령어 실행
docker network ls | grep kafka
docker run --rm --network [network-name] confluentinc/cp-kafka:latest kafka-topics --create --topic [topic-name] --bootstrap-server Kafka00Service:9092

# Kafka UI
http://localhost:9206

# Document for confluentinc/cp-kafka
https://hub.docker.com/r/confluentinc/cp-kafka/
https://docs.confluent.io/platform/current/installation/docker/config-reference.html