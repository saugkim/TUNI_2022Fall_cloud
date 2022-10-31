## Triton Cloud Platform

**Preliminary task**

<br>


**Installation Triton Docker Cli**

on Ubuntu Server 01  
1-4.  

5.Install Triton Docker CLI tool

```
triton -i env fi-tuni-01
triton -i profile docker-setup fi-tuni-01 
  yes
triton -i env --docker fi-tuni-01 >> ~/.profile
sudo bash -c 'curl -o /usr/local/bin/triton-docker https://raw.githubusercontent.com/joyent/triton-docker-cli/master/triton-docker && chmod +x /usr/local/bin/triton-docker && ln -Fs /usr/local/bin/triton-docker /usr/local/bin/triton-compose && ln -Fs /usr/local/bin/triton-docker /usr/local/bin/triton-docker-install'
sudo triton-docker-install

triton-docker info

sudo poweroff
re-open connection
```

6.Test the configuration and installation of Triton Docker CLI tool. Type the following commands. Take a
screenshot and paste the image to appendix one. We use Docker's TLS authentication. Use flag “--tls”
to accept secure connections. Do not care about message “error (DEPTH_ZERO_SELF_SIGNED_CERT)”
etc.

```
clear
triton-docker --tls info
```
<br>
<br>

**Triton Docker CLI – Running Docker containers on Triton cloud platform**

```
triton docker cli
```
<br>


**Triton Docker CLI – Running Gauntlet on Triton cloud platform**

https://tritondatacenter.com/blog/video-training-dockerize-applications

on Ubuntu Server 01
```
git clone https://github.com/jakesgordon/javascript-gauntlet.git
ls 
cd javascript-gauntlet

touch Dockerfile
nano Dockerfile

#FROM is the base image for which we will run our application
FROM nginx:latest

# Copy files and directories from the application
COPY index.html /usr/share/nginx/html
COPY Rakefile /usr/share/nginx/html
COPY Gemfile /usr/share/nginx/html
COPY Gemfile.lock /usr/share/nginx/html
COPY LICENSE /usr/share/nginx/html
COPY README.md /urs/share/nginx/html
COPY css/ /usr/share/nginx/html/css/
COPY images/ /usr/share/nginx/html/images/
COPY js/ /usr/share/nginx/html/js/
COPY levels/ /usr/share/nginx/html/levels/
COPY sounds/ /usr/share/nginx/html/sounds/

# Tell Docker we are going to use this port
EXPOSE 80

exit from nano

docker build -t GauntletImage:latest .
  
triton-docker run -d -p 80 --name gauntletContainer GauntletImage

```





