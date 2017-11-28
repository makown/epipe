FROM  tomcat:7.0.82-jre7
MAINTAINER whb <whb@163.com>
ADD  server.xml  /usr/local/tomcat/conf/
ADD  tomcat-users.xml  /usr/local/tomcat/conf/
RUN  rm -rf  /usr/local/tomcat/webapps
ADD  webapps  /usr/local/tomcat/webapps
CMD ["catalina.sh", "run"]

