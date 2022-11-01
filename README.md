# vagrant-ansiblebox

[![GitHub Workflow Status](https://img.shields.io/github/workflow/status/dmotte/vagrant-ansiblebox/release?logo=github&style=flat-square)](https://github.com/dmotte/vagrant-ansiblebox/actions)
[![Vagrant Cloud](https://img.shields.io/badge/vagrant-dmotte/ansiblebox-blue?logo=vagrant&style=flat-square)](https://app.vagrantup.com/dmotte/boxes/ansiblebox)

:package: **Debian Vagrant box** with **Ansible** installed via _pip_ with _Python 3_.

Since Ansible cannot run natively on a _Windows_ host, this Vagrant box can be useful if you need Ansible but you're using Windows on your controller.

This project uses [geerlingguy/ansible-role-pip](https://github.com/geerlingguy/ansible-role-pip) to install _pip_ and _Ansible_ inside the VM.

> :package: This box is also on **Vagrant Cloud** as [`dmotte/ansiblebox`](https://app.vagrantup.com/dmotte/boxes/ansiblebox).

## Usage

TODO improve usage section

```ruby
config.vm.synced_folder "~/.ssh", "/home/vagrant/.ssh-host",
    mount_options: ["dmode=700,fmode=600"]

config.vm.provision "shell", inline: <<-SHELL
    apt-get install -y rsync
SHELL

config.vm.provision "shell", privileged: false, inline: <<-SHELL
    touch ~/.ssh/config && chmod 600 ~/.ssh/config
    echo "UserKnownHostsFile ~/.ssh-host/known_hosts" >> ~/.ssh/config
    echo -e "Host *\n    IdentityFile ~/.ssh-host/id_ed25519" >> ~/.ssh/config
SHELL
```
