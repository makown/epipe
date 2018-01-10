FROM  tomcat:7.0.82-jre8-alpine
MAINTAINER whb <whb@163.com>
ENV  TIME_ZONE Asia/Shanghai
RUN  apk add --no-cache tzdata  &&  echo "${TIME_ZONE}" > /etc/timezone  && ln -sf /usr/share/zoneinfo/${TIME_ZONE} /etc/localtime
ADD  tomcat-users.xml  /usr/local/tomcat/conf/
ADD  server.xml        /usr/local/tomcat/conf/
RUN  rm -rf   /usr/local/tomcat/webapps
ADD  webapps  /usr/local/tomcat/webapps
ADD  java.security  /usr/lib/jvm/java-1.7-openjdk/jre/lib/security/java.security
CMD ["catalina.sh", "run"]
