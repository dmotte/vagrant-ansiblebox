# vagrant-ansiblebox

[![GitHub Workflow Status](https://img.shields.io/github/actions/workflow/status/dmotte/vagrant-ansiblebox/release.yml?branch=main&logo=github&style=flat-square)](https://github.com/dmotte/vagrant-ansiblebox/actions)
[![Vagrant Cloud](https://img.shields.io/badge/vagrant-dmotte/ansiblebox-blue?logo=vagrant&style=flat-square)](https://app.vagrantup.com/dmotte/boxes/ansiblebox)

:package: **Debian Vagrant box** with **Ansible** and **Ansible Lint** installed via _APT_.

Since Ansible cannot run natively on a _Windows_ host, this Vagrant box can be useful if you need Ansible but you're using Windows on your controller.

> :package: This box is also on **Vagrant Cloud** as [`dmotte/ansiblebox`](https://app.vagrantup.com/dmotte/boxes/ansiblebox).

## Usage

See https://github.com/dmotte/misc/blob/main/examples/vagrant-ansible-provisioner for inspiration on how you could use this box.

If you want your host **SSH identity keys** and **known_hosts** to be available inside the VM, you can mount the host's `~/.ssh` directory like this:

```ruby
config.vm.synced_folder "~/.ssh", "/home/vagrant/.ssh-host",
    mount_options: ["dmode=700,fmode=600"]
```

Then you'll need to add some directives to the `~/.ssh/config` file inside the VM:

```ruby
config.vm.provision "shell", privileged: false, inline: <<-SHELL
    touch ~/.ssh/config; chmod 600 ~/.ssh/config
    echo "UserKnownHostsFile ~/.ssh-host/known_hosts" >> ~/.ssh/config
    echo -e "Host *\n    IdentityFile ~/.ssh-host/id_ed25519" >> ~/.ssh/config
SHELL
```

If you want to install additional packages:

```ruby
config.vm.provision "shell", inline: <<-SHELL
    apt-get update; apt-get install -y rsync
SHELL
```
