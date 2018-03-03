FROM docker.elastic.co/kibana/kibana:6.2.2

COPY ./config/kibana.yml /usr/share/kibana/config/kibana.yml

USER root

RUN echo "Asia/Shanghai" > /etc/timezone

USER kibana
