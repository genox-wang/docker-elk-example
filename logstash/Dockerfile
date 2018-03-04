FROM docker.elastic.co/logstash/logstash:6.2.2

LABEL maintainer="genius840215@163.com"

COPY ./config /usr/share/logstash/config
COPY ./pipeline /usr/share/logstash/pipeline

USER root

RUN echo "Asia/Shanghai" > /etc/timezone

USER logstash