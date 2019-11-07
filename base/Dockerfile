FROM openjdk:buster AS spark-base

RUN curl http://apache.mirror.anlx.net/spark/spark-2.4.4/spark-2.4.4-bin-hadoop2.7.tgz | tar -xzf - && \
	mv /spark* /spark

WORKDIR /spark
ENV spark_port 7077
ENV web_port 8080

FROM spark-base AS spark-master

ENTRYPOINT ["bin/spark-class", "org.apache.spark.deploy.master.Master"]

FROM spark-base AS spark-worker

ENTRYPOINT ["bin/spark-class", "org.apache.spark.deploy.worker.Worker"]

FROM spark-base AS spark-submit

ENTRYPOINT ["/spark/bin/spark-submit"] 
CMD ["--master", "spark://spark-master:7077", "--class", "org.apache.spark.examples.SparkPi", "examples/jars/spark-examples_2.11-2.4.4.jar", "1000"]
