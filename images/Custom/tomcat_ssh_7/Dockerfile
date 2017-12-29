FROM registry.cn-hangzhou.aliyuncs.com/whb/basic:v1
MAINTAINER whb <whb@163.com>
ENV JAVA_HOME=/usr/local/jdk1.7.0_45
ENV PATH $JAVA_HOME/bin:$PATH
ENV CLASSPATH $JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
ENV CATALINA_HOME /usr/local/tomcat/
ADD jdk1.7.0_45.tar.gz  /usr/local/
ADD tomcat.tar.gz   /usr/local/
ADD     supervisor_tomcat.conf  /etc/supervisor.conf.d/tomcat.conf
EXPOSE 8080
ENTRYPOINT ["/usr/bin/supervisord", "-n", "-c", "/etc/supervisord.conf"]
