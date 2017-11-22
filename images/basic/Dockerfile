FROM       centos:centos7.4.1708
MAINTAINER whb <whb@163.com>

ENV TZ "Asia/Shanghai"
ENV TERM xterm

ADD aliyun-mirror.repo /etc/yum.repos.d/CentOS-Base.repo
ADD aliyun-epel.repo   /etc/yum.repos.d/epel.repo

RUN yum install -y curl wget tar bzip2 unzip vim-enhanced passwd sudo yum-utils hostname net-tools rsync man && \
    yum install -y gcc gcc-c++ git make automake cmake patch logrotate python-devel libpng-devel libjpeg-devel openssh-server  && \
    yum install -y --enablerepo=epel pwgen python-pip && \
    yum clean all

RUN pip install supervisor
ADD supervisord.conf /etc/supervisord.conf
RUN mkdir -p /etc/supervisor.conf.d && \
    mkdir -p /var/log/supervisor

#取消pam限制
RUN sed -i 's/session    required     pam_loginuid.so/#session    required     pam_loginuid.so/g'  /etc/pam.d/sshd
#将密钥文件复制到/etc/ssh/目录中
ADD ssh_host_rsa_key /etc/ssh/ssh_host_rsa_key
ADD ssh_host_ecdsa_key /etc/ssh/ssh_host_ecdsa_key
ADD ssh_host_ed25519_key /etc/ssh/ssh_host_ed25519_key
RUN chmod 600  /etc/ssh/ssh_host* && mkdir -p /root/.ssh  && mkdir -p /var/run/sshd
ADD authorized_keys /root/.ssh/authorized_keys
RUN echo "root:abcd1234*"|chpasswd
ADD     supervisor_sshd.conf  /etc/supervisor.conf.d/sshd.conf
EXPOSE 22

ENTRYPOINT ["/usr/bin/supervisord", "-n", "-c", "/etc/supervisord.conf"]
