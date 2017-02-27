FROM centos:7

ARG http_proxy
ARG https_proxy

ENV container docker
ENV KIBANA_VERSION 5.2.1

RUN (cd /lib/systemd/system/sysinit.target.wants/; for i in *; do [ $i == systemd-tmpfiles-setup.service ] || rm -f $i; done); \
    rm -f /lib/systemd/system/multi-user.target.wants/*;\
    rm -f /etc/systemd/system/*.wants/*;\
    rm -f /lib/systemd/system/local-fs.target.wants/*; \
    rm -f /lib/systemd/system/sockets.target.wants/*udev*; \
    rm -f /lib/systemd/system/sockets.target.wants/*initctl*; \
    rm -f /lib/systemd/system/basic.target.wants/*;\
    rm -f /lib/systemd/system/anaconda.target.wants/*;

RUN curl -o /root/kibana.rpm -L -O https://artifacts.elastic.co/downloads/kibana/kibana-$KIBANA_VERSION-x86_64.rpm
RUN yum localinstall -y /root/kibana.rpm
COPY kibana.yml /etc/kibana/kibana.yml

RUN systemctl enable kibana

CMD ["/usr/sbin/init"]