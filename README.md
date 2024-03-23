# jenkins-hello-world
this is not my own project, i just follow devopsjouerney1
Project for practicing jenkins + docker container

Step1. build image BlueOcean 
docker build -t myjenkins-blueocean:2.414.2 .


Step2. create network
docker network create jenkins

Step3. Run container
docker run --name jenkins-blueocean --restart=on-failure --detach \
  --network jenkins --env DOCKER_HOST=tcp://docker:2376 \
  --env DOCKER_CERT_PATH=/certs/client --env DOCKER_TLS_VERIFY=1 \
  --publish 8088:8080 --publish 50000:50000 \
  --volume jenkins-data:/var/jenkins_home \
  --volume jenkins-docker-certs:/certs/client:ro \
  myjenkins-blueocean:2.414.2


#use 8088, because in my case 8080 used by VM jenkins


Step4. Get admin pass
 docker exec f7d55bf71889 cat /var/jenkins_home/secrets/initialAdminPassword


Step5. alpine/socat container to forward traffic from Jenkins to Docker Desktop on Host Machine
https://stackoverflow.com/questions/47709208/how-to-find-docker-host-uri-to-be-used-in-jenkins-docker-plugin


docker run -d --restart=always -p 127.0.0.1:2376:2375 --network jenkins -v /var/run/docker.sock:/var/run/docker.sock alpine/socat tcp-listen:2375,fork,reuseaddr unix-connect:/var/run/docker.sock
docker inspect <container_id> | grep IPAddress


tcp://172.18.0.3:2375



devopsjourney1/myjenkinsagents:python
 

 
