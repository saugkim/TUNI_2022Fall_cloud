## Application level containers


**Docker containers**

install docker 
```
sudo apt update
sudo apt upgrade

sudo apt install apt-transport-https ca-certificates curl software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"
apt-cache policy docker-ce
sudo apt install docker-ce

sudo systemctl status docker

docker ps
docker start <container name>
docker stop <container name>
docker rm <container name>

```
<br>
avoiding sudo

```
sudo usermod -aG docker ${USER}
su - ${USER}
groups

sudo usermod -aG docker myusernamehere
```


https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-20-04  

<br>

**WordPress installation with Docker**

```
curl -V

# MariaDB in a container
mkdir ~/wordpress && cd ~/wordpress
docker run -e MYSQL_ROOT_PASSWORD=1234 -e MYSQL_DATABASE=wordpress --name wordpressdb -v "$PWD/database":/var/lib/mysql -d mariadb:latest

# wordpress
docker pull wordpress
docker run -e WORDPRESS_DB_USER=root -e WORDPRESS_DB_PASSWORD=1234 --name wordpress --link wordpressdb:mysql -p 80:80 -v "$PWD/html":/var/www/html -d wordpress

```  
https://upcloud.com/resources/tutorials/wordpress-with-docker#point-2



http://192.168.59.128/admin

