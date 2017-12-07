FROM       mysql:5.6
MAINTAINER whb <whb@163.com>

ENV TZ "Asia/Shanghai"
ENV TERM xterm
ADD  master.cnf   /etc/mysql/conf.d/master.cnf

#ENTRYPOINT ["docker-entrypoint.sh"]

CMD ["mysqld"]  
