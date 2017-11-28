FROM       basic:v1
MAINTAINER whb <whb@163.com>


ADD  pcre-8.39.tar.gz /usr/local/src/
ADD  nginx-1.10.2.tar.gz   /usr/local/src/
RUN  yum install openssl openssl-devel -y && groupadd www && useradd -s /sbin/nologin -g www www && cd /usr/local/src/nginx-1.10.2  && ./configure --user=www --group=www --prefix=/usr/local/nginx --with-http_stub_status_module --with-http_ssl_module --with-http_v2_module  --with-http_gzip_static_module --with-ipv6 --with-http_sub_module --with-http_realip_module  --with-http_addition_module  --with-pcre=/usr/local/src/pcre-8.39 && make && make install &&  mkdir -p /usr/local/nginx/conf/vhost
ADD  supervisor_nginx.conf  /etc/supervisor.conf.d/nginx.conf
ADD  conf   /usr/local/nginx/conf
EXPOSE 80
ENTRYPOINT ["/usr/bin/supervisord", "-n", "-c", "/etc/supervisord.conf"]
