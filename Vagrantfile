#===============================================================================
#
#         USAGE: `vagrant up --provider virtualbox`
# 
#   DESCRIPTION: Vagrant box for the ansible-osmo-iuh playbook originally created by BuildTheRobots
# 
#  REQUIREMENTS: Vagrant >v1.7, Ansible, VirtualBox
#          BUGS: ---
#         NOTES: Ansible script will prompt for SUDO password, you can just press enter to bypass this. It has been left in to cater for the original deployment which was not setup with NOPASSWD in the sudoers file.
#        AUTHOR: Matt Robey (secopsbot), matt@r0bey.co.uk
#       CREATED: 16/02/17
#      REVISION:  0.1
#===============================================================================
# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.require_version ">= 1.7.0"
 Vagrant.configure("2") do |config|
  config.vm.box = "secopsbot/ansible-osmo-iuh"
  config.ssh.username = "iuh"
  config.ssh.password = "iuh"

  config.vm.network "public_network", bridge: "eth0", ip: "10.9.1.120"
  config.vm.network "public_network", bridge: "eth0", ip: "10.9.1.13"

  config.vm.provision "ansible" do |ansible|
#    ansible.verbose = "v"
    ansible.playbook = "osmo-iuh.yml"
  end

end
