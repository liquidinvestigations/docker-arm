FROM arm32v6/alpine:3.6

RUN apk \
  --no-cache \
  --repository http://dl-cdn.alpinelinux.org/alpine/edge/community/ \
  add nodejs nodejs-npm

RUN mkdir -p /opt/hoover/ui
WORKDIR /opt/hoover/ui

ADD ./upstream/package.json /opt/hoover/ui/
RUN npm install

ADD ./upstream/ /opt/hoover/ui/
