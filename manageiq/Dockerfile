FROM manageiq/manageiq:latest-darga

ENV BEATS_VERSION 5.1.1

RUN curl -o /root/filebeat.rpm -L -O https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-$BEATS_VERSION-x86_64.rpm 
RUN curl -o /root/metricbeat.rpm -L -O https://artifacts.elastic.co/downloads/beats/metricbeat/metricbeat-$BEATS_VERSION-x86_64.rpm

RUN yum localinstall -y /root/filebeat.rpm /root/metricbeat.rpm && \
    yum clean all

COPY filebeat.yml /etc/filebeat/filebeat.yml
COPY metricbeat.yml /etc/metricbeat/metricbeat.yml

RUN systemctl enable filebeat
RUN systemctl enable metricbeat

