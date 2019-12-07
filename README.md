# cbhost-ansible

Ansible playbooks for a multi-purpose personal server.

This node hosts the following containers behind a NGINX reverse proxy:
 - 3x [WordPress](https://github.com/collinbarrett/wp-host-on-containers) (w/NGINX, Redis, & MariaDB)
 - [FilterLists](https://github.com/collinbarrett/FilterLists)
    - 1x [Create React App](https://create-react-app.dev) (w/NGINX)
    - 1x ASP.NET Core API (w/MariaDB)
    - 1x .NET Core console app
    - 1x [Discourse](https://hub.filterlists.com/)
 - 1x [Bitwarden](https://help.bitwarden.com/article/install-on-premise/)

## Managed Node Setup

Use a single [DigitalOcean](https://m.do.co/c/fea63c0a77d1) Ubuntu LTS droplet as a host. The $10/mo instance is required to satisfy Bitwarden's SQL Server dependency requiring 2GB ram. Include a public SSH key stored with DigitalOcean when creating the droplet. Enable droplet backups.

## Control Node Setup

As primarily a .NET developer, I use a Windows development environment.

> Windows is not supported for the control node. [Ansible Docs](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html#control-node-requirements)

So, to get up and running, I am using [WSL](https://docs.microsoft.com/en-us/windows/wsl/about).

### Enable and Install WSL

Follow the [official docs](https://docs.microsoft.com/en-us/windows/wsl/install-win10) for getting WSL up and running. Use the latest Ubuntu LTS image.

### SSH Keys

Copy over `.pem` and `.pub` SSH keys (of the same name) into WSL `~/.ssh` directory.

Use `keychain` to automatically launch `ssh-agent` and `ssh-add` the key every time a WSL terminal instance is opened.

 - `sudo apt-get install keychain`

 - Add to `~/.bashrc`: `eval $(keychain --eval id_rsa)`

via [StackOverflow](https://stackoverflow.com/a/24902046/2343739)

### git clone

Clone this `cbhost-ansible` repo into a directory inside of the WSL instance.

### Authenticate with GitHub

With 2FA enabled on GitHub, create a personal access token (PAT) and configure `credential.helper` to store it via git in WSL. The first `git push` requires providing a username and PAT. The credentials are then stored for future pushes.

### VS Code WSL Remote

Install the [`Remote - WSL`](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-wsl) extension inside of Visual Studio Code on the Windows host to edit the git repo.

### Inventory

Add the IP of the managed node droplet to `/etc/ansible/hosts` inside WSL.

## Common Ansible Commands for Running/Debugging

 - `ansible all -m ping -u root`
 - `ansible all -m ping`
 - `ansible-playbook 00-cbhost.yml`
