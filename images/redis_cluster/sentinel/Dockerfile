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
