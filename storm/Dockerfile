FROM phusion/baseimage

# Install required packages

RUN apt-get update && \
    apt-get install -y build-essential && \
    apt-get install -y software-properties-common python-software-properties && \
    apt-get install -y python && \
    apt-get install -y wget

# Install Java.

RUN \
  add-apt-repository -y ppa:webupd8team/java && \
  apt-get update && \
  apt-get install -y openjdk-8-jdk && \
  rm -rf /var/lib/apt/lists/* && \
  rm -rf /var/cache/oracle-jdk8-installer

ENV JAVA_HOME /usr/lib/jvm/java-1.8.0-openjdk-amd64
ENV JAVAHOME /usr/lib/jvm/java-1.8.0-openjdk-amd64

# Install Storm.

ENV STORM_USER=platform \
    STORM_CONF_DIR=/conf \
    STORM_DATA_DIR=/data \
    STORM_LOG_DIR=/logs

# Add a user and make dirs
RUN set -ex; \
    adduser "$STORM_USER"; \
    mkdir -p "$STORM_CONF_DIR" "$STORM_DATA_DIR" "$STORM_LOG_DIR"; \
    chown -R "$STORM_USER:$STORM_USER" "$STORM_CONF_DIR" "$STORM_DATA_DIR" "$STORM_LOG_DIR"``

# Apache Storm distribution version
ARG DISTRO_NAME=apache-storm-0.10.0

# Download Apache Storm.
RUN set -ex; \
    wget -q "http://archive.apache.org/dist/storm/$DISTRO_NAME/$DISTRO_NAME.tar.gz"; \
    export GNUPGHOME="$(mktemp -d)"; \
    tar -xzf "$DISTRO_NAME.tar.gz"; \
    chown -R "$STORM_USER:$STORM_USER" "$DISTRO_NAME"; \
    rm "$DISTRO_NAME.tar.gz";

ENV PATH $PATH:/$DISTRO_NAME/bin

# Copy storm configuration files to image
ADD storm.yaml /conf

RUN chown -R "$STORM_USER" "$STORM_CONF_DIR" "$STORM_DATA_DIR" "$STORM_LOG_DIR"

# Install Maven.
ENV MAVEN_VERSION="3.5.4" \
    M2_HOME=/usr/lib/mvn

RUN cd /tmp && \
    wget "http://www-us.apache.org/dist/maven/maven-3/$MAVEN_VERSION/binaries/apache-maven-$MAVEN_VERSION-bin.tar.gz" && \
    tar -zxvf "apache-maven-$MAVEN_VERSION-bin.tar.gz" && \
    mv "apache-maven-$MAVEN_VERSION" "$M2_HOME" && \
    ln -s "$M2_HOME/bin/mvn" /usr/bin/mvn && \
    rm -R /tmp/*

RUN mkdir /project

WORKDIR /project
