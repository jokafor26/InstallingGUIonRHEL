# InstallingGUIonRHEL

Installing GUI on RHEL

I started by creating a snapshot of my instances just for backup reasons.
 
![Image](https://github.com/user-attachments/assets/510a6ab4-a840-4240-80f3-7eedf792ce43)

I changed the instances type to t2.medium. I turned the instance on then used the systemcetl get-default command to record the output which is the multi-user.target which is the default server which starts required units for operational and non graphical system with network support.
 
 ![Image](https://github.com/user-attachments/assets/21c3d47b-16dc-4076-8747-f38a04652077)
 
![Image](https://github.com/user-attachments/assets/275251c2-6a15-4995-bd5e-2c5313b8e3c8)

I updated my instances by using the yum -y update command then installed the gnome gui by using the yum groupinstall -y “Server with GUI” command. Then set it to start by default with the systemctl set-default graphical.target and sudo systemctl default commands. 

I first setup XRDP by starting with the command rpm -Uvh http://li.nux.ro/download/nux/dextop/el7/x86_64/nux-dextop-release-0-1.el7.nux.noarch.rpm which would get the needed packages. 

![Image](https://github.com/user-attachments/assets/0c9b79c9-ffc1-4619-b0be-a41a02d90d9f)

Using the sudo yum install -y xrdp tigervnc-server I was able to install XRDP and VNC.

 ![Image](https://github.com/user-attachments/assets/f3fd17fb-3854-42dd-a2fc-5d96dbe19e37)

After completion I configured, I used systemctl start and xrdp enable commands to start XRDP at boot.

![Image](https://github.com/user-attachments/assets/03d594c3-a790-4484-8b00-e450ec08531a)

With the firewall operational I have to configure the remote desktop protocol rule by allowing the connection using sudo firewall-cmd --permanent --add-port=3389/tcp and sudo firewall-cmd –reload commands. 

![Image](https://github.com/user-attachments/assets/9efcb4d2-55aa-4064-97bb-2f80b9e9fb64)

I made some configuratios in the xrdp config file by using the vi /etc/xrdp/xrdp.ini command then comment out the channel_code since it wont be needed.

![Image](https://github.com/user-attachments/assets/e814a126-14aa-45d4-85e4-70cfc6a078db)

Made a quick install of firefox browser using the yum install firefox command in the cli then using security groups in the AWS console I allowes RDP port for incomming connections on the 3389 port number.
 
![Image](https://github.com/user-attachments/assets/f7184820-8fbe-49bb-ba17-339d54ef4c6c)

I my desktop I used my RDP client to connect to my instance then oppened firefox to navigate to http//127.0.0.1:9090 with the webadmin user I created before.

![Image](https://github.com/user-attachments/assets/ca4b6636-0949-42d5-855a-aed0b812a055)

I was able to log in which indicated RDP is working to my webadmin console.

![Image](https://github.com/user-attachments/assets/6ff70e67-e11c-4372-8166-10b4723b4508)

![Image](https://github.com/user-attachments/assets/d164d436-591a-4113-bc21-f3252d95e88c)

Showing a restablished RDP session that included firefox connection through webadmin account.

![Image](https://github.com/user-attachments/assets/698bc0cc-de04-4d2d-81b0-1f48379892ec)

I restarted my instances and switched the instance type back to t2.mirco through the AWS console.

![Image](https://github.com/user-attachments/assets/6f5e0bdc-0292-42f6-b4ab-39b6fbd130a2)

I disabled XRDP start at bootup and set default run level using systemctl set-default runlevel command.
 
![Image](https://github.com/user-attachments/assets/3f51cff8-59e8-4ad8-984e-a2ae3f8e32c7)
