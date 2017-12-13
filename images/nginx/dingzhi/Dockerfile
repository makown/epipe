FROM registry.cn-shenzhen.aliyuncs.com/epipe/nginx:buiding
RUN  ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
VOLUME   /usr/local/nginx/conf/vhost
VOLUME   /data
EXPOSE 80
STOPSIGNAL SIGTERM
CMD ["nginx"]
