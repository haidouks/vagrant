# encoding: utf-8
# -*- mode: ruby -*-
# vi: set ft=ruby :
# Box / OS
VAGRANT_BOX = 'ubuntu/trusty64'
# Memorable name for your
VM_NAME = 'ubuntu'
# VM User — 'vagrant' by default
VM_USER = 'vagrant'
# Host folder to sync
HOST_PATH = '/Users/cansinaldanmaz/Downloads/Workspace'
# Where to sync to on Guest — 'vagrant' is the default user name
GUEST_PATH = '/workspace'
# # VM Port — uncomment this to use NAT instead of DHCP
# VM_PORT = 8080
Vagrant.configure(2) do |config|
  # Vagrant box from Hashicorp
  config.vm.box = VAGRANT_BOX
  
  # Actual machine name
  config.vm.hostname = VM_NAME
  # Set VM name in Virtualbox
  config.vm.provider "virtualbox" do |v|
    v.name = VM_NAME
    v.memory = 2048
  end
  #DHCP — comment this out if planning on using NAT instead
  config.vm.network "private_network", type: "dhcp"
  # # Port forwarding — uncomment this to use NAT instead of DHCP
  # config.vm.network "forwarded_port", guest: 80, host: VM_PORT
  # Sync folder
  config.vm.synced_folder HOST_PATH, GUEST_PATH
  # Disable default Vagrant folder, use a unique path per project
  config.vm.synced_folder '.', '/home/'+VM_USER+'', disabled: true
  # Install Git, Node.js 6.x.x, Latest npm
  config.vm.provision "shell", inline: <<-SHELL
    apt-get update
    apt-get install -y git
    curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
    npm install -g npm
    apt-get update
    apt-get upgrade -y
    apt-get autoremove -y
	#install docker for trusty
	sudo apt-get install -y \
		linux-image-extra-$(uname -r) \
		linux-image-extra-virtual
	sudo apt-get update
	sudo apt-get install -y\	
		apt-transport-https \
		ca-certificates \
		curl \
		software-properties-common
	curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
	sudo apt-key fingerprint 0EBFCD88
	sudo add-apt-repository \
		"deb [arch=amd64] https://download.docker.com/linux/ubuntu \
		$(lsb_release -cs) \
		stable"
	sudo apt-get update
	sudo apt-get install -y docker-ce
	sudo groupadd docker
	sudo usermod -aG docker $USER
  SHELL
end