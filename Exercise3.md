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

```
MariaDB Environment variables are marked in the Docker command with -e:
-e MYSQL_ROOT_PASSWORD= Set your own password here.
-e MYSQL_DATABASE= Creates and names a new database e.g. wordpress.

Docker parameters:
–name wordpressdb – Names the container.
-v “$PWD/database”:/var/lib/mysql – Creates a data directory linked to the container storage to ensure data persistence.
-d – Tells Docker to run the container in daemon.
mariadb:latest – Finally defines what to install and which version.

WordPress container also takes environment variables and Docker parameters:
-e WORDPRESS_DB_PASSWORD= Set the same database password here.
–name wordpress – Gives the container a name.
–link wordpressdb:mysql – Links the WordPress container with the MariaDB container so that the applications can interact.
-p 80:80 – Tells Docker to pass connections from your server’s HTTP port to the containers internal port 80.
-v “$PWD/html”:/var/www/html – Sets the WordPress files accessible from outside the container. The volume files will remain even if the container was removed.
-d – Makes the container run on background
wordpress – Tells Docker what to install. Uses the package downloaded earlier with the docker pull wordpress -command.

```


http://192.168.59.128/admin

