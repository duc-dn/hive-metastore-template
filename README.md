## Iceberg Kafka Connector
---
Build jar files connector in https://github.com/tabular-io/iceberg-kafka-connect
Path project in 102: `/home/dev-ic/ducdn/iceberg-kafka-connect`
#### Creating config sink
- Edit config sink file in `/home/dev-ic/ducdn/iceberg-kafka-connect/connector-config`
---
#### Post connector to kafka-connect
```
curl -X POST -H "Content-Type:application/json" -d @$PWD/connector-config/iceberg-config-hive.json http://localhost:8083/connectors
```
#### Creating iceberg table in Trino
```
CREATE TABLE iceberg_hms.default.users (
    userid varchar,
    name varchar,
    year integer,
    job varchar,
    city varchar,
    salary bigint
)
with (
    format='parquet',
    partitioning = ARRAY['city'],
    location = 's3a://iceberg-kafka-connector/users'
);

insert into iceberg_hms."default".users values ('user', 'duc', 2020, 'data', 'Ha Nam', 1213213);
select  * from "default".users;
```


CREATE TABLE `hive_catalog`.`default`.`sample` (
    id BIGINT COMMENT 'unique id',
    data STRING
);