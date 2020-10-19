# cbhost-ansible

Ansible playbooks for a multi-purpose personal server.

## Managed Node Setup

Use a single [DigitalOcean](https://m.do.co/c/fea63c0a77d1) Ubuntu LTS droplet as a host. Include a public SSH key stored with DigitalOcean when creating the droplet. Enable droplet backups.

## Control Node Setup

As primarily a .NET developer, I use a Windows development environment.

> Windows is not supported for the control node. [Ansible Docs](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html#control-node-requirements)

So, to get up and running, I am using [WSL](https://docs.microsoft.com/en-us/windows/wsl/about).

### Enable and Install WSL

Follow the [official docs](https://docs.microsoft.com/en-us/windows/wsl/install-win10) for getting WSL up and running. Use the latest Ubuntu LTS image.

### Install Ansible inside WSL

via [Ansible Docs](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html#installing-ansible-on-ubuntu)

### SSH Keys

- `cp /path/to/id_rsa.pub ~/.ssh/id_rsa.pub`
- `cp /path/to/id_rsa ~/.ssh/id_rsa`
- `chmod 700 ~/.ssh`
- `chmod 644 ~/.ssh/id_rsa.pub`
- `chmod 600 ~/.ssh/id_rsa`

### git clone

Clone this `cbhost-ansible` repo into a directory inside of the WSL instance.

### Inventory

Add the IP of the managed node droplet to `/etc/ansible/hosts` inside WSL.

## Common Ansible Commands for Running/Debugging

- `ansible all -m ping -u root`
- `ansible all -m ping`
- `ansible-playbook 00-cbhost.yml`
