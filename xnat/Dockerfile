FROM tomcat:7-jre8-alpine
MAINTAINER John Flavin <jflavin@wustl.edu>

ARG XNAT_ROOT=/data/xnat
ARG XNAT_HOME=/data/xnat/home
ARG TOMCAT_XNAT_FOLDER=ROOT
ARG XNAT_VERSION=1.7.5.6

RUN rm -rf $CATALINA_HOME/webapps/* && \
    mkdir -p $CATALINA_HOME/webapps/${TOMCAT_XNAT_FOLDER} 

ADD xnat-web-${XNAT_VERSION}.war $CATALINA_HOME/webapps/${TOMCAT_XNAT_FOLDER}/xnat-web.war

RUN mkdir -p \
      $XNAT_HOME/config \
			$XNAT_HOME/logs \
			$XNAT_HOME/plugins \
			$XNAT_HOME/work \
			$XNAT_ROOT/archive \
			$XNAT_ROOT/build \
			$XNAT_ROOT/cache \
			$XNAT_ROOT/ftp \
			$XNAT_ROOT/pipeline \
			$XNAT_ROOT/prearchive && \
		cd $CATALINA_HOME/webapps/${TOMCAT_XNAT_FOLDER} && \
		unzip -o xnat-web.war && \
		rm -f xnat-web.war 

ADD make-xnat-config.sh /usr/local/bin/make-xnat-config.sh

ADD plugins 

EXPOSE 8080
ENV XNAT_HOME=${XNAT_HOME} XNAT_ROOT=${XNAT_ROOT}

CMD ["make-xnat-config.sh", "/usr/local/tomcat/bin/catalina.sh", "run"]
