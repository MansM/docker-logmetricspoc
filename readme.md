## Logs and Metrics POC


### Why?
Just because I can and want to learn something

### What?
* Docker
* Filebeat
* Metricbeat
* Kafka
* Logstash
* Elasticsearch
* Kibana
* ManageIQ (generates lots of logs with some clicks, but please inform if there is a better thingy)

### How?

docker-compose up -d

browser -> [http://dockerip:5601](http://dockerip:5601) / [http://localhost:5601](http://localhost:5601)

Pattern -> filebeat-* or metricbeat-*


### FAQ

#### Help! No logs are coming in
Probably there is a chance that the docker-machine time is totally out of sync with your systemtime. Check this with:
```
date && docker exec -it kibana  date
Fri Dec  9 15:25:30 CET 2016
Fri Dec  9 14:25:29 UTC 2016
```

try this first:
docker run --rm --privileged centos:7 hwclock -s

if its totally off... just restart your docker-machine/docker for mac or windows

If this is not the case... I probably messed up, please send me a message

### Credits
manageiq grok pattern: https://github.com/ldomb/elkformiqonrhel7
