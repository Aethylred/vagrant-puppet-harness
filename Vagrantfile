# -*- mode: ruby -*-
# vi: set ft=ruby :

# For the most part, this is a stock config from `vagrant init`

Vagrant.configure("2") do |config|
  # All Vagrant configuration is done here. The most common configuration
  # options are documented and commented below. For a complete reference,
  # please see the online documentation at vagrantup.com.

  # Every Vagrant virtual environment requires a box to build off of.
  config.vm.box = 'ubuntu-12042-x64-vbox4210-nocm'
 
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

  # Create a private network
  # config.vm.network :private_network, ip: "192.168.33.10"

  # Create a public network
  # config.vm.network :public_network

  # Provision scripts to install software
  # Bootstrap puppet installation
  config.vm.provision :shell, :path => 'bootstrap/ubuntu.sh'

  # Install packages for rspec-puppet, run bundle in your module directory if it has a Gemfile to prep for running spec tests.
  config.vm.provision :shell,
    inline: 'apt-get -q -y install git ruby1.9.1-dev ruby-dev pkg-config libxml2-dev libxslt-dev ruby-bundler augeas-tools augeas-lenses libaugeas-dev libaugeas-ruby1.9.1 libaugeas-ruby rake rubygems joe > /dev/null'

  # Install requirements for librarian-puppet
  config.vm.provision :shell,
    inline: 'apt-get -q -y install git joe > /dev/null'
  config.vm.provision :shell,
    inline: 'gem install --no-ri --no-rdoc librarian-puppet'

  # VirtualBox specific configuration
  config.vm.provider :virtualbox do |vb|
    # Don't boot with headless mode
    vb.gui   = false
    vb.name  = "Vagrant Puppet Harness puppet.local"

    # Use VBoxManage to customize the VM. For example to change memory:
    vb.customize ["modifyvm", :id, "--memory", "1024"]
    vb.customize ["modifyvm", :id, "--ioapic", "on"]
    vb.customize ["modifyvm", :id, "--cpus", "2"] 
  end

  config.vm.provider :vmware_fusion do |v, override|
    override.vm.box = 'ubuntu-svr-12042-x64-vf503-nocm'
    v.gui = false
    v.vmx["memsize"] = "1024"
    v.vmx["numvcpus"] = "2"
  end

  config.vm.provider :vmware_workstation do |v, override|
    override.vm.box = 'ubuntu-svr-12042-x64-vf503-nocm'
    v.gui = false
    v.vmx["memsize"] = "1024"
    v.vmx["numvcpus"] = "2"
  end

end
