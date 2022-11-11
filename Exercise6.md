## Operating system level container 


**Connecting LXD container to the LAN**


1. Create a new LXD profile and use maclan to connect container to the LAN. Then, launch Ubuntu 20.04 container under the new profile. Name the new container to Minetest. Read installation instructions from the [link](https://blog.simos.info/how-to-make-your-lxd-container-get-ip-addresses-from-your-lan/). Check that Minetest container is on the same LAN as Ubuntu host.  
```
lxc profile list
lxc profile create maclan
ip route show default 0.0.0.0/0
    default via X.X.X.X dev ens33 proto dhcp src x.x.x.x metric 100
    
lxc profile device add maclan eth0 nic nictype-maclan parent=??
   error: eth0 upsupported device type

lxc profile show maclan

lxc launch ubuntu:20.04 Minetest --profile default --profile maclan
lxc list
lxc exet Minetest -- ping -c 3 IPV4
  error: 
```

2. You cannot connect from Ubuntu host to Minetest container because netplan does not support macvlan interface. This is confusing, but you can connect to Minetest container from the desktop PC and other virtual instances in same the LAN.

3. Move into Ubuntu 20.04 container and install Minetest server. Minetest is an open source version of Minecraft. Read installation instructions from the link. Note the following refinements.

```
lxc shell Minetest

step 0
apt update
apt install wget
apt install nano
apt install software-properties-common

step 1
add-apt-repository ppa:minetestdevs/stable
apt update
apt install minetest

setp 2
useradd -mU minetest
ufw allow 30000
su minetest
  $ minetest --server
  $ Control+C --> stop server
  $ exit   

step 3
cd /home/minetest
wget https://raw.githubusercontent.com/minetest/minetest/master/minetest.conf.example
mv minetest.conf.example minetest.conf
nano minetest.conf
   server_name = Minetest server
   server_description = Welcome to my Minetest Server
   bind_address = ubuntu IP address here (which I failed to get proper one)
   prot = 30000
   exit from nano

step 4
cd
cat > /etc/systemd/system/minetest.service

[Unit]
Description=Minetest Server
After=network.target

[Service]
Type=simple
User=minetest
Group=minetest
WorkingDirectory=/home/minetest
ExecStart=/usr/bin/minetest --server
Restart=on-abort

[Install]
WantedBy=multi-user.target

Control+C to exit from editing

systemctl enable minetest.service
systemctl start minetest.service
```

4. Download (on Windows)  
5. on Windows edit minetest.conf  
6. on Windows launch Minetest client and open Join game tab  
7. on Windows play the game  
8. on Game press Esc key and take screenshot  
9. on Game climb the ...  

10. on Ubuntu Server still inside the lxc shell 
```
head --lines=100 /home/minetest/.minetest/debug.txt
```


 
