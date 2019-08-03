FROM tomcat:7-jre8-alpine
MAINTAINER John Flavin <jflavin@wustl.edu>

ARG XNAT_WAR_FILE=xnat-web-1.7.5.3.war
ARG XNAT_ROOT=/data/xnat
ARG XNAT_HOME=/data/xnat/home

RUN rm -rf $CATALINA_HOME/webapps/* && \
    mkdir -p \
        $CATALINA_HOME/webapps/${TOMCAT_XNAT_FOLDER} \
        ${XNAT_HOME}/config \
        ${XNAT_HOME}/logs \
        ${XNAT_HOME}/plugins \
        ${XNAT_HOME}/work \
        ${XNAT_ROOT}/archive \
        ${XNAT_ROOT}/build \
        ${XNAT_ROOT}/cache \
        ${XNAT_ROOT}/ftp \
        ${XNAT_ROOT}/pipeline \
        ${XNAT_ROOT}/prearchive 

ADD ${XNAT_WAR_FILE} ${CATALINA_HOME}/webapps/${TOMCAT_XNAT_FOLDER}

run cd ${CATALINA_HOME}/webapps/${TOMCAT_XNAT_FOLDER} && \
    unzip -o ${XNAT_WAR_FILE} && \
		rm ${XNAT_WAR_FILE}

COPY make-xnat-config.sh /usr/local/bin/make-xnat-config.sh
COPY wait-for-postgres.sh /usr/local/bin/wait-for-postgres.sh

RUN apk add --no-cache postgresql-client

EXPOSE 8080
ENV XNAT_HOME=${XNAT_HOME} XNAT_DATASOURCE_USERNAME=${XNAT_DATASOURCE_USERNAME}

CMD ["make-xnat-config.sh", "/usr/local/tomcat/bin/catalina.sh", "run"]
