# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  config.vm.box = "ubuntu/trusty64"
  config.vm.network "forwarded_port", guest: 3000, host: 3000

  config.vm.provider "virtualbox" do |vb|
    vb.memory = "1024"
  end
  config.vm.provision "shell", privileged: false, inline: <<-SHELL
    sudo apt-get update
    sudo apt-get install -y curl nodejs git
    export DEBIAN_FRONTEND=noninteractive
    sudo apt-get install -y mysql-server mysql-client libmysqlclient-dev
    sudo mysqladmin -u root password root
    unset DEBIAN_FRONTEND
    echo "unset rvm_path" >> ~/.bashrc
    echo "unset GEM_HOME" >> ~/.bashrc
    source ~/.bashrc
    gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3
    curl -sSL https://get.rvm.io | bash -s stable
    source /home/vagrant/.rvm/scripts/rvm
    rvm install 2.2.1
    rvm use 2.2.1
    gem install rails
    cd /vagrant/
    rails new app
    cd /vagrant/app/
    bundle install
    sudo locale-gen fr_FR.UTF-8
  SHELL
end
