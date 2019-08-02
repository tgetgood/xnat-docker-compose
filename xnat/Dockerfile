FROM tomcat:7-jre8-alpine
MAINTAINER John Flavin <jflavin@wustl.edu>

ARG XNAT_WAR_FILE
ARG XNAT_ROOT=/data/xnat
ARG XNAT_HOME=/data/xnat/home
ARG XNAT_DATASOURCE_DRIVER=org.postgresql.Driver
ARG XNAT_DATASOURCE_URL=jdbc:postgresql://xnat-db/xnat
ARG XNAT_DATASOURCE_USERNAME=xnat
ARG XNAT_DATASOURCE_PASSWORD=xnat
ARG XNAT_HIBERNATE_DIALECT=org.hibernate.dialect.PostgreSQL9Dialect
ARG TOMCAT_XNAT_FOLDER=ROOT
ARG SMTP_ENABLED=false
ARG SMTP_HOSTNAME=fake.fake
ARG SMTP_PORT
ARG SMTP_AUTH
ARG SMTP_USERNAME
ARG SMTP_PASSWORD

COPY make-xnat-config.sh /usr/local/bin/make-xnat-config.sh
COPY ${XNAT_WAR_FILE} /opt/xnat.war

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
        ${XNAT_ROOT}/prearchive \
    && \
    cd ${CATALINA_HOME}/webapps/ && \
    cd ${TOMCAT_XNAT_FOLDER} && \
    unzip -o /opt/xnat.war && \
    rm -f /opt/xnat.war

EXPOSE 8080
ENV XNAT_HOME=${XNAT_HOME} XNAT_DATASOURCE_USERNAME=${XNAT_DATASOURCE_USERNAME}

CMD ["make-xnat-config.sh", "/usr/local/tomcat/bin/catalina.sh", "run"]
