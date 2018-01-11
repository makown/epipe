#FROM registry.cn-shenzhen.aliyuncs.com/whb/jdk:1.7.0.45
FROM registry.cn-shenzhen.aliyuncs.com/whb/jdk:1.8.0_151
MAINTAINER whb <whb@163.com>
ENV CATALINA_HOME /usr/local/tomcat/
ADD apache-tomcat-8.5.24.tar.gz   /usr/local/
RUN ln -sf /usr/local/apache-tomcat-8.5.24 /usr/local/tomcat && cd /usr/local/tomcat/webapps && rm -rf ROOT  docs examples host-manager && mv manager manager7390
ADD server.xml /usr/local/tomcat/conf/
ADD tomcat-users.xml /usr/local/tomcat/conf/
RUN sed -i  '/allow=/c allow="^.*$" />' /usr/local/tomcat/webapps/manager7390/META-INF/context.xml
EXPOSE 8080
CMD ["/usr/local/tomcat/bin/catalina.sh", "run"]
#docker push  registry.cn-shenzhen.aliyuncs.com/whb/tomcat8:jdk_1.7.0.45
#docker push  registry.cn-shenzhen.aliyuncs.com/whb/tomcat8:jdk_1.8.0_151
