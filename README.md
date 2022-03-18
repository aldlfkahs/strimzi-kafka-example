# Kafka Connect
## Mysql to Postgres 예제
* DB 생성
  * Mysql, Postgres, Redis 생성
    ```bash
    kubectl apply -f db-deploy/
    ```

* Kafka Broker, Schema Registry, Kafka Connect 생성
  * Kafka Broker
    ```bash
    kubectl apply -f 1_kafka-simple-connect.yaml
    kubectl apply -f 2_schema-registry.yaml
    kubectl apply -f 3_kafka-connect.yaml
    ```

* Mysql Source Connector, Postgres Sink connector 생성
  * 컨테이너 접속하여 아래 명령어 실행
    ```bash
    kubectl apply -f 4_kafka-mysql-source-connector.yaml
    kubectl apply -f 5_kafka-postgres-sink-connector.yaml
    ```

* Postgres에 Mysql과 똑같은 테이블 및 데이터가 생성되는 것 확인
  * postgres 컨테이너 접속
  ```bash
  kubectl exec -it {postgres pod 이름} -n kafka -- psql -U postgres
  ```
  * 테이블 확인 및 데이터 확인
  ```bash
  postgres=# \dt
  postgres=# select * from example;
  ```
