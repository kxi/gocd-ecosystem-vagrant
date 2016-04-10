# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure(2) do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://atlas.hashicorp.com/search.
  config.vm.define "go-server" do |server|
    server.vm.box = "bento/centos-7.1"
    server.vm.hostname = "go-server"
    server.vm.network "forwarded_port", guest: 8153, host: 1153
    server.vm.network "private_network", ip: "192.168.50.4"
    server.vm.provider "virtualbox" do |vb|
      vb.memory = "4096"
    end
    server.vm.provision "ansible" do |ansible|
      ansible.playbook = "playbooks/system_provision.yml"
      ansible.limit = "go-server"
    end
  end

  config.vm.define "go-agent" do |agent|
    agent.vm.box = "bento/centos-7.1"
    agent.vm.hostname = "go-agent"
    agent.vm.network "forwarded_port", guest: 8153, host: 2153
    agent.vm.network "private_network", ip: "192.168.50.3"
    agent.vm.provider "virtualbox" do |vb|
      vb.memory = "1024"
    end
    agent.vm.provision "ansible" do |ansible|
      ansible.playbook = "playbooks/system_provision.yml"
      ansible.limit = "go-agent"
    end
  end
end
