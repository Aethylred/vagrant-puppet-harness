# -*- mode: ruby -*-
# vi: set ft=ruby :

# For the most part, this is a stock config from `vagrant init`

Vagrant.configure("2") do |config|
  # All Vagrant configuration is done here. The most common configuration
  # options are documented and commented below. For a complete reference,
  # please see the online documentation at vagrantup.com.

  # Every Vagrant virtual environment requires a box to build off of.

  cores   = 2
  memory  = 1024
  if ARGV[1]
    name = ARGV[1]
  else
    name = 'puppet.local'
  end

  case ARGV[1]
  when 'ubuntu-1310'
    ubuntu            = true
    box               = 'puppetlabs/ubuntu-13.10-64-nocm'
    rspec_packages    = 'ruby-dev pkg-config libxml2-dev libxslt1-dev ruby-bundler augeas-tools augeas-lenses libaugeas-dev libaugeas-ruby rake rubygems'
    librarian_deps    = 'git'
    librarian_gems    = 'librarian-puppet'
    editor_packages   = 'joe'
    boot_wait         = 120
  when 'ubuntu-1404'
    ubuntu            = true
    box               = 'puppetlabs/ubuntu-14.04-64-nocm'
    rspec_packages    = 'ruby-dev pkg-config libxml2-dev libxslt1-dev ruby-bundler augeas-tools augeas-lenses libaugeas-dev libaugeas-ruby rake'
    librarian_deps    = 'git'
    librarian_gems    = 'librarian-puppet'
    editor_packages   = 'joe'
    boot_wait         = 120
  when 'centos-6'
    centos  = true
    box     = 'puppetlabs/centos-6.5-64-nocm'
    rspec_packages    = 'ruby-devel'
    librarian_deps    = 'git'
    librarian_gems    = 'librarian-puppet -v 1.0.3'
    editor_packages   = 'joe'
    boot_wait         = 120
  when 'centos-5'
    centos  = true
    box     = 'puppetlabs/centos-5.10-64-nocm'
    rspec_packages    = 'ruby-devel'
    librarian_deps    = 'git'
    librarian_gems    = 'librarian-puppet -v 1.0.3'
    editor_packages   = 'joe'
    boot_wait         = 120
  else
    ubuntu            = true
    box               = 'puppetlabs/ubuntu-12.04-64-nocm'
    rspec_packages    = 'ruby-dev pkg-config libxml2-dev libxslt1-dev ruby-bundler augeas-tools augeas-lenses libaugeas-dev libaugeas-ruby rake rubygems'
    librarian_deps    = 'git'
    librarian_gems    = 'librarian-puppet -v 1.0.3'
    editor_packages   = 'joe'
    boot_wait         = 120
  end

  config.vm.define name, primary: true do |puppet_local|
    puppet_local.vm.box_check_update = true
    puppet_local.vm.box = box
    # Share an additional folders to the guest VM.
    puppet_local.vm.synced_folder 'etc-puppet', '/etc/puppet',
      owner:  'root',
      group:  'root',
      create: true,
      mount_options: ['dmode=775','fmode=664']
    puppet_local.vm.boot_timeout = boot_wait
    if ubuntu
      # Set hostname
      puppet_local.vm.hostname = "puppet.local"
      # Install Puppet
      puppet_local.vm.provision :shell, :path => 'bootstrap/ubuntu.sh'
      # puts 'Install packages for rspec-puppet'
      # run bundle in your module directory if it has a Gemfile to prep for running spec tests.
      puppet_local.vm.provision :shell,
        inline: "apt-get -q -y install #{rspec_packages} > /dev/null"
      # puts 'Install requirements for librarian-puppet'
      puppet_local.vm.provision :shell,
        inline: "apt-get -q -y install #{librarian_deps} > /dev/null"
      # puts 'Install editor'
      puppet_local.vm.provision :shell,
        inline: "apt-get -q -y install #{editor_packages} > /dev/null"
    end
    if centos
      # Set hostnamem, breaks things for CentOS?
      # puppet_local.vm.hostname = "puppet.local"
      # Install Puppet
      case name
      when 'centos-5'
        puppet_local.vm.provision :shell, :path => 'bootstrap/centos_5_x.sh'
      when 'centos-6'
        puppet_local.vm.provision :shell, :path => 'bootstrap/centos_6_x.sh'
      end
      # puts 'Install packages for rspec-puppet'
      # run bundle in your module directory if it has a Gemfile to prep for running spec tests.
      puppet_local.vm.provision :shell,
        inline: "yum -y install #{rspec_packages} > /dev/null"
      # puts 'Install requirements for librarian-puppet'
      puppet_local.vm.provision :shell,
        inline: "yum -y install #{librarian_deps} > /dev/null"
      # puts 'Install editor'
      puppet_local.vm.provision :shell,
        inline: "yum -y install #{editor_packages} > /dev/null"
    end
    # puts 'Install librarian-puppet'
    puppet_local.vm.provision :shell,
      inline: "gem install --no-ri --no-rdoc #{librarian_gems} > /dev/null"
    # VirtualBox specific puppet_localuration
    puppet_local.vm.provider :virtualbox do |vb|
      # Don't boot with headless mode
      vb.gui   = false
      vb.name  = "Vagrant Puppet Harness puppet.local"

      # Use VBoxManage to customize the VM. For example to change memory:
      vb.customize ["modifyvm", :id, "--memory", memory]
      vb.customize ["modifyvm", :id, "--ioapic", "on"]
      vb.customize ["modifyvm", :id, "--cpus", cores] 
    end

    puppet_local.vm.provider :vmware_fusion do |v, override|
      v.gui = false
      v.vmx["memsize"]  = memory
      v.vmx["numvcpus"] = cores
    end

    puppet_local.vm.provider :vmware_workstation do |v, override|
      v.gui = false
      v.vmx["memsize"]  = memory
      v.vmx["numvcpus"] = cores
    end
  end

end
