FROM       mysql:5.6
MAINTAINER whb <whb@163.com>

ENV TZ "Asia/Shanghai"
ENV TERM xterm
ADD  slave.cnf   /etc/mysql/conf.d/slave.cnf

#ENTRYPOINT ["docker-entrypoint.sh"]

CMD ["mysqld"]  
