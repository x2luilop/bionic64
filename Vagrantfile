# -*- mode: ruby -*-
# vi: set ft=ruby :

ubuntu_log_file = File.join(Dir.pwd, ".resources/tmp/ubuntu-bionic-18.04-cloudimg-console.log")
scripts_path = File.join(Dir.pwd, ".resources/scripts")

Vagrant.configure("2") do |config|

  config.vm.box = "ubuntu/bionic64"
  config.vm.hostname = "bionic64"
  config.vm.network "private_network", ip: "192.168.30.10"

  config.vm.synced_folder id: "idx1", "./code", "/var/www",
    :mount_options => ["dmode=777", "fmode=777"],
    :owner => 'vagrant', 
    :group => 'www-data'

  config.vm.synced_folder id: "idx2", "./encrypted", "/encrypted",
    :mount_options => ["dmode=777", "fmode=777"],
    :owner => 'vagrant', 
    :group => 'www-data'

  config.vm.synced_folder id: "idx3", "./task", "/var/task", 
    :mount_options => ["dmode=777", "fmode=777"]
    :owner => 'vagrant', 
    :group => 'www-data'

  config.vm.provider "virtualbox" do |vb|
    vb.customize ["modifyvm", :id, "--uartmode1", "file", ubuntu_log_file]
    vb.memory = 4096
    vb.cpus = 2
  end

  config.vm.provision "bootstrap", type: "shell" do |s|
    s.path = scripts_path + '/bootstrap.sh'
  end

  config.vm.provision "install-apache", type: "shell" do |s|
    s.path = scripts_path + '/install-apache.sh'
  end

  config.vm.provision "install-vhost", type: "shell" do |s|
    s.path = scripts_path + '/install-vhost.sh'
  end

  config.vm.provision "install-mysql", type: "shell" do |s|
    s.path = scripts_path + '/install-mysql.sh'
  end

  config.vm.provision "install-php", type: "shell" do |s|
    s.path = scripts_path + '/install-php.sh'
  end

  config.vm.provision "install-zend", type: "shell" do |s|
    s.path = scripts_path + '/install-zend.sh'
  end

  config.vm.provision "install-python", type: "shell" do |s|
    s.path = scripts_path + '/install-python.sh'
  end

  config.vm.provision "install-node", type: "shell", privileged: false do |s|
    s.path = scripts_path + '/install-node.sh'
  end

  config.vm.provision "install-aliases", type: "shell", privileged: false do |s|
    s.path = scripts_path + '/install-aliases.sh'
  end

end