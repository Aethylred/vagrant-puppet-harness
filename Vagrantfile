# -*- mode: ruby -*-
# vi: set ft=ruby :

# For the most part, this is a stock config from `vagrant init`

Vagrant.configure("2") do |config|
  # All Vagrant configuration is done here. The most common configuration
  # options are documented and commented below. For a complete reference,
  # please see the online documentation at vagrantup.com.

  # Every Vagrant virtual environment requires a box to build off of.
  config.vm.box = "ubuntu-12042-x64-vbox4210-nocm"
 
  # Share an additional folders to the guest VM.
  config.vm.synced_folder 'etc-puppet', '/etc/puppet',
    owner:  'root',
    group:  'root',
    create: true,
    mount_options: ['dmode=775','fmode=664']

  # Set up hostname, this breaks things for some reason!
  config.vm.hostname = "puppet.local"

  # Change boot timeout
  config.vm.boot_timeout = 120

  # Forwarded port mapping 
  # config.vm.network :forwarded_port, guest: 80, host: 8080
  config.vm.network :forwarded_port, guest: 8140, host: 8140

  # Create a private network
  # config.vm.network :private_network, ip: "192.168.33.10"

  # Create a public network
  # config.vm.network :public_network

  # Provision scripts to install software
  # Bootstrap puppet installation
  config.vm.provision :shell, :path => 'bootstrap/ubuntu.sh'

  # VirtualBox specific configuration
   config.vm.provider :virtualbox do |vb|
     # Don't boot with headless mode
     vb.gui   = false
     vb.name  = "Dynaguppy puppet.local"
  
     # Use VBoxManage to customize the VM. For example to change memory:
     vb.customize ["modifyvm", :id, "--memory", "1024"]
     vb.customize ["modifyvm", :id, "--ioapic", "on"]
     vb.customize ["modifyvm", :id, "--cpus", "2"] 
   end

end