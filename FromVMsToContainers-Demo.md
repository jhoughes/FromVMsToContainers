**Quick Docker Installation (Ubuntu 18.04)**

`sudo apt-get update`

`sudo apt-get install apt-transport-https ca-certificates curl gnupg-agent software-properties-common`

`curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -`

`sudo apt-key fingerprint 0EBFCD88`

`sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"`

`sudo apt-get update`

`sudo apt-get install docker-ce docker-ce-cli containerd.io`



**Basic Docker Examples**
`docker version`

`docker run hello-world`

`docker run -dit --name new_container alpine ash`

`docker ps`

`docker exec -it new_container ping -w4 google.com`

`docker network ls`

`docker inspect new_container`

_NOTE: Get IP of 'new_container' from above and enter it in place of %new_container_IP% below_  
`ping %new_container_IP%`

`docker stop new_container`

`docker ps`

`docker ps -a`

`docker start new_container`

`docker run -d -p 8080:80 --name new_web_server nginx`




**Basic Docker Networking**

`docker network inspect bridge`

`docker network create test_network`

`docker network ls`

`docker network inspect test_network`

`docker run -dit --name pingtest1 --network test_network alpine ash`

`docker run -dit --name pingtest2 --network test_network alpine ash`

`docker network inspect test_network`

`docker container attach pingtest1`

`ping -c 4 pingtest2`

_NOTE: Get IP of 'new_container' from above and enter it in place of %new_container_IP% below_  
`ping -c 4 %new_container_IP%`

_NOTE: Get IP of 'nginx' from above and enter it in place of %nginx_IP% below_  
`ping -c 4 %nginx_IP%`


__Create a Docker image__

`docker run -it ubuntu:18.04 /bin/bash`

`echo 'hello world!' > /message`

`exit`

`docker ps -a`

_NOTE: Get name of image from above and enter it in place of %imagename% below_  
`docker commit %imagename% hello_world_local`

`docker image ls`

`docker run hello_world_local cat /message`

`docker commit --change='CMD ["cat", "/message"]' $(docker ps -lq) hello_world_local:fixed`

`docker run hello_world_local:fixed`
