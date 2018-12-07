FROM jenkins/jnlp-slave:3.27-1-alpine
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