# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://vagrantcloud.com/search.
  config.vm.box = "centos/7"
  # `vagrant box outdated`. This is not recommended.
  config.vm.box_check_update = true
  # config.vm.network "forwarded_port", guest: 80, host: 8080
  # config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"
  config.vm.network "private_network", ip: "192.168.33.10"
  config.vm.hostname = "centos7"
  # config.vm.network "public_network"
  # config.vm.synced_folder "../data", "/vagrant_data"
  config.vm.provider "virtualbox" do |vb|
  #   # Display the VirtualBox GUI when booting the machine
  #   vb.gui = true
     vb.cpus = "2"
     vb.memory = "4096"
     vb.name = "OneVMPuppetServer"
  end
  config.vm.provision "shell", inline: <<-SHELL
    rpm -ivh https://yum.puppetlabs.com/puppetlabs-release-pc1-el-7.noarch.rpm
    yum update
    yum -y install puppetserver ntpdate ruby rubygems mc git vim
    timedatectl set-timezone Europe/Kiev
    ntpdate 0.ua.pool.ntp.org
#    gem install puppet_forge
#    gem install semantic_puppet:0.1.0
#    gem install r10k
    /opt/puppetlabs/puppet/bin/gem install r10k
    echo ''':cachedir: '/var/cache/r10k'
:sources:
  cdp:
    remote: 'https://github.com/akopitsa/cdp1-control-repo.git'
    basedir: '/etc/puppetlabs/code/environments'
    prefix: false
''' >> /etc/puppetlabs/puppet/r10k.yaml
   /opt/puppetlabs/puppet/bin/r10k deploy environment production -pv -c /etc/puppetlabs/puppet/r10k.yaml
   /opt/puppetlabs/puppet/bin/r10k deploy environment development -pv -c /etc/puppetlabs/puppet/r10k.yaml
   SHELL
end
