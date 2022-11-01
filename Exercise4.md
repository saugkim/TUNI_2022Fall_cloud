## Docker Compose

Take a snapshot as "Snapshot 4"

**ownCloud** 

```
sudo apt update
sudo apt upgrade
sudo apt install docker compose
docker compose version
    - v2.12.2

mkdir owncloud-docker-server
cd owncloud-docker-server

ifconfig ens33 
    - 192.168.59.128  

wget https://raw.githubusercontent.com/owncloud/docs-server/master/modules/admin_manual/examples/installation/docker/docker-compose.yml

cat << EOF > .env
OWNCLOUD_VERSION=10.11
OWNCLOUD_DOMAIN=192.168.59.128:8080
OWNCLOUD_TRUSTED_DOMAINS=192.168.59.128
ADMIN_USERNAME=admin
ADMIN_PASSWORD=admin
HTTP_PORT=8080
EOF

docker-compose up -d

docker-compose ps

```

https://docs.docker.com/compose/install/  
https://doc.owncloud.com/server/10.11/admin_manual/installation/docker/#docker-compose  

```
sudo -i
updatedb
locate test1_own_capturing1.PNG
  - /var/lib/docker/volumes/owncloud-docker-server_files/_data/files/username/files/Photos
```

<br>



<br>

**ClamAV installation**

```
sudo docker pull clamav/clamav
sudo docker run --interactive --tty --rm clamav/clamav
sudo docker run -d -p 3310:3310 clamav/clamav

sudo docker run -d -p 3310:3310 mkodockx/docker-clamav:buster-slim

sudo docker ps

sudo docker stop youthful_gagarin
sudo docker stop owncloud_server
sudo docker stop owncloud_mariadb
sudo docker stop owncloud_redis

sudo docker-compose down

sudo poweroff
```

https://hub.docker.com/r/clamav/clamav  
https://mko-x.github.io/docker-clamav/  

<br> 

**Testing of ClamAV**

download ClamAV virus file  
https://github.com/eagleas/clamav/blob/master/spec/clamav-testfiles/clam.exe

```
clear
docker ps
docker logs name_of_clamav_container | tail
```

