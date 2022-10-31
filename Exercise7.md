## Triton Cloud Platform -Episode 1


**Preliminary task - Generation of SSH keys**  

on Ubuntu Server 01 
```
mkdir ~/.ssh
chmod 700 ~/.ssh
ssh-keygen -t rsa
```

on Windows power shell 
```
ps> cd /Temp
ps> sftp username@111.111.11.11
sftp> cd .ssh
sftp> get id_rsa.pub
sftp> bye
```

on Ubuntu Server 01
```
sudo poweroff
```

**Installation of Triton cloud platform**  - I cannot do this on my computer  

on Windows side -this might unnecessary in case using school computer    
download Triton ISO file save to C:\Temp  
configure the network setting of VMware Workstation    

create virtual machine  
Triton_Coal MEM 8GB, CPU 2, HD 80GB, OS Solaris 11 64 bit, ....   

boot and configure Head node  

take a screenshot from Triton Setup -verify configuration menu

----- I hope you can manage this ----  

<br>
<br>



**Installation of Triton CLI tool**

on Ubuntu Server 01  

install Triton CLI tool (not defined environment variables)  

```
sudo apt update
sudo apt upgrade
sudo apt install npm
sudo npm install -g triton
npm install -g triton
sudo npm install -g triton
```

configure Triton profiles  

```
pwd
triton -i profile create
  name: fi-tuni-01
  url: https://10.88.88.XX --> XX?
  account: ugkim
  keyid: 6c:84:dc:ce:ea:cf:8trtrd:77:de:32:fb:5f:83:71:47:b2

trion -i info
```

<br>


**Triton CLI tool -Running instances on Triton cloud platform**





