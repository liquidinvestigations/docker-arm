FROM arm64v8/debian:jessie

ENV PYTHONUNBUFFERED 1
ENV LANG C.UTF-8

RUN set -e \
 && echo 'deb http://deb.debian.org/debian jessie non-free' >> /etc/apt/sources.list \
 && echo 'deb http://deb.debian.org/debian jessie-updates non-free' >> /etc/apt/sources.list \
 && echo 'deb http://security.debian.org jessie/updates non-free' >> /etc/apt/sources.list \
 && apt-get update \
 && apt-get install -y --no-install-recommends \
      build-essential \
      libxml2-dev libxslt1-dev libmagic-dev \
      python3 python3-dev python3-pip \
      postgresql-server-dev-all \
      p7zip-full p7zip-rar \
      pst-utils \
      cpanminus \
      curl \
 && ln -s /usr/bin/python3 /usr/local/bin/python \
 && ln -s /usr/bin/pip3 /usr/local/bin/pip \
 && cpanm --notest Email::Outlook::Message \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN mkdir -p /opt/hoover/snoop
WORKDIR /opt/hoover/snoop

ADD ./upstream/requirements.txt ./
RUN pip3 install -r requirements.txt

COPY ./upstream/ ./

RUN set -e \
 && curl https://raw.githubusercontent.com/vishnubob/wait-for-it/8ed92e8c/wait-for-it.sh -o /wait-for-it \
 && echo '#!/bin/bash -e' > /runserver \
 && echo 'waitress-serve --port 80 snoop.site.wsgi:application' >> /runserver \
 && chmod +x /runserver /wait-for-it

CMD /runserver
