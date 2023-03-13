**Exercise 1: Basic Linux Commands**

Virtualization is not directly supported by an operating system. Virtualization support is implemented with separate virtualization software (Tier-2). Virtualization software is used to create a virtual machine. A virtual machine works like a real computer. In the next exercise, we will use VMware Workstation virtualization software and install Linux operating system on a virtual machine.

Installation of Ubuntu Server

The following instructions are made for Microsoft Windows 10. If you are using MacOS, then you have to adapt instructions.

1. Download Ubuntu Server 20.04.* LTS from Ubuntu home page ([Link](https://releases.ubuntu.com/focal/)). Save ISO file to directory C:\Temp.

2. Configure the virtualization software. Set the following information.

|Quest operating system| Virtual machine name |Location|
|:- |:- |:- |
|Ubuntu 64-bit |Ubuntu Server 01 |e.g. C:\Temp\Ubuntu_Server_01|

3. Change the virtual machine settings.

|Memory (GB) | Hard Disk (SCSI) | CD/DVD (IDE) | Network Adapter |
|:- |:- |:- |:- |
|2048 |40GB |Use ISO image file -> C:\Temp\ubuntu*.iso | VMware: NAT, Oracle: Bridge|

4. Start the virtual machine and install Ubuntu Server.

5. Storage configuration. Uncheck “Set up this disk as an LVM group”.
Image 1. Default settings. Image 2. Customs settings.

6. Remember to install SSH server. After installation, reboot Ubuntu Server.

7. The default installation does not include a graphical user interface. Usually, when we run virtual machines or instances in a cloud, the proper solution to configure virtual resources is a command line.

8. Check IP address of the virtual machine with ip command.

```
Ubuntu# ip addr
```

9. Download Netflix.txt from Moodle and save the file to directory C:\Temp.

10. User SFTP command transfer files from the local computer to the virtual machine.

11. Start PowerShell on Windows 10 and open the SFTP connection on the virtual machine. Use help
command to list available commands. If you have problems using PowerShell, you can use WinSCP.

```
PS> cd C:\Temp
PS> sftp user_name@IP_address
SFTP> help
```

12. Upload the Netflix.txt to Ubuntu Server and close the SFTP connection.

13. Open the SSH connection on the virtual machine. If you have problems using PowerShell, you can use Putty.

```
PS> ssh user_name@IP_address
```

14. Fill in the table and answer the questions “step-by-step”.
