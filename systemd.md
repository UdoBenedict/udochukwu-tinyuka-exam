## SystemD
### What is SystemD?
It is an init system. The init system of any Linux distro is a process & a process is any task that runs in the background.   
The init system is the most important process because **it starts up the system, loads other processes and manages all services like apache, nginx that run in the background.** It has a process ID of 1.

-----
### Working with Units
Units are resources or anything that systemd is able to manage for you. These include but are not limited to; services, timers, mounts, automounts etc.

----
### Systemctl
This manages and interacts with the systemd system. Some of its commands are as follows;  
+ systemctl start servicename  
+ systemctl stop servicename  
+ systemctl restart servicename - restarts a specific service.  
+ systemctl enable servicename - enables a service to start automatically after boot.    
* systemctl disable servicename.
* systemctl reboot - reboots the system.
* systemctl shutdown - shutdowns the system.
* +systemctl lists-units - lists all units (services, timers, etc.) managed by systemd.
* +systemctl lists-units --type=service - lists all services.
* +systemctl lists-units --type=service --all - lists all services including the inactive ones.

----
### Unit Files
Systemd looks at files to know or understand how it needs to interact with processes. Service files or unit files are just text files that contain instructions that tell systemd how to manage that particular service.

The three most important systemd unit directories are:

1. /etc/systemd/system - stores config files or unit files with top priority. It is recommended to store custom config files here because this directory is priority & storing files in /lib/systemd/system can have them overwritten when the application or service does an update.
2. /run/systems/system - stores runtime systemd units.
3. /lib/systemd/system - stores files from any application or service you install.

----
### Understanding Unit Files
![image of a unit file]("\Markdown texts\unit file.png")

----
### Editing and Overriding Unit Files
In editing unit files, stick to the syntax as the file is case sensitive.

To edit a unit file, run the command; <mark>sudo systemctl edit servicename.ext</mark>

Code preview;  
`sudo systemctl edit apache.service`  

#### Overriding Unit files
An Apache service file /lib/systemd/system/apache.service stored in /lib/systemd/system directory is to be overriden or edited.  
The system saves the overriden file /etc/systemd/system/apacheservice.d/override.conf in the /etc/systemd/system directory.  
This is because /etc/systemd/system takes the most priority of all systemd directories.  
Inside the config file, editing or overriding should be done between the first two comments.  

----
### Undo-ing changes to a service file
Run the command; <mark>sudo rm filepath</mark>

Code preview;  
`sudo rm /etc/systemd/system/apacheservice.d/`

**N.B:**  
1. The overriden or edited file is always in the /etc/systemd/system directory.

2. After overriding a service file, use the <mark>sudo systemctl daemon-reload</mark> to reload systemd to make sure that it takes into account all the changes made. 