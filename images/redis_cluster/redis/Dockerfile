FROM redis:4-alpine
MAINTAINER Li Yi <denverdino@gmail.com>
ENV  TIME_ZONE Asia/Shanghai
RUN   apk add --no-cache tzdata  &&  echo "${TIME_ZONE}" > /etc/timezone  && ln -sf /usr/share/zoneinfo/${TIME_ZONE} /etc/localtime
