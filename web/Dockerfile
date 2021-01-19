# Dockerfile for building NetXMS webui and websvc

FROM jetty:9

ENV MAJOR=3 MINOR=7 RELEASE=130
ENV VERSION=${MAJOR}.${MINOR}.${RELEASE} NETXMS_SERVER=127.0.0.1 NETXMS_SESSIONTIMEOUT=120 NETXMS_ENABLEADVANCEDSETTINGS=true
ENV WEBAPI_PORT=4701 WEBAPI_USEENCRYPTION=true

COPY ./docker-entrypoint.sh /

RUN echo 'debconf debconf/frontend select Noninteractive' | debconf-set-selections && \
    apt-get update && apt-get -y install curl apt-transport-https && \
    curl -L https://www.netxms.org/download/releases/${MAJOR}.${MINOR}/${VERSION}/nxmc-${VERSION}.war -o /var/lib/jetty/webapps/nxmc.war && \
	curl -L https://www.netxms.org/download/releases/${MAJOR}.${MINOR}/${VERSION}/netxms-websvc-${VERSION}.war -o /var/lib/jetty/webapps/webapi.war && \
    chmod 755 /docker-entrypoint.sh

ENTRYPOINT [ "/docker-entrypoint.sh" ]