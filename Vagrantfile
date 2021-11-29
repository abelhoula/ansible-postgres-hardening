# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://vagrantcloud.com/search.
  config.vm.box = "centos/8"
  config.vbguest.auto_update = false
  config.vm.synced_folder ".", "/vagrant", disabled: true


  config.vm.provision "shell", inline: <<-SHELL
       yum update -y
  SHELL

  config.vm.define "local.dev" do |vm_cfg|

    # Hostname to access from the host machine
    vm_cfg.vm.hostname = "local.dev"
    vm_cfg.vm.network "private_network", ip: "10.0.0.2"
    
    #vm_cfg.vm.network "forwarded_port", guest: 5432, host: 5432

    config.vm.provider :virtualbox do |vb|
      vb.gui = false
      vb.customize ["modifyvm", :id, "--memory", "2048", "--cpus", "2"]   
    end
  end
end
