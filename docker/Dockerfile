# base image
FROM openjdk:11

# define spark and hadoop versions
ENV SPARK_VERSION=3.2.0
ENV HADOOP_VERSION=3.3.1

# download and install hadoop
RUN mkdir -p /opt && \
    cd /opt && \
    curl -fSL http://archive.apache.org/dist/hadoop/common/hadoop-${HADOOP_VERSION}/hadoop-${HADOOP_VERSION}.tar.gz -o hadoop.tar.gz && \
    tar -xzf hadoop.tar.gz && \
    ln -s hadoop-${HADOOP_VERSION} hadoop && \
    rm hadoop.tar.gz && \
    echo "Hadoop ${HADOOP_VERSION} installed in /opt/hadoop"

# download and install spark
RUN mkdir -p /opt && \
    cd /opt && \
    curl -fSL http://archive.apache.org/dist/spark/spark-${SPARK_VERSION}/spark-${SPARK_VERSION}-bin-hadoop2.7.tgz -o spark.tgz && \
    tar -xzf spark.tgz && \
    ln -s spark-${SPARK_VERSION}-bin-hadoop2.7 spark && \
    rm spark.tgz && \
    echo "Spark ${SPARK_VERSION} installed in /opt/spark"

# add scripts and update spark default config
ADD common.sh spark-master spark-worker /
ADD spark-defaults.conf /opt/spark/conf/spark-defaults.conf

# update PATH
ENV PATH $PATH:/opt/spark/bin
