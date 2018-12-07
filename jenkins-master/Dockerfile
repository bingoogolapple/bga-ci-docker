FROM jenkins/jenkins:2.154-alpine
LABEL maintainer="bingoogolapple@gmail.com"

USER root

# https://wiki.alpinelinux.org/wiki/Docker
# Alpine 使用清华大学镜像
# RUN echo "https://mirrors.tuna.tsinghua.edu.cn/alpine/latest-stable/main" > /etc/apk/repositories \
#   && echo "https://mirrors.tuna.tsinghua.edu.cn/alpine/latest-stable/community" >> /etc/apk/repositories \
#   && apk -U --no-cache --allow-untrusted add docker py-pip openrc \
#   && pip install --upgrade pip \
#   && pip install docker-compose \
#   && rc-update add docker boot

# dind 不需要设置开机启动
RUN echo "https://mirrors.tuna.tsinghua.edu.cn/alpine/latest-stable/main" > /etc/apk/repositories \
  && echo "https://mirrors.tuna.tsinghua.edu.cn/alpine/latest-stable/community" >> /etc/apk/repositories \
  && apk -U --no-cache --allow-untrusted add docker py-pip \
  && pip install --upgrade pip \
  && pip install docker-compose

# Jenkins Update Center 使用清华大学镜像 https://mirrors.tuna.tsinghua.edu.cn/jenkins/updates/current/update-center.json
# RUN sed -i -e "s/https:\/\/updates.jenkins.io/https:\/\/mirrors.tuna.tsinghua.edu.cn\/jenkins\/updates\/current\/" /var/jenkins_home/hudson.model.UpdateCenter.xml