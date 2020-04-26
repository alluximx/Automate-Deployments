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

*	Optional
	*	Install Bashit to have a "sexy theme"
		*	git clone --depth=1 https://github.com/Bash-it/bash-it.git ~/.bash_it && ~/.bash_it/install.sh \
			&& mkdir -p ~/.bash_it/plugins/enabled/ \
			&& ln -s ~/.bash_it/plugins/available/history.plugin.bash ~/.bash_it/plugins/enabled/250---history.plugin.bash \
			&& sed -i 's/bobby/sexy/' ~/.bashrc
*	Configure a user with sudo privileges 
	*	useradd -m -s /bin/bash -G sudo "user-name"
*	Set password to the user created
	*	passwd "user-name"

