# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  config.vm.box = "centos/7"

  config.vm.provider "virtualbox" do |v|
	  v.memory = 256
  end

  config.vm.define "inetRouter" do |inetRouter|
    inetRouter.vm.network "private_network", ip: "192.168.255.1", virtualbox__intnet: "router-net"
    inetRouter.vm.network "private_network", ip: "192.168.255.2", virtualbox__intnet: "router-net"
	inetRouter.vm.hostname = "inetRouter"
  end

  config.vm.define "centralRouter" do |centralRouter|
    centralRouter.vm.network "private_network", ip: "192.168.255.11", virtualbox__intnet: "router-net"
    centralRouter.vm.network "private_network", ip: "192.168.255.12", virtualbox__intnet: "router-net"
    centralRouter.vm.network "private_network", ip: "192.168.100.1", virtualbox__intnet: "office1-net"
    centralRouter.vm.network "private_network", ip: "192.168.0.1", virtualbox__intnet: "dir-net"
	centralRouter.vm.hostname = "centralRouter"
  end
  
  config.vm.define "testClient1" do |testClient1|
    testClient1.vm.network "private_network", ip: "10.10.10.254", virtualbox__intnet: "testLAN"
    testClient1.vm.network "private_network", ip: "192.168.100.10", virtualbox__intnet: "office1-net"
    testClient1.vm.hostname = "testClient1"
  end

  config.vm.define "testClient2" do |testClient2|
    testClient2.vm.network "private_network", ip: "10.10.10.254", virtualbox__intnet: "testLAN"
    testClient2.vm.network "private_network", ip: "192.168.100.20", virtualbox__intnet: "office1-net"
    testClient2.vm.hostname = "testClient2"
  end

  config.vm.define "testServer1" do |testServer1|
    testServer1.vm.network "private_network", ip: "10.10.10.1", virtualbox__intnet: "testLAN"
    testServer1.vm.network "private_network", ip: "192.168.0.10", virtualbox__intnet: "dir-net"
    testServer1.vm.hostname = "testServer1"
  end

  config.vm.define "testServer2" do |testServer2|
    testServer2.vm.network "private_network", ip: "10.10.10.1", virtualbox__intnet: "testLAN"
    testServer2.vm.network "private_network", ip: "192.168.0.20", virtualbox__intnet: "dir-net"
    testServer2.vm.hostname = "testServer2"
  end

  config.vm.provision "ansible" do |ansible|
    ansible.verbose = "vvv"
    ansible.playbook = "provisioning/playbook.yml"
    ansible.become = "true"
  end

end
