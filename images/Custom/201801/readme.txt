dockerfile_list
base_0
FROM       centos:centos7.4.1708
MAINTAINER whb <whb@163.com>
ENV  TIME_ZONE Asia/Shanghai
RUN echo "${TIME_ZONE}" > /etc/timezone && ln -sf /usr/share/zoneinfo/${TIME_ZONE} /etc/localtime 
ADD aliyun-mirror.repo /etc/yum.repos.d/CentOS-Base.repo
ADD aliyun-epel.repo   /etc/yum.repos.d/epel.repo
RUN yum install -y net-tools telnet && yum clean all
#docker push registry.cn-shenzhen.aliyuncs.com/whb/base:0


jdk_7:
FROM  registry.cn-shenzhen.aliyuncs.com/whb/base:0
MAINTAINER whb <whb@163.com>
ENV JAVA_HOME=/usr/local/jdk1.7.0_45
ENV PATH $JAVA_HOME/bin:$PATH
ENV CLASSPATH $JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
ADD jdk1.7.0_45.tar.gz  /usr/local/
ADD  java.security  /usr/local/jdk1.7.0_45/jre/lib/security/java.security
#docker push  registry.cn-shenzhen.aliyuncs.com/whb/jdk:1.7.0.45

jdk_8:
FROM  registry.cn-shenzhen.aliyuncs.com/whb/base:0
MAINTAINER whb <whb@163.com>
ENV JAVA_HOME=/usr/local/jdk1.8.0_151
ENV PATH $JAVA_HOME/bin:$PATH
ENV CLASSPATH $JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
ADD  jdk-8u151-linux-x64.tar.gz  /usr/local/
ADD  java.security  /usr/local/jdk1.8.0_151/jre/lib/security/java.security
#docker push  registry.cn-shenzhen.aliyuncs.com/whb/jdk:1.8.0_151



tomcat7
FROM registry.cn-shenzhen.aliyuncs.com/whb/jdk:1.7.0.45
#FROM registry.cn-shenzhen.aliyuncs.com/whb/jdk:1.8.0_151
MAINTAINER whb <whb@163.com>
ENV CATALINA_HOME /usr/local/tomcat/
ADD apache-tomcat-7.0.61.tar.gz   /usr/local/
RUN ln -sf /usr/local/apache-tomcat-7.0.61 /usr/local/tomcat && cd /usr/local/tomcat/webapps && rm -rf ROOT  docs examples host-manager && mv manager manager7390
ADD server.xml /usr/local/tomcat/conf/
ADD tomcat-users.xml /usr/local/tomcat/conf/
EXPOSE 8080
CMD ["/usr/local/tomcat/bin/catalina.sh", "run"]
#docker push  registry.cn-shenzhen.aliyuncs.com/whb/tomcat7:jdk_1.7.0.45
#docker push  registry.cn-shenzhen.aliyuncs.com/whb/tomcat7:jdk_1.8.0_151

tomcat8
FROM registry.cn-shenzhen.aliyuncs.com/whb/jdk:1.7.0.45
#FROM registry.cn-shenzhen.aliyuncs.com/whb/jdk:1.8.0_151
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

tomcat7_session
FROM registry.cn-shenzhen.aliyuncs.com/whb/jdk:1.7.0.45
#FROM registry.cn-shenzhen.aliyuncs.com/whb/jdk:1.8.0_151
MAINTAINER whb <whb@163.com>
ENV CATALINA_HOME /usr/local/tomcat/
ADD apache-tomcat-7.0.61.tar.gz   /usr/local/
RUN ln -sf /usr/local/apache-tomcat-7.0.61 /usr/local/tomcat && cd /usr/local/tomcat/webapps && rm -rf ROOT  docs examples host-manager && mv manager manager7390
ADD server.xml /usr/local/tomcat/conf/
ADD tomcat-users.xml /usr/local/tomcat/conf/
ADD context.xml /usr/local/tomcat/conf/
ADD lib  /usr/local/tomcat/lib/
EXPOSE 8080
CMD ["/usr/local/tomcat/bin/catalina.sh", "run"]
#docker push  registry.cn-shenzhen.aliyuncs.com/whb/tomcat7:jdk_1.7.0.45_session

FROM  mysql:5.6
MAINTAINER whb
RUN  ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
ADD  my.cnf /etc/mysql/conf.d/
#registry.cn-shenzhen.aliyuncs.com/whb/mysql:5.6

FROM zookeeper:3.4
MAINTAINER whb
ENV  TIME_ZONE Asia/Shanghai
RUN   apk add --no-cache tzdata  &&  echo "${TIME_ZONE}" > /etc/timezone  && ln -sf /usr/share/zoneinfo/${TIME_ZONE} /etc/localtime
#registry.cn-shenzhen.aliyuncs.com/epipe/zookeeper
#registry.cn-shenzhen.aliyuncs.com/whb/dubbo

FROM redis:4-alpine
MAINTAINER Li Yi <denverdino@gmail.com>
ENV  TIME_ZONE Asia/Shanghai
RUN   apk add --no-cache tzdata  &&  echo "${TIME_ZONE}" > /etc/timezone  && ln -sf /usr/share/zoneinfo/${TIME_ZONE} /etc/localtime
#registry.cn-shenzhen.aliyuncs.com/whb/redis

FROM redis:4-alpine
MAINTAINER Li Yi <denverdino@gmail.com>
ENV  TIME_ZONE Asia/Shanghai
RUN   apk add --no-cache tzdata  &&  echo "${TIME_ZONE}" > /etc/timezone  && ln -sf /usr/share/zoneinfo/${TIME_ZONE} /etc/localtime
EXPOSE 26379
ADD sentinel.conf /etc/redis/sentinel.conf
RUN chown redis:redis /etc/redis/sentinel.conf
ENV AUTH_PASS ""
ENV SENTINEL_QUORUM  1
ENV SENTINEL_DOWN_AFTER 5000
ENV SENTINEL_FAILOVER   180000
COPY sentinel-entrypoint.sh /usr/local/bin/
RUN chmod +x /usr/local/bin/sentinel-entrypoint.sh
ENTRYPOINT ["sentinel-entrypoint.sh"]
#registry.cn-shenzhen.aliyuncs.com/whb/sentinel

常用镜像列表 
docker.elastic.co elk官网
registry.cn-shenzhen.aliyuncs.com/kye/elasticsearch-platinum:6.2.4
registry.cn-shenzhen.aliyuncs.com/kye/elasticsearch:6.2.4
