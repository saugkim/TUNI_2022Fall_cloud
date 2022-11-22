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
<br>

**Installation of Triton cloud platform**  - I cannot do this on my computer  
<br>
*Pre-installation procedures*  

on Windows side -this might unnecessary in case using school computer    

1. download Triton ISO file save to C:\Temp  
link https://filesender.funet.fi/?s=download&token=74b27791-94e3-4adc-a265-a2e3488cf432


2. configure the network settings of VMware Workstation. Read installation instructions from the link (Downloading CoaL;  https://github.com/TritonDataCenter/triton/blob/master/docs/developer-guide/coal-setup.md#downloading-coal). Configure external and admin networks.

```
PS# wget https://raw.githubusercontent.com/joyent/triton/master/tools/coal-windows-vmware-setup.bat -OutFile coal-windows-vmware-setup.bat
```

3. create virtual machine  
Triton_Coal  
MEM: 16GB, CPU: 2, HD: 80GB, OS: Solaris 11 64 bit, Network Adapter: Nat, Network Adapter 2: Host-only.   

*Installation*

4. boot and configure Head Node. Read installation instructions from the link (Booting the head node;  https://github.com/TritonDataCenter/triton/blob/master/docs/developer-guide/coal-setup.md#booting-the-head-node). Follow instructions but make the following changes in configuration phase.

    • Company Name: Tampere University  
    • Data center region: tuni-cloud  
    • Data center name: coal-01  
    • City and state: Tampere, Pirkanmaa  
    • NTP Server: time.mikes.fi  
    • admin interface: 2  
    • (admin) headnode IP address: 10.99.99.7  
    • Add external network now? Y  
    • 'external' interface: 1  
    • (external) headnode IP address: 10.99.99.200  
    • (external) gateway IP address: 10.99.99.2  
    • Head node domain name: example.com  
    • DNS Search Domain: example.com  
    • Set root password: rootpass  
    • Set admin password: adminpass1  
    • Default channel: release  
    
5. Take a screenshot from "Triton Setup - Verify Configuration" menu. Add the image to appendix 1.

6. Finally, verify settings and confirm configuration.     
 
7. The installation process takes 25-40 minutes. Installation is not complete until the Setup complete message displays (Source).  


*Post-installation procedures*

8. Open a SSH connection to Head Node.  
```
PS# ssh root@10.88.88.200
mac# ssh root@10.88.88.200
```

9. Perform the post-installation procedures. Read installation instructions from the link (Testing and Developing). Skip instructions on chapter “Maintaining CoaL”.
https://github.com/TritonDataCenter/triton/blob/master/docs/developer-guide/coal-setup.md#testing-and-developing  

```
#Root Access
ssh root@10.88.88.200  (#password 'rootpass')

#Health checks
#To confirm the health of the services:
sdcadm health

#Adding external Nics
#To add external nics to imgapi and adminui:
sdcadm post-setup common-external-nics
-- Added external nic to adminui
-- Added external nic to imgapi

#To confirm which services have an external IP, run sdc-vmapi
sdc-vmapi /vms?state=running | json -H -ga alias nics.0.ip nics.1.ip

#To test whether you can access the AdminUI via the external IP address, in a web browser on the host computer, navigate to https://10.88.88.3.

#Setting up CloudAPI for development

#CloudAPI provides the self-serve API access to Triton. If you are developing or testing against CloudAPI, you can install it by running:

sdcadm post-setup cloudapi
-- cloudapi0 zone created

# If you plan to use CloudAPI in CoaL and to provision VMs, you will need to enable the head node to act as a compute node for instances. 
# The head node is excluded from the set of servers used for provisioning customer instances. 
# For development and testing, allowing the head node to act as a compute node for instances is useful.
# To enable the head node to act as a compute node for instances:

sdcadm post-setup dev-headnode-prov
-- Configuring CNAPI to allow headnode provisioning and over-provisioning (allow a minute to propagate)

```

10. Install Docker Engine for Triton. Use following commands (Source).  
https://github.com/TritonDataCenter/sdc-docker#installation

```
 sdcadm post-setup dev-sample-data
 sdcadm post-setup docker

 ssh root@10.99.99.7                   (#ssh to the CoaL GZ)
 sdcadm self-update
 sdcadm post-setup common-external-nics && sleep 10  (#imgapi needs external)
 sdcadm post-setup dev-headnode-prov
 sdcadm post-setup dev-sample-data  (#sample packages for docker containers)
 sdcadm post-setup cloudapi
 sdcadm post-setup docker
 sdcadm experimental update dockerlogger
```

11. Check the IP address of AdminUI and CloudAPI. AdminUI offers operator's management interface. Respectively, CloudAPI offers API interface for managing customer instances.  
```
headnode# sdc-vmapi /vms?state=running | json -H -ga alias nics.0.ip nics.1.ip
```

12. Write down the addresses. You will need them later.   
    AdminUI: 10.88.88.??    
    CloudAPI: 10.88.88.??   

13. Start a web browser and open AdminUI address https://10.88.88.XX.  
 
14. You can manage Triton cloud platform with AdminUI interface. Create a new user. Do not use Scandinavian letters. Use your TUNI e-mail address and name. Activate “Approve For Provisioning” option. Finally, save the setting.  

15. Select the user and add SSH key. Open id_rsa.pub file from directory C:\Temp and copy key to “SSH Public Key” field. Name the key file to id_rsa.pub. Finally, save the key.  

16. Check that the SSH fingerprints match each other.  
   Check the id_rsa.pub fingerprint from AdminUI.  
      ---> fingerprint: X1:X2:X3:…    
   ubuntu# ssh-keygen -l -E md5 -f .ssh/id_rsa.pub  
      ---> X1:X2:X3:...  

17. You have added the account for Triton cloud platform.

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
  keyid: 6c:84:dc:ce:ea:cf:8d:77:de:32:fb:5f:83:71:47:b2

triton profile set fi-tuni-01
triton -i info
  error (ECONNREFUSED): connect ECONNREFUSED  10.88.88.XX:80
```
I cannnot get correct result here, because I could not get proper url (XX)

<br>


**Triton CLI tool -Running instances on Triton cloud platform** 

create an ubuntu instance 
```
triton -i images
triton -i packages
```

open a ssh connection to the ubuntu instance
```
clear
triton -i instance list
triton -i ssh name_of_instance
uname -a
hostnamectl
```





