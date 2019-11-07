# Little local spark runner

A little docker stack to run spark.

## Build

```shell
docker-compose build
```

## Run

```shell
docker-compose up -d
```

## Example application

Uncomment the service in the `docker-compose.yaml` file, then:
```shell
docker-compose build
docker-compose run spark-example
```
