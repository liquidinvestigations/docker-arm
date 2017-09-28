FROM arm64v8/debian:jessie

ENV PYTHONUNBUFFERED 1

RUN echo 'deb http://deb.debian.org/debian jessie non-free' >> /etc/apt/sources.list
RUN echo 'deb http://deb.debian.org/debian jessie-updates non-free' >> /etc/apt/sources.list
RUN echo 'deb http://security.debian.org jessie/updates non-free' >> /etc/apt/sources.list

RUN apt-get update
RUN apt-get install -y --no-install-recommends \
  build-essential \
  libxml2-dev libxslt1-dev libmagic-dev \
  python3 python3-dev python3-pip \
  postgresql-server-dev-all \
  p7zip-full p7zip-rar \
  pst-utils \
  cpanminus
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

RUN ln -s /usr/bin/python3 /usr/local/bin/python
RUN ln -s /usr/bin/pip3 /usr/local/bin/pip

RUN cpanm --notest Email::Outlook::Message

RUN mkdir -p /opt/hoover/snoop
WORKDIR /opt/hoover/snoop

ADD ./upstream/requirements.txt ./
RUN pip3 install -r requirements.txt

COPY ./upstream/ ./

CMD waitress-serve --port 80 snoop.site.wsgi:application
