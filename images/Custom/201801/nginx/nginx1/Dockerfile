#nginx:1.12_1
FROM registry.cn-shenzhen.aliyuncs.com/whb/nginx:1.12_0
MAINTAINER whb <whb@163.com>
ENV  TIME_ZONE Asia/Shanghai
RUN  apk add --no-cache tzdata  &&  echo "${TIME_ZONE}" > /etc/timezone  && ln -sf /usr/share/zoneinfo/${TIME_ZONE} /etc/localtime && mkdir -p /app/vhost && mkdir -p /app/data && mkdir -p /app/logs && chown -R nginx:nginx /app
ADD  conf /etc/nginx/
CMD ["nginx", "-g", "daemon off;"]
#docker push registry.cn-shenzhen.aliyuncs.com/whb/nginx:1.12_1
