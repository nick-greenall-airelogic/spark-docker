# Little local spark runner

A little docker stack to toy with spark.

## Build

```shell
docker-compose build
```

## Run

Without further modification this runs spark with a single worker and runs a jupyter
notebook application with a python3 notebooks setup.

```shell
docker-compose up -d
```
The spark control panel is available under `localhost:8080` and the jupyter notebook application
is available under `localhost:8888`.

## Example application

Uncomment the service in the `docker-compose.yaml` file, then:
```shell
docker-compose build
docker-compose run spark-example
```

### Caveats 

This is provided as is under a BSD 3 clause license. It is intended for experimenting with Spark
on a local machine and not for deployment.
