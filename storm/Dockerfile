FROM drrzmr/java:8.0.201-2

RUN set -eux; \
apt-get update; \
apt-get -qy install python-minimal; \
rm -rf /var/lib/apt/lists/*

ENV STORM_VERSION="0.10.0"

RUN set -eux; \
curl -s http://archive.apache.org/dist/storm/apache-storm-${STORM_VERSION}/apache-storm-${STORM_VERSION}.tar.gz | tar zxC /opt; \
ln -s /opt/apache-storm-${STORM_VERSION} /opt/storm

COPY storm.yaml /opt/storm/conf/storm.yaml
COPY worker.xml /opt/storm/log4j2/worker.xml
COPY cluster.xml /opt/storm/log4j/cluster.xml

RUN mkdir -p /data

VOLUME /data/storm

ENV PATH="${PATH}:/opt/storm/bin"
