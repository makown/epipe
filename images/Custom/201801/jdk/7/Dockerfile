FROM  registry.cn-shenzhen.aliyuncs.com/whb/base:0
MAINTAINER whb <whb@163.com>
ENV JAVA_HOME=/usr/local/jdk1.7.0_45
ENV PATH $JAVA_HOME/bin:$PATH
ENV CLASSPATH $JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
ADD jdk1.7.0_45.tar.gz  /usr/local/
ADD  java.security  /usr/local/jdk1.7.0_45/jre/lib/security/java.security
#docker push  registry.cn-shenzhen.aliyuncs.com/whb/jdk:1.7.0.45
