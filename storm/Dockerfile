FROM drrzmr/java:8.0.201-2

# Install Storm.
ENV STORM_USER=platform \
    STORM_CONF_DIR=/conf \
    STORM_DATA_DIR=/data \
    STORM_LOG_DIR=/logs

ENV JAVA_HOME=/opt/sdkman/candidates/java/current

RUN apt-get update &&\
    apt-get install -y python &&\
    apt-get autoclean

# Add a user and make dirs
RUN set -ex; \
    adduser "$STORM_USER"; \
    mkdir -p "$STORM_CONF_DIR" "$STORM_DATA_DIR" "$STORM_LOG_DIR"; \
    chown -R "$STORM_USER:$STORM_USER" "$STORM_CONF_DIR" "$STORM_DATA_DIR" "$STORM_LOG_DIR"``

# Apache Storm distribution version
ARG STORM_VERSION=0.10.0

RUN set -eux; \
    curl -s "http://archive.apache.org/dist/storm/apache-storm-$STORM_VERSION/apache-storm-$STORM_VERSION.tar.gz" | tar zxC /opt; \
    ln -s /opt/apache-storm-${STORM_VERSION} /opt/storm

ENV PATH $PATH:/opt/apache-storm-$STORM_VERSION/bin

# Copy storm configuration files to image
ADD storm.yaml /conf

RUN chown -R "$STORM_USER" "$STORM_CONF_DIR" "$STORM_DATA_DIR" "$STORM_LOG_DIR"

# Install Maven.
RUN mkdir /project

EXPOSE 8080/tcp

WORKDIR /project
