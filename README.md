# tasks

# 1. *Setup SSH server & only allow SSH port 2202 via firewall*
- Disable password authentication and only allow via ssh keys
- Connect via SSH to that host through key pair only
- Write a script to automatically connect to vm server and take incremental backup (rsync) of
  a directory from vm server to your local directory hourly 



  ## Setting up ssh server and allowing ssh port 2202


At first when we look at the ports that are open and actively listenning. We can see the port 22 is active and is for ssh by default.
[!screenshot](images/1.png)


Now to change the port number for ssh, we go into the configuration file which is inside the etc dir. Most of the configuration for the linux system is inside this dir. now lets go into /etc/ssh/ and we can see there are many config file. The one we want to look into is sshd_config.
[!screenshot](images/2.png)



we need to change the configuration of sshd_config. We can do this by a text editor. I am gonna use vim to edit the configuration.
[!screenshot](images/3.png)


inside all the commented configuration are the ones that are by default. If we want to change any of the configuration we can uncomment the line and change it. Here I am gonna change the port number which is set to 22 > 2202.
[!screenshot](images/4.png)


Here i change the port number. Likewise if we were to change the password auth, we can search for Password authentication and change the value to "no". By default it would be set to "yes"
[!screenshot](images/5.png)


before this i had already tried this so it is displaying "skipping adding existing rule" and we do not need to do this step if there are no firewall. Here i am telling my firewall(ufw), to allow ssh on port 2202. for differennt linux distros like centos, redhat there might be different firewalls.
[!screenshot](images/6.png)



Now to put this into effect we need to restart the service ssh by "systemctl restart ssh" or simply reboot the machine. Now if we look into the ports, we can see that the port 22 has been changed to port 2202.
[!screenshot](images/7.png)


Now we can log in to the vm using ssh and since the ssh is not on port 22 anymore, we need to define which port it is by "-p 2202"
[!screenshot](images/8.png)
