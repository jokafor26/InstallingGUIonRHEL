# InstallingGUIonRHEL

Installing GUI on RHEL

I started by creating a snapshot of my instances just for backup reasons.
 
![Image](https://github.com/user-attachments/assets/510a6ab4-a840-4240-80f3-7eedf792ce43)

I changed the instances type to t2.medium. I turned the instance on then used the systemcetl get-default command to record the output which is the multi-user.target which is the default server which starts required units for operational and non graphical system with network support.
 
 ![Image](https://github.com/user-attachments/assets/21c3d47b-16dc-4076-8747-f38a04652077)
 
![Image](https://github.com/user-attachments/assets/275251c2-6a15-4995-bd5e-2c5313b8e3c8)

I updated my instances by using the yum -y update command then installed the gnome gui by using the yum groupinstall -y “Server with GUI” command. Then set it to start by default with the systemctl set-default graphical.target and sudo systemctl default commands. 

I first setup XRDP by starting with the command rpm -Uvh http://li.nux.ro/download/nux/dextop/el7/x86_64/nux-dextop-release-0-1.el7.nux.noarch.rpm which would get the needed packages. 

![Image](https://github.com/user-attachments/assets/7985f92a-7330-40c0-9d78-f463d65e6de3)

Using the sudo yum install -y xrdp tigervnc-server I was able to install XRDP and VNC.
 
![Image](https://github.com/user-attachments/assets/2334173d-fc97-43af-a198-5390dc188cdc)

After completion I configured, I used systemctl start and xrdp enable commands to start XRDP at boot.
 ![Image](https://github.com/user-attachments/assets/05b47b6f-3112-4be2-a3b0-c6b306878242)


With the firewall operational I have to configure the remote desktop protocol rule by allowing the connection using sudo firewall-cmd --permanent --add-port=3389/tcp and sudo firewall-cmd –reload commands. 
 ![Image](https://github.com/user-attachments/assets/dd4d22d2-2aa8-4aad-bbeb-2cdcb9363f71)


I made some configuratios in the xrdp config file by using the vi /etc/xrdp/xrdp.ini command then comment out the channel_code since it wont be needed.

 ![Image](https://github.com/user-attachments/assets/b9ff58ec-a3a8-460b-a545-2cf55e9ffd8c)

Made a quick install of firefox browser using the yum install firefox command in the cli then using security groups in the AWS console I allowes RDP port for incomming connections on the 3389 port number.
 
![Image](https://github.com/user-attachments/assets/6bc85cbb-eb69-44c2-9976-1b03b34b19f7)

I my desktop I used my RDP client to connect to my instance then oppened firefox to navigate to http//127.0.0.1:9090 with the webadmin user I created before.

 ![Image](https://github.com/user-attachments/assets/cd3eab4b-81f3-440a-8f9f-db8d77d9002e)


I was able to log in which indicated RDP is working to my webadmin console.

 ![Image](https://github.com/user-attachments/assets/59d70d9e-acab-432d-bbe0-8e44894d0f62)


Showing a restablished RDP session that included firefox connection through webadmin account.

![Image](https://github.com/user-attachments/assets/67de0e6c-2c08-4838-8f64-5c2e2ca5af7b)

 ![Image](https://github.com/user-attachments/assets/c2b5c4f6-226c-45cb-b8fd-ff15a057a75b)


I restarted my instances and switched the instance type back to t2.mirco through the AWS console.

 ![Image](https://github.com/user-attachments/assets/92211179-3e0f-4d46-b15e-c266d591d6b7)

I disabled XRDP start at bootup and set default run level using systemctl set-default runlevel command.
 
![Image](https://github.com/user-attachments/assets/80f4f95c-f756-44a4-b724-f7fdedb2c098)



