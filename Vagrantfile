# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/focal64"

  config.vm.provider "virtualbox" do |vb|
    vb.memory = "512"
  end

  (0..2).each do |n|
    config.vm.define "lb-0" do |c|
        c.vm.hostname = "lb-#{n}"
        c.vm.network "public_network", ip: "172.20.0.#{n}", :netmask => '255.240.0.0', bridge: "wlp7s0"
    end
  end

  (0..2).each do |n|
    config.vm.define "controller-#{n}" do |c|
      c.vm.hostname = "controller-#{n}"
      c.vm.network "public_network", ip: "172.20.1.#{n}", :netmask => '255.240.0.0', bridge: "wlp7s0"
      c.vm.provider "virtualbox" do |vb|
        vb.memory = "1024"
      end
    end
  end

  (0..2).each do |n|
    config.vm.define "worker-#{n}" do |c|
      c.vm.hostname = "worker-#{n}"
      c.vm.network "public_network", ip: "172.20.2.#{n}", :netmask => '255.240.0.0', bridge: "wlp7s0"
      c.vm.provider "virtualbox" do |vb|
        vb.cpus = 2
        vb.memory = "2048"
      end
    end
  end

  config.vm.define "deployer" do |c|
    c.vm.hostname = "deployer"
    c.vm.network "public_network", ip: "172.20.255.1", :netmask => '255.240.0.0', bridge: "wlp7s0"
    c.vm.provider "virtualbox" do |vb|
      vb.cpus = 2
      vb.memory = "1024"
    end
  end
end
