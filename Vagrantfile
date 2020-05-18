# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.provider "virtualbox" do |vb|
    vb.name = "docker"
    vb.memory = "4096"
  end

  config.vm.define "docker"
  config.vm.box = "centos/7"  
  config.vm.network "private_network", ip: "192.168.33.10"

  config.vm.network "forwarded_port", guest: 80, host: 80

  config.vm.provision "file", source: "src", destination: "src"
  config.vm.provision "file", source: "Dockerfile", destination: "Dockerfile"
  config.vm.provision "file", source: ".dockerignore", destination: ".dockerignore"
  config.vm.provision "file", source: ".gitignore", destination: ".gitignore"
  config.vm.provision "file", source: "nest-cli.json", destination: "nest-cli.json"
  config.vm.provision "file", source: "package.json", destination: "package.json"
  config.vm.provision "file", source: "package-lock.json", destination: "package-lock.json"
  config.vm.provision "file", source: "tsconfig.json", destination: "tsconfig.json"
  config.vm.provision "file", source: "tsconfig.build.json", destination: "tsconfig.build.json"
  config.vm.provision "file", source: "docker-compose.yml", destination: "docker-compose.yml"
  
  config.vm.provision "shell", inline: <<-SHELL
    # install docker
    sudo yum remove docker docker-client docker-client-latest docker-common docker-latest docker-latest-logrotate docker-logrotate docker-engine
    sudo yum install -y yum-utils device-mapper-persistent-data lvm2
    sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
    sudo yum install -y docker-ce docker-ce-cli containerd.io
    sudo systemctl start docker
    sudo usermod -aG docker vagrant

    # install docker-compose
    # sudo curl -L "https://github.com/docker/compose/releases/download/1.25.3/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
    sudo chmod +x /usr/local/bin/docker-compose

    sudo yum update -y
  SHELL
end
