# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
    config.vm.box = "debian/bookworm64"

    config.vm.hostname = "ansiblebox"

    config.vm.provision "shell", inline: <<-SHELL
        # git is needed by Ansible Lint
        # sshpass is needed by Ansible for password-based SSH login
        apt-get update; apt-get install -y git sshpass ansible ansible-lint
    SHELL

    config.ssh.insert_key = false # This is usually recommended for base boxes
end
