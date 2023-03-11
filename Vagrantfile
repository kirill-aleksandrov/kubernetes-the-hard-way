# -*- mode: ruby -*-
# vi: set ft=ruby :

network_interface = "eno1"

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/focal64"

  config.vm.provider "virtualbox" do |vb|
    vb.memory = "512"
  end

  config.vm.define "lb-api" do |c|
    c.vm.hostname = "lb-api"
    c.vm.network "public_network", ip: "172.20.0.0", :netmask => '255.240.0.0', bridge: network_interface
  end

  (0..1).each do |n|
    config.vm.define "metallb-#{n}" do |c|
      c.vm.hostname = "metallb-#{n}"
      c.vm.network "public_network", ip: "172.20.0.#{n+1}", :netmask => '255.240.0.0', bridge: network_interface
    end
  end

  (0..2).each do |n|
    config.vm.define "controller-#{n}" do |c|
      c.vm.hostname = "controller-#{n}"
      c.vm.network "public_network", ip: "172.20.1.#{n}", :netmask => '255.240.0.0', bridge: network_interface
      c.vm.provider "virtualbox" do |vb|
        vb.memory = "1024"
      end
    end
  end

  (0..2).each do |n|
    config.vm.define "worker-#{n}" do |c|
      c.vm.hostname = "worker-#{n}"
      c.vm.network "public_network", ip: "172.20.2.#{n}", :netmask => '255.240.0.0', bridge: network_interface
      c.vm.provider "virtualbox" do |vb|
        vb.cpus = 2
        vb.memory = "2048"
      end
    end
  end
end
