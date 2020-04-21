# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

    config.vm.define "docker" do |docker|
      docker.vm.box = "ubuntu/bionic64"
      docker.vm.network :"private_network", ip: "10.0.0.10"
      docker.vm.hostname = 'docker'
      docker.vm.provider :virtualbox do |v|
        v.customize ["modifyvm", :id, "--memory", 1024]
        v.customize ["modifyvm", :id, "--name", "docker"]
      end
      docker.vm.network "forwarded_port", id: "tomcat", guest: 8080, host: 8080
      docker.vm.provision "file", source: "keys/id_rsa.pub", destination: "/home/vagrant/.ssh/authorized_keys"
      docker.vm.provision "shell", inline: <<-SHELL
        apt-get update -y
        # chmod 400 /home/vagrant/.ssh/id_rsa.pub
        apt-get install docker -y
        apt-get install docker.io -y
        #add the vagrant user to the docker group, so that it doesn't need to sudo
        usermod -aG docker vagrant
        systemctl start docker
      SHELL
  
    end
  
  end
  