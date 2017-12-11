FROM  tomcat:8.5.23-jre8-alpine
#FROM  tomcat:7.0.82-jre7
MAINTAINER whb <whb@163.com>
ENV  TIME_ZONE Asia/Shanghai
RUN   apk add --no-cache tzdata  &&  echo "${TIME_ZONE}" > /etc/timezone  && ln -sf /usr/share/zoneinfo/${TIME_ZONE} /etc/localtime
ADD  server.xml  /usr/local/tomcat/conf/
ADD  tomcat-users.xml  /usr/local/tomcat/conf/
RUN  rm -rf  /usr/local/tomcat/webapps
ADD  webapps  /usr/local/tomcat/webapps
CMD ["catalina.sh", "run"]

