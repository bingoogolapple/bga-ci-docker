FROM jenkins/jnlp-slave:3.27-1-alpine
LABEL maintainer="bingoogolapple@gmail.com"

ARG JENKINS_AGENT_HOME=/root

ENV JENKINS_AGENT_HOME ${JENKINS_AGENT_HOME}

# setup SSH server
RUN echo "https://mirrors.tuna.tsinghua.edu.cn/alpine/latest-stable/main" > /etc/apk/repositories \
  && echo "https://mirrors.tuna.tsinghua.edu.cn/alpine/latest-stable/community" >> /etc/apk/repositories \
  && apk -U --no-cache --allow-untrusted add bash git openssh

RUN sed -i /etc/ssh/sshd_config \
        -e 's/#PermitRootLogin.*/PermitRootLogin yes/' \
        -e 's/#RSAAuthentication.*/RSAAuthentication yes/'  \
        -e 's/#PubkeyAuthentication.*/PubkeyAuthentication yes/'  \
        -e 's/#PasswordAuthentication.*/PasswordAuthentication no/' \
        -e 's/#SyslogFacility.*/SyslogFacility AUTH/' \
        -e 's/#LogLevel.*/LogLevel INFO/' && \
    mkdir /var/run/sshd

VOLUME "${JENKINS_AGENT_HOME}" "/tmp" "/run" "/var/run"
WORKDIR "${JENKINS_AGENT_HOME}"

COPY setup-sshd /usr/local/bin/setup-sshd

RUN chmod +x /usr/local/bin/setup-sshd

EXPOSE 22

ENTRYPOINT ["setup-sshd"]


# docker build -t jenkins-slave-ssh .
# docker run -d -m 1024M --restart=always --name jenkins-slave-ssh -p 9922:22 -e JENKINS_SLAVE_SSH_PUBKEY="todo" jenkins-slave-ssh
