FROM ubuntu:focal

# See https://github.com/phusion/baseimage-docker/issues/58
RUN echo 'debconf debconf/frontend select Noninteractive' | debconf-set-selections

RUN apt-get update -y \
    && apt-get install -y wget python3-dev openjdk-8-jre-headless python3-pip nano\
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

RUN pip install --upgrade pip
RUN pip install pymongo

RUN useradd --create-home --shell /bin/bash ubuntu

ENV HOME /home/ubuntu
ENV SPARK_VERSION 3.3.0
ENV HADOOP_VERSION 3
ENV MONGO_SPARK_VERSION 3.0.1
ENV SCALA_VERSION 2.12.3

WORKDIR ${HOME}

ENV SPARK_HOME ${HOME}/spark-${SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}

ENV PATH $PATH:${SPARK_HOME}/bin

COPY files/times.json files/readme.txt files/examples.py files/initDocuments.py files/population_by_country_1980_2010.csv /home/ubuntu/

RUN chown -R ubuntu:ubuntu /home/ubuntu/*

USER ubuntu

# get spark
RUN wget https://downloads.apache.org/spark/spark-${SPARK_VERSION}/spark-${SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}.tgz && \
tar -xvzf spark-${SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}.tgz

RUN rm -fv spark-${SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}.tgz
