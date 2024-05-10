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
Example:
*Void*
`xbps-install -Su`
`xbps-install -S git python ansible`

**0.2** If you haven't installed locales yet, you need to do so, otherwise ansible won't be able to run:
You need to uncomment #en_US.UTF-8 UTF-8 line:
*Void*
`vim /etc/default/libc-locales`
`xbps-reconfigure -fa`

*Arch*
`vim /etc/locale.gen`
`locale-gen`

### Changing config files
In the project, there are two places for configuration:

* `defaults/main.yml` - for Ansible configuration.
* `docker/docker.env` - for Docker configuration.

This Ansible script won't automatically start these containers; you'll have to do it manually after installation. Therefore, *you only need* to configure defaults/main.yml.

Mandatory:
**1.1** Open the file defaults/main.yml, and modify all settings; there's a comment next to each one so you won't get confused.

Optional:
*1.2* Open the file docker/docker.env, and modify all Docker settings.


## License
Licensed under [The MIT License](https://opensource.org/license/mit/)
