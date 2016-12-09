FROM centos:7

ARG http_proxy
ARG https_proxy

ENV container docker

RUN (cd /lib/systemd/system/sysinit.target.wants/; for i in *; do [ $i == systemd-tmpfiles-setup.service ] || rm -f $i; done); \
    rm -f /lib/systemd/system/multi-user.target.wants/*;\
    rm -f /etc/systemd/system/*.wants/*;\
    rm -f /lib/systemd/system/local-fs.target.wants/*; \
    rm -f /lib/systemd/system/sockets.target.wants/*udev*; \
    rm -f /lib/systemd/system/sockets.target.wants/*initctl*; \
    rm -f /lib/systemd/system/basic.target.wants/*;\
    rm -f /lib/systemd/system/anaconda.target.wants/*;

RUN yum install -y java-1.8.0-openjdk-headless which

RUN curl -o /root/logstash.rpm https://artifacts.elastic.co/downloads/logstash/logstash-5.0.2.rpm
RUN yum install -y /root/logstash.rpm && yum install -y java-1.8.0-openjdk-devel gem 

#needed for proxy
#COPY settings.xml /root/.m2/settings.xml
RUN /usr/share/logstash/bin/logstash-plugin install logstash-input-beats

COPY logstash.conf /etc/logstash/conf.d/logstash.conf



RUN systemctl enable logstash

CMD ["/usr/sbin/init"]