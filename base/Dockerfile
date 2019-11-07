FROM openjdk:8 AS spark-base

RUN curl http://apache.mirror.anlx.net/spark/spark-2.4.4/spark-2.4.4-bin-hadoop2.7.tgz | tar -xzf - && \
	mv /spark* /spark
RUN apt update && \
    apt install -qy python3

WORKDIR /spark
ENV spark_port 7077
ENV web_port 8080
ENV PYSPARK_PYTHON python3
ENV PYSPARK_DRIVER_PYTHON python3

FROM spark-base AS spark-master

ENTRYPOINT ["bin/spark-class", "org.apache.spark.deploy.master.Master"]

FROM spark-base AS spark-worker

ENTRYPOINT ["bin/spark-class", "org.apache.spark.deploy.worker.Worker"]

FROM spark-base AS spark-submit

ENTRYPOINT ["/spark/bin/spark-submit"] 
CMD ["--master", "spark://spark-master:7077", "--class", "org.apache.spark.examples.SparkPi", "examples/jars/spark-examples_2.11-2.4.4.jar", "1000"]

FROM spark-base AS pyspark-shell

ENV PYSPARK_DRIVER_PYTHON ipython3

RUN apt update && \
    apt install -qy ipython3
ENTRYPOINT ["bin/pyspark"]

FROM spark-base AS pyspark-notebook

ENV PYSPARK_DRIVER_PYTHON jupyter
ENV PYSPARK_DRIVER_PYTHON_OPTS "notebook --ip 0.0.0.0"

RUN apt update && \
    apt install -qy python3-notebook jupyter-core jupyter-notebook jupyter-nbextension-jupyter-js-widgets

RUN mkdir /data
WORKDIR /data
ENTRYPOINT ["/spark/bin/pyspark"]
