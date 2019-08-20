FROM tomcat:7-jre8-alpine
MAINTAINER John Flavin <jflavin@wustl.edu>

ARG XNAT_ROOT=/data/xnat
ARG XNAT_HOME=/data/xnat/home
ARG TOMCAT_XNAT_FOLDER=ROOT

ADD make-xnat-config.sh /usr/local/bin/make-xnat-config.sh

RUN rm -rf $CATALINA_HOME/webapps/* && \
    mkdir -p $CATALINA_HOME/webapps/${TOMCAT_XNAT_FOLDER} 

ADD xnat-web-1.7.5.3.war $CATALINA_HOME/webapps/${TOMCAT_XNAT_FOLDER}/xnat-web.war

RUN cd $CATALINA_HOME/webapps/ && \
    cd ${TOMCAT_XNAT_FOLDER} && \
    unzip -o xnat-web.war && \
    rm -f xnat-web.war 

EXPOSE 8080
ENV XNAT_HOME=${XNAT_HOME} XNAT_ROOT=${XNAT_ROOT}

CMD ["make-xnat-config.sh", "/usr/local/tomcat/bin/catalina.sh", "run"]
