FROM       centos:centos7.4.1708
MAINTAINER whb <whb@163.com>
ENV  TIME_ZONE Asia/Shanghai
RUN echo "${TIME_ZONE}" > /etc/timezone && ln -sf /usr/share/zoneinfo/${TIME_ZONE} /etc/localtime 
ADD aliyun-mirror.repo /etc/yum.repos.d/CentOS-Base.repo
ADD aliyun-epel.repo   /etc/yum.repos.d/epel.repo
RUN yum install -y net-tools telnet && yum clean all
#docker push registry.cn-shenzhen.aliyuncs.com/whb/base:0
