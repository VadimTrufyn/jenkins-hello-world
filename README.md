# jenkins-hello-world
Project for practicing jenkins + docker container

Step1. build image BlueOcean 
docker build -t myjenkins-blueocean:2.414.2 .


Step2. create network
docker network create jenkins


docker run --name jenkins-blueocean --restart=on-failure --detach \
  --network jenkins --env DOCKER_HOST=tcp://docker:2376 \
  --env DOCKER_CERT_PATH=/certs/client --env DOCKER_TLS_VERIFY=1 \
  --publish 8088:8080 --publish 50000:50000 \
  --volume jenkins-data:/var/jenkins_home \
  --volume jenkins-docker-certs:/certs/client:ro \
  myjenkins-blueocean:2.414.2


#use 8088, because in my case 8080 used by VM jenkins


