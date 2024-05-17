# Ansible Server
## Hello! 
I use this Ansible script to do *basic* server configuration after a bare installation. What can it do?

* Creates a user with root privileges.
* Changes the default SSH port, disables password login, and copies your SSH key.
* Configures the firewall.

Additionally:

* In the docker folder, there is a docker-compose.yml with my container configuration, this script will not run them automatically.
* The script automatically creates a convenient file structure in /home for storing Docker containers data.

I hope you find this project interesting and learn something new from it, maybe even consider using it!

## Installation
I assume you've just installed your system, and it's bare. This instruction will help you deploy my configuration correctly

### Installing the necessary dependencies
**0.1** Depending on your distribution, you need to update your system and then install git, python, and ansible:
Example:\
*Void*\
`xbps-install -Su`\
`xbps-install -S git python ansible`

**0.2** If you haven't installed locales yet, you need to do so, otherwise ansible won't be able to run:
You need to uncomment *#en_US.UTF-8 UTF-8* line:\
*Void*\
`vim /etc/default/libc-locales`\
`xbps-reconfigure -fa`

*Arch*\
`vim /etc/locale.gen`\
`locale-gen`

**0.3** Cloning the repo\
`git clone https://github.com/alytidae/ansible-server-voidlinux`

### Add an additional disk configuration
This is just my recommendation, but before or after running (whichever you prefer), you could set
up disk redundancy using two excellent tools: [snapraid](https://www.snapraid.it/) and [mergerfs](https://github.com/trapexit/mergerfs). 
This will help prevent data loss in case one of the disks fails. However, it still won't replace backups!

### Changing config files
In the project, there are two places for configuration:

* `defaults/main.yml` - for Ansible configuration.
* `docker/docker.env` - for Docker configuration.

This Ansible script won't automatically start these containers; you'll have to do it manually after installation. Therefore, *you only need* to configure defaults/main.yml.

**1.1** Open the file defaults/main.yml, and modify all settings; there's a comment next to each one so you won't get confused.

*1.2(Optional)* Open the file docker/docker.env, and modify all Docker settings.

### Starting the Ansible
**1.3** In the project folder:\
`ansible-playbook playbook.yml`

### Configure backup
Don't forget to set up a backup of your server. I highly recommend using [restic](https://restic.net/) along with [cron](https://en.wikipedia.org/wiki/Cron).

## Additional Information

If you want to start Docker containers, you can simply go to the docker folder and run\
`sudo docker-compose --env-file docker.env up` \
However, if you want to use Grafana, before that, you need to copy the file 
`docker/prometheus-config/prometheus.yml` to `/home/your_username/containers/prometheus` on the server. 
This is the default Prometheus config, but there are additional lines to make node-exporter work for you. 
After that, you can start the Docker containers, and everything should run without errors.

Initially, this project was conceived as deploying the server only on the Voidlinux
distribution, as there are some peculiarities when working with Ansible. 
However, in the end, I abandoned this idea because I didn't use anything specific to Voidlinux.

## License
Licensed under [The MIT License](https://opensource.org/license/mit/)
