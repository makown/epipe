FROM       basic:v1
MAINTAINER whb <whb@163.com>

ENV JAVA_HOME=/jdk/jdk1.8.0_151
ENV PATH $JAVA_HOME/bin:$PATH
ENV CLASSPATH $JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
ENV CATALINA_HOME /tomcat/apache-tomcat-8.0.23
ADD jdk-8u151-linux-x64.tar.gz  /jdk
ADD apache-tomcat-8.0.23.tar.gz   /tomcat
ADD     supervisor_tomcat.conf  /etc/supervisor.conf.d/tomcat.conf
EXPOSE 8080

ENTRYPOINT ["/usr/bin/supervisord", "-n", "-c", "/etc/supervisord.conf"]
