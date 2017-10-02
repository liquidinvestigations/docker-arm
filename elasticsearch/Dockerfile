FROM openjdk:8-jre

ENV ES_VERSION 2.4.3
ENV ES_DOWNLOAD_URL https://download.elastic.co/elasticsearch/elasticsearch/elasticsearch-$ES_VERSION.tar.gz

RUN cd /usr/share && curl -L $ES_DOWNLOAD_URL | tar xz
RUN mv /usr/share/elasticsearch-$ES_VERSION /usr/share/elasticsearch
COPY runserver /runserver

EXPOSE 9200
CMD /runserver
