FROM arm64v8/debian:stretch

# copied from https://github.com/LogicalSpark/docker-tikaserver/blob/6b589fb/Dockerfile

ENV TIKA_VERSION 1.16
ENV TIKA_SERVER_URL https://www.apache.org/dist/tika/tika-server-$TIKA_VERSION.jar

RUN apt-get update
RUN apt-get install -y \
    openjdk-8-jre-headless curl gdal-bin gnupg tesseract-ocr \
    tesseract-ocr-eng tesseract-ocr-ita tesseract-ocr-fra \
    tesseract-ocr-spa tesseract-ocr-deu
RUN curl -sSL https://people.apache.org/keys/group/tika.asc -o /tmp/tika.asc
RUN gpg --import /tmp/tika.asc
RUN curl -sSL $TIKA_SERVER_URL.asc -o /tmp/tika-server-$TIKA_VERSION.jar.asc
RUN curl -sSL $TIKA_SERVER_URL -o /tika-server-$TIKA_VERSION.jar
RUN apt-get clean -y && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

EXPOSE 9998
ENTRYPOINT java -jar /tika-server-${TIKA_VERSION}.jar -h 0.0.0.0
