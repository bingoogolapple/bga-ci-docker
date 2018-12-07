# BGA-CI-Docker

## jenkins-master

```shell
docker stop jenkins-master && docker rm jenkins-master && docker volume rm jenkins-master-home

docker rmi jenkins-master

docker build --file jenkins-master/Dockerfile -t jenkins-master .

docker run -d -m 512M --name jenkins-master -v jenkins-master-home:/var/jenkins_home -v /var/run/docker.sock:/var/run/docker.sock -p 8010:8080 -p 50010:50000 jenkins-master

docker exec -it jenkins-master bash

docker logs jenkins-master
```

## jenkins-slave-jnlp

```shell
docker stop jenkins-slave1 && docker rm jenkins-slave1

docker rmi jenkins-slave-jnlp
docker build --file jenkins-slave-jnlp/Dockerfile -t jenkins-slave-jnlp .

docker run -d -m 128M --name jenkins-slave1 -v /var/run/docker.sock:/var/run/docker.sock --env JENKINS_AGENT_WORKDIR=/home/jenkins/agent --env JENKINS_URL=http://ci.bingoogolapple.cn --env JENKINS_TUNNEL=ci.bingoogolapple.cn:50010 --env JENKINS_SECRET=427e94dd18c32a7a0bc0d3da26a5ed8f3993c055b020b8ed32547c3125270b9e --env JENKINS_AGENT_NAME=jenkins-slave1 jenkins-slave-jnlp

docker exec -it jenkins-slave1 bash

docker logs jenkins-slave1
```