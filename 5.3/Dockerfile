FROM debian:jessie

MAINTAINER Andrea Usuelli <andrea.usuelli@prima.it>

ENV FILEBEAT_VERSION=5.3.0 \
    FILEBEAT_SHA1=c6f56d1a938889ec9f5db7caea266597f625fcc1

RUN set -x && \
  apt-get update && \
  apt-get install -y wget && \
  wget https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-${FILEBEAT_VERSION}-linux-x86_64.tar.gz -O /opt/filebeat.tar.gz && \
  cd /opt && \
  echo "${FILEBEAT_SHA1}  filebeat.tar.gz" | sha1sum -c - && \
  tar xzvf filebeat.tar.gz && \
  cd filebeat-* && \
  cp filebeat /bin && \
  cd /opt && \
  rm -rf filebeat* && \
  apt-get purge -y wget && \
  apt-get autoremove -y && \
  apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

COPY docker-entrypoint.sh /
ENTRYPOINT ["/docker-entrypoint.sh"]
CMD [ "filebeat", "-e" ]
