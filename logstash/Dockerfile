FROM centos:7

ARG http_proxy
ARG https_proxy

ENV container docker
ENV LOGSTASH_VERSION 5.1.1

RUN (cd /lib/systemd/system/sysinit.target.wants/; for i in *; do [ $i == systemd-tmpfiles-setup.service ] || rm -f $i; done); \
    rm -f /lib/systemd/system/multi-user.target.wants/*;\
    rm -f /etc/systemd/system/*.wants/*;\
    rm -f /lib/systemd/system/local-fs.target.wants/*; \
    rm -f /lib/systemd/system/sockets.target.wants/*udev*; \
    rm -f /lib/systemd/system/sockets.target.wants/*initctl*; \
    rm -f /lib/systemd/system/basic.target.wants/*;\
    rm -f /lib/systemd/system/anaconda.target.wants/*;

RUN yum install -y java-1.8.0-openjdk-headless which

RUN curl -o /root/logstash.rpm https://artifacts.elastic.co/downloads/logstash/logstash-$LOGSTASH_VERSION.rpm
RUN yum install -y /root/logstash.rpm && yum install -y java-1.8.0-openjdk-devel gem 

#needed for proxy
#COPY settings.xml /root/.m2/settings.xml
RUN /usr/share/logstash/bin/logstash-plugin install logstash-input-beats logstash-input-kafka

COPY logstash.conf /etc/logstash/conf.d/logstash.conf
COPY grokevmpattern.conf /opt/logstash/patterns/evm.conf


RUN systemctl enable logstash

CMD ["/usr/sbin/init"]