# InstallingGUIonRHEL

Installing GUI on RHEL

I started by creating a snapshot of my instances just for backup reasons.
 
<img width="746" height="281" alt="image" src="https://github.com/user-attachments/assets/6493f3fd-f01c-4eed-a435-a45f632f836b" />

I changed the instances type to t2.medium. I turned the instance on then used the systemcetl get-default command to record the output which is the multi-user.target which is the default server which starts required units for operational and non graphical system with network support.
 
<img width="751" height="232" alt="image" src="https://github.com/user-attachments/assets/23d7a6de-0ce9-461a-85b8-3cec1d1276ee" />
 
<img width="735" height="246" alt="image" src="https://github.com/user-attachments/assets/86e643ee-f904-4138-901b-184c1dc2f817" />

I updated my instances by using the yum -y update command then installed the gnome gui by using the yum groupinstall -y “Server with GUI” command. Then set it to start by default with the systemctl set-default graphical.target and sudo systemctl default commands. 

I first setup XRDP by starting with the command rpm -Uvh http://li.nux.ro/download/nux/dextop/el7/x86_64/nux-dextop-release-0-1.el7.nux.noarch.rpm which would get the needed packages. 

<img width="860" height="283" alt="image" src="https://github.com/user-attachments/assets/10214da4-42e0-4259-88cb-3df5e9b382c4" />

Using the sudo yum install -y xrdp tigervnc-server I was able to install XRDP and VNC.

<img width="774" height="771" alt="image" src="https://github.com/user-attachments/assets/9e3f1039-adda-4857-9874-84324ef0c06b" />

After completion I configured, I used systemctl start and xrdp enable commands to start XRDP at boot.

<img width="837" height="141" alt="image" src="https://github.com/user-attachments/assets/d598af21-f45b-4b31-8e69-0ed51e52d6c6" />

With the firewall operational I have to configure the remote desktop protocol rule by allowing the connection using sudo firewall-cmd --permanent --add-port=3389/tcp and sudo firewall-cmd –reload commands. 

<img width="812" height="257" alt="image" src="https://github.com/user-attachments/assets/1435b99e-a0e5-436c-af22-67dc8baac5ee" />

I made some configuratios in the xrdp config file by using the vi /etc/xrdp/xrdp.ini command then comment out the channel_code since it wont be needed.

<img width="478" height="590" alt="image" src="https://github.com/user-attachments/assets/c42d0247-75f6-4326-b291-20709c1ef61a" />

Made a quick install of firefox browser using the yum install firefox command in the cli then using security groups in the AWS console I allowes RDP port for incomming connections on the 3389 port number.
 
<img width="768" height="255" alt="image" src="https://github.com/user-attachments/assets/07db605f-8f44-41a8-9b87-cb6781ef4776" />

I my desktop I used my RDP client to connect to my instance then oppened firefox to navigate to http//127.0.0.1:9090 with the webadmin user I created before.

<img width="511" height="364" alt="image" src="https://github.com/user-attachments/assets/9184cbc2-2fe7-4617-ab8c-67a25a0658f0" />

I was able to log in which indicated RDP is working to my webadmin console.

<img width="480" height="374" alt="image" src="https://github.com/user-attachments/assets/9e77bd03-eff5-419b-bb42-ea8f53901a93" />

<img width="523" height="419" alt="image" src="https://github.com/user-attachments/assets/ef8e4903-34a1-4066-8958-e70ebfdb5d2d" />

Showing a restablished RDP session that included firefox connection through webadmin account.

<img width="588" height="473" alt="image" src="https://github.com/user-attachments/assets/441216be-0765-41ee-b223-6acb78b96105" />

I restarted my instances and switched the instance type back to t2.mirco through the AWS console.

<img width="634" height="200" alt="image" src="https://github.com/user-attachments/assets/b1325134-f367-4c2d-ade1-9d4e9f43266d" />

I disabled XRDP start at bootup and set default run level using systemctl set-default runlevel command.
 
<img width="851" height="407" alt="image" src="https://github.com/user-attachments/assets/09a099c0-2cde-41c4-a92b-8cc2ae134d19" />
