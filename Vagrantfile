# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|

  config.vm.provider :virtualbox do |vm|
    vm.linked_clone = true
    vm.customize ["modifyvm", :id, "--memory", 2048 ]
    vm.customize ["modifyvm", :id, "--cpus", 2 ]
  end

  config.vm.define "server" do |m|
    m.vm.provision "shell", inline: <<-SHELL
    sudo ansible-galaxy install -fr /vagrant/provisioning/requirements-server.yml
    sudo VARS_FILE=preferences-server-vars.yml \
         PYTHONUNBUFFERED=1 \
         ansible-playbook /vagrant/provisioning/playbook-server.yml
SHELL
    m.vm.box = "inclusivedesign/centos7"
    m.vm.network :private_network, ip: "192.168.50.10"
    m.vm.network "forwarded_port", guest: 8081, host: 8081
    m.vm.provider :virtualbox do |vm|
      vm.customize ["modifyvm", :id, "--memory", 1024 ]
    end
  end

  config.vm.define "fedora", autostart: false do |m|
    m.vm.provision "shell", inline: <<-SHELL
    sudo ansible-galaxy install -fr /vagrant/provisioning/requirements-fedora.yml
    sudo VARS_FILE=linux-framework-vars.yml \
         PYTHONUNBUFFERED=1 \
         ansible-playbook /vagrant/provisioning/playbook-fedora.yml
SHELL
    m.vm.provider :virtualbox do |vm|
      vm.customize ["modifyvm", :id, "--memory", 2048]
      vm.customize ["modifyvm", :id, "--cpus", 2]
      vm.customize ["modifyvm", :id, "--vram", "128"]
      vm.customize ["modifyvm", :id, "--accelerate3d", "on"]
      vm.customize ["modifyvm", :id, "--audio", "null", "--audiocontroller", "ac97"]
      vm.customize ["modifyvm", :id, "--ioapic", "on"]
      vm.customize ["setextradata", "global", "GUI/SuppressMessages", "all"]
    end
    m.vm.network :private_network, ip: "192.168.50.11"
    m.vm.box = "inclusivedesign/fedora23"
  end
  
  config.vm.define "windows", autostart: false do |m|
    m.vm.network :private_network, ip: "192.168.50.12"
    m.vm.box = "inclusivedesign/windows10-eval"
  end
end
