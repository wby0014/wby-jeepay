FROM eclipse-temurin:17

ENV ACTIVEMQ_VERSION 5.16.4
ENV ACTIVEMQ apache-activemq-$ACTIVEMQ_VERSION
ENV ACTIVEMQ_HOME /opt/activemq

RUN apt-get update && \
    apt-get install -y curl && \
    rm -rf /var/lib/apt/lists/* && \
    mkdir -p /opt && \
    curl -s -S https://archive.apache.org/dist/activemq/${ACTIVEMQ_VERSION}/${ACTIVEMQ}-bin.tar.gz | tar -xz -C /opt && \
    ln -s /opt/${ACTIVEMQ} ${ACTIVEMQ_HOME} && \
    groupadd -r activemq && \
    useradd -r -g activemq -d ${ACTIVEMQ_HOME} -s /sbin/nologin activemq && \
    chown -R activemq:activemq /opt/${ACTIVEMQ} && \
    chown -h activemq:activemq ${ACTIVEMQ_HOME}

COPY ./activemq.xml ${ACTIVEMQ_HOME}/conf/activemq.xml

EXPOSE 1883 5672 8161 61613 61614 61616

USER activemq
WORKDIR ${ACTIVEMQ_HOME}

CMD ["bin/activemq", "console"]
