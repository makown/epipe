FROM  tomcat:7.0.82-jre7-alpine
MAINTAINER whb <whb@163.com>
#ADD  server.xml  /usr/local/tomcat/conf/
ENV  TIME_ZONE Asia/Shanghai
RUN   apk add --no-cache tzdata  &&  echo "${TIME_ZONE}" > /etc/timezone  && ln -sf /usr/share/zoneinfo/${TIME_ZONE} /etc/localtime
ADD  tomcat-users.xml  /usr/local/tomcat/conf/
RUN  rm -rf  /usr/local/tomcat/webapps
ADD  webapps  /usr/local/tomcat/webapps
CMD ["catalina.sh", "run"]

