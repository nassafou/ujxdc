# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  # master server
  config.vm.define "mujx" do |mujx|
    mujx.vm.box = "ubuntu/xenial64"
    mujx.vm.hostname = "mujx"
    mujx.vm.box_url = "ubuntu/xenial64"
    mujx.vm.network :private_network, ip: "192.168.100.10"
    mujx.vm.provider :virtualbox do |v|
      v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      v.customize ["modifyvm", :id, "--memory", 4096]
      v.customize ["modifyvm", :id, "--name", "mujx"]
      v.customize ["modifyvm", :id, "--cpus", "2"]
    end
    config.vm.provision "shell", inline: <<-SHELL
      sudo apt -y install vim tree net-tools telnet git python3-pip
      sed -i 's/ChallengeResponseAuthentication no/ChallengeResponseAuthentication yes/g' /etc/ssh/sshd_config    
      service ssh restart
    SHELL
    mujx.vm.provision "shell", path: "install_common.sh"
    mujx.vm.provision "shell", path: "install_master.sh"
  end

  numberSrv=1
  # slave server
  (1..numberSrv).each do |i|
    config.vm.define "nodeujx#{i}" do |nodeujx|
      nodeujx.vm.box = "ubuntu/xenial64"
      nodeujx.vm.hostname = "nodeujx#{i}"
      nodeujx.vm.network "private_network", ip: "192.168.100.1#{i}"
      nodeujx.vm.provider "virtualbox" do |v|
        v.name = "nodeujx#{i}"
        v.memory = 1024
        v.cpus = 1
      end
      config.vm.provision "shell", inline: <<-SHELL
        sudo apt -y install vim tree net-tools telnet git python3-pip
        sed -i 's/ChallengeResponseAuthentication no/ChallengeResponseAuthentication yes/g' /etc/ssh/sshd_config    
        service ssh restart
      SHELL
      nodeujx.vm.provision "shell", path: "install_common.sh"
      nodeujx.vm.provision "shell", path: "install_node.sh"
    end
  end
end


