# cbhost-ansible

An Ansible playbook collection for a multi-purpose personal server.

This node will host the following containers behind a NGINX reverse proxy:
 - 3x WordPress (w/NGINX, Redis, & MariaDB)
 - 1x React (w/NGINX)
 - 1x ASP.NET Core API (w/MariaDB)
 - 1x .NET Core console app
 - 1x Discourse
 - 1x Bitwarden

## Host Setup

I use a single minimal DigitalOcean droplet as a host. It's a $10/mo instance since Bitwarden's SQL Server dependency requires 2GB ram. I have a public SSH key stored with DigitalOcean that I add to the droplet when creating it. I enable droplet backups.

## Control Node Setup

As primarily a .NET developer, I use a Windows development environment.

> Windows is not supported for the control node. [Ansible Docs](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html#control-node-requirements)

So, to get up and running, I am using WSL.

### Enable and Install WSL

Follow [official docs](https://docs.microsoft.com/en-us/windows/wsl/install-win10) for getting WSL up and running. I am using the latest Ubuntu LTS image.

### SSH Keys

Copy over `.pem` and `.pub` SSH keys (of the same name) into WSL `~/.ssh` directory.

I am using `keychain` to automatically launch `ssh-agent` and `ssh-add` my key every time I open the WSL terminal.

https://stackoverflow.com/a/24902046/2343739

### git clone

Clone this `cbhost-ansible` repo into a directory inside of the WSL instance.

### Authenticate with GitHub

Since I have 2FA enabled on GitHub, I created a personal access token and configured `credential.helper` to store via git in WSL. The first time I try to `git push`, I provide username and PAT. It is then stored for me for future pushes.

### VS Code WSL Remote

Install the `Remote - WSL` extension inside of Visual Studio Code on the Windows host to edit the git repo.

### Ansible Hosts Inventory

Add the IP of the host droplet to `/etc/ansible/hosts` inside WSL.

## Commands

 - `ansible all -m ping -u root`
 - `ansible all -m ping`
 - `ansible-playbook 00-cbhost.yml`
