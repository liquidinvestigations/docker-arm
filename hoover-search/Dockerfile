FROM arm64v8/debian:jessie

ENV PYTHONUNBUFFERED 1

RUN echo 'deb http://deb.debian.org/debian jessie non-free' >> /etc/apt/sources.list
RUN echo 'deb http://deb.debian.org/debian jessie-updates non-free' >> /etc/apt/sources.list
RUN echo 'deb http://security.debian.org jessie/updates non-free' >> /etc/apt/sources.list

RUN apt-get update
RUN apt-get install -y --no-install-recommends \
  build-essential \
  python3 python3-dev python3-pip \
  postgresql-server-dev-all \
  qrencode \
  curl
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

RUN ln -s /usr/bin/python3 /usr/local/bin/python
RUN ln -s /usr/bin/pip3 /usr/local/bin/pip

RUN mkdir -p /opt/hoover/search
WORKDIR /opt/hoover/search

ADD ./upstream/requirements.txt ./
RUN pip3 install -r requirements.txt

COPY ./upstream/ ./

RUN echo 'SECRET_KEY="a"' > hoover/site/settings/local.py
RUN ./manage.py downloadassets
RUN ./manage.py collectstatic --noinput
RUN rm hoover/site/settings/local.py

RUN curl https://raw.githubusercontent.com/vishnubob/wait-for-it/8ed92e8c/wait-for-it.sh -o /wait-for-it
RUN echo '#!/bin/bash -e' > /runserver && \
    echo 'waitress-serve --port 80 hoover.site.wsgi:application' >> /runserver && \
    chmod +x /runserver /wait-for-it

CMD /runserver
