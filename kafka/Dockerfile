FROM centos:7

ENV KAFKA_VERSION="0.10.1.0" 
ENV SCALA_VERSION="2.11"

RUN yum install -y java-1.8.0-openjdk-headless

RUN curl -o /root/kafka_${SCALA_VERSION}-${KAFKA_VERSION}.tgz \
    http://mirrors.supportex.net/apache/kafka/${KAFKA_VERSION}/kafka_${SCALA_VERSION}-${KAFKA_VERSION}.tgz && \
    tar -xvzf /root/kafka_${SCALA_VERSION}-${KAFKA_VERSION}.tgz -C /opt && \
    rm /root/kafka_${SCALA_VERSION}-${KAFKA_VERSION}.tgz

COPY server.properties /opt/kafka_${SCALA_VERSION}-${KAFKA_VERSION}/config/server.properties
CMD ["/opt/kafka_2.11-0.10.1.0/bin/kafka-server-start.sh", "/opt/kafka_2.11-0.10.1.0/config/server.properties"]