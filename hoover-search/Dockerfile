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
  qrencode


RUN apt-get clean && rm -rf /var/lib/apt/lists/*

RUN mkdir -p /opt/hoover/search
WORKDIR /opt/hoover/search

ADD ./upstream/requirements.txt ./
RUN pip3 install -r requirements.txt

COPY ./upstream/ ./

RUN echo 'SECRET_KEY="a"' > hoover/site/settings/local.py
RUN python3 manage.py downloadassets
RUN python3 manage.py collectstatic --noinput
RUN rm hoover/site/settings/local.py

CMD waitress-serve --port 80 hoover.site.wsgi:application
