# Setting up docker-compose for services

## Prerequisites
CentOS 7 || ubuntu 16.04 || Arch || coreOS

## Set up Docker

coreOs all ready comes with docker so it can skip to the next step  
If your on arch just run `pacman -S docker docker-compose`  
For centos and ubuntu follow the instructions below  
Add docker repos and install it
!!!!VERY IMPORTANT NEVER PIPE TO SHELL !!!!!

``` bash
curl -fsSL https://get.docker.com/ >> getdocker.sh
less getdocker.sh
bash getdocker.sh
```
Add docker compose
``` bash
sudo curl -L "https://github.com/docker/compose/releases/download/1.10.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
docker-compose --version
```
You should get `docker-compose version: 1.10.0` or higher

## Set Up services

1. First Create a folder to keep all the files. I suggest `/ect/docker-compose/services/`
  run `sudo mkdir /ect/docker-compose/services/`
2. Add services
  ``` bash
  cd /etc/docker-compose/services
  mkdir nginx
  cd nginx
  docker network create --driver bridge nginx-proxy
  wget https://raw.githubusercontent.com/jwilder/nginx-proxy/master/nginx.tmpl
  wget https://raw.githubusercontent.com/redbrick/admin-training/master/docker/docker-compose.yml
  docker-compose up -d
```

Thats is do to port 443 on your domain and itll be your nginx  
To explain what we did we created a network for all the containers to communicate over then using docker compose the containers where created with the specifications we set in the docker-compose.yml  
We can manage these containers like any other containers with `docker stop` and `docker restart` or use docker-compose, such as the command `docker-compose logs`
