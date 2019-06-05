FROM drrzmr/java:8.0.201-2

ENV JAVA_HOME=/opt/sdkman/candidates/java/current

RUN apt-get update &&\
    apt-get install -y python &&\
    apt-get autoclean

# Apache Storm distribution version
ARG STORM_VERSION=0.10.0

RUN set -eux; \
    curl -s "http://archive.apache.org/dist/storm/apache-storm-$STORM_VERSION/apache-storm-$STORM_VERSION.tar.gz" | tar zxC /opt; \
    ln -s /opt/apache-storm-${STORM_VERSION} /opt/storm

ENV PATH $PATH:/opt/apache-storm-$STORM_VERSION/bin

# Copy storm configuration files to image
ADD storm.yaml /conf

RUN mkdir /project

EXPOSE 8080/tcp

WORKDIR /project
