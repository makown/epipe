FROM  registry.cn-shenzhen.aliyuncs.com/whb/base:0
MAINTAINER whb <whb@163.com>
ENV JAVA_HOME=/usr/local/jdk1.8.0_151
ENV PATH $JAVA_HOME/bin:$PATH
ENV CLASSPATH $JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
ADD  jdk-8u151-linux-x64.tar.gz  /usr/local/
ADD  java.security  /usr/local/jdk1.8.0_151/jre/lib/security/java.security
#docker push  registry.cn-shenzhen.aliyuncs.com/whb/jdk:1.8.0_151
