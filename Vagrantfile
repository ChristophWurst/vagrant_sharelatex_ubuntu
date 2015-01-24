# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  config.vm.box = "hashicorp/precise64"

  #make sharelatex available host port 8080
  config.vm.network "forwarded_port", guest: 3000, host: 8080

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  config.vm.provider "virtualbox" do |vb|
    vb.memory = "1024"
  end
  #

  # Define a Vagrant Push strategy for pushing to Atlas. Other push strategies
  # such as FTP and Heroku are also available. See the documentation at
  # https://docs.vagrantup.com/v2/push/atlas.html for more information.
  # config.push.define "atlas" do |push|
  #   push.app = "YOUR_ATLAS_USERNAME/YOUR_APPLICATION_NAME"
  # end

  config.vm.provision "shell", inline: <<-SHELL
    sudo apt-get update
    sudo apt-get -y install git build-essential curl python-software-properties zlib1g-dev zip unzip

    #install node.js
    sudo apt-add-repository -y ppa:chris-lea/node.js
    sudo apt-get update
    sudo apt-get -y install nodejs
    #npm
    sudo npm install -g grunt-cli

    #install redis
    sudo apt-add-repository -y ppa:chris-lea/redis-server
    sudo apt-get update
    sudo apt-get -y install redis-server
    sudo sed -i 's/^appendonly no/appendonly yes/' /etc/redis/redis.conf
    sudo service redis-server restart

    #install mongodb
    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 7F0CEB10
    echo 'deb http://downloads-distro.mongodb.org/repo/ubuntu-upstart dist 10gen' | sudo tee /etc/apt/sources.list.d/mongodb.list
    sudo apt-get update
    sudo apt-get -y install mongodb-org

    #install aspell
    sudo apt-get -y install aspell

    #install sharelatex
    wget -q https://github.com/sharelatex/sharelatex/releases/download/v0.1.0/sharelatex_0.1.0_amd64.deb
    sudo dpkg -i sharelatex_0.1.0_amd64.deb

    #install TeXLive
    wget -q http://mirror.ctan.org/systems/texlive/tlnet/install-tl-unx.tar.gz
    tar -xvf install-tl-unx.tar.gz
    cd install-tl-*
    echo "1" | sudo ./install-tl
    export PATH=/usr/local/texlive/2014/bin/x86_64-linux:$PATH

  SHELL
end
