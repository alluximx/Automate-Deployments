# Automate-Deployments

1. Create the VPS Server
2. Set time zone and encodings
	*	As root user run
		```dpkg-reconfigure tzdata && \
		dpkg-reconfigure locales  && \
		apt-get update  && \
		apt-get upgrade -y && \
		apt-get install -y git vim wget curl
		```
3. Install unattended upgrades
	```apt-get install -y unattended-upgrades update-notifier-common && \
	dpkg-reconfigure --priority=low unattended-upgrades
	```
4. Optional
	*	Install Bashit to have a "sexy theme"
		```git clone --depth=1 https://github.com/Bash-it/bash-it.git ~/.bash_it && ~/.bash_it/install.sh \
		&& mkdir -p ~/.bash_it/plugins/enabled/ \
		&& ln -s ~/.bash_it/plugins/available/history.plugin.bash ~/.bash_it/plugins/enabled/250---history.plugin.bash \
		&& sed -i 's/bobby/sexy/' ~/.bashrc
		```
5. Configure a user with sudo privileges
	*	As root
	```useradd -m -s /bin/bash -G sudo "user-name"```
6. Set password to the user created
	*	As root
	```passwd "user-name"```
7. Chage user, add ssh keys and set permissions
	```su "user-name"
	mkdir ~/.ssh
	chmod 700 ~/.ssh
	vim ~/.ssh/authorized_keys
	chmod 600 ~/.ssh/authorized_keys
	```
	```
	ssh-keygen -t rsa -b 4096 -C "server"
	eval "$(ssh-agent -s)"
	ssh-add ~/.ssh/id_rsa
	```
	```
	ssh -T git@github.com
	```
8. Edit  ```/etc/ssh/sshd_config```
	```PermitRootLogin no```
9. Restart the sshd server
	```sudo systemctl restart sshd```
10. Optional
	* You can set a new hostname for your server
	```sudo hostnamectl set-hostname "server-name"```
11. 