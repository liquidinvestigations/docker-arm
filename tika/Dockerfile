FROM arm64v8/debian:stretch

# copied from https://github.com/LogicalSpark/docker-tikaserver/blob/6b589fb/Dockerfile

ENV TIKA_VERSION 1.16
ENV TIKA_SERVER_URL https://www.apache.org/dist/tika/tika-server-$TIKA_VERSION.jar

RUN set -e \
 && apt-get update \
 && apt-get install -y \
      openjdk-8-jre-headless curl gdal-bin gnupg tesseract-ocr \
      tesseract-ocr-eng tesseract-ocr-ita tesseract-ocr-fra \
      tesseract-ocr-spa tesseract-ocr-deu \
 && apt-get clean -y && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN set -e \
 && curl -sSL https://people.apache.org/keys/group/tika.asc -o /tmp/tika.asc \
 && gpg --import /tmp/tika.asc \
 && curl -sSL $TIKA_SERVER_URL.asc -o /tmp/tika-server-$TIKA_VERSION.jar.asc \
 && curl -sSL $TIKA_SERVER_URL -o /tika-server-$TIKA_VERSION.jar

EXPOSE 9998
ENTRYPOINT java -jar /tika-server-${TIKA_VERSION}.jar -h 0.0.0.0
