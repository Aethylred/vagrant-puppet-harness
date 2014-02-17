# vagrant-puppet-harness

This is a Vagrant based development and testing harness developed for the [dynaguppy](dynaguppy) project. It bootstraps the installation of puppet and mounts the content of the `etc-puppet` in `/etc/puppet` of the Vagrant guest.
[dynaguppy]:https://github.com/Aethylred/dynaguppy

# Vagrant

This harness provisions a virtual machine using [Vagrant](vagrant) with [VirtualBox](vbox), though it could be configured to use a different Vagrant provisioner. Vagrant and VirtualBox will need to be installed and configured for your development and testing environment before the vagrant-puppet-harness can be used.
[vagrant]:http://www.vagrantup.com/
[vbox]:https://www.virtualbox.org/

## Vagrant Puppet Bootstrap Scripts

The Puppet bootstrap scripts in the `bootstrap` directory are from from the [Vagrant](vagrant) [puppet-bootstrap scripts](https://github.com/hashicorp/puppet-bootstrap) provided by [Hashicorp](http://www.hashicorp.com/).

The current `Vagrantfile` is configured to use the [Ubuntu NoCM Virtualbox box](http://puppet-vagrant-boxes.puppetlabs.com/ubuntu-server-12042-x64-vbox4210-nocm.box) from the [PuppetLabs box repository](http://puppet-vagrant-boxes.puppetlabs.com/)

## Getting started

1. Add the Vagrant box to your collection:  
```
vagrant box add ubuntu-12042-x64-vbox4210-nocm http://puppet-vagrant-boxes.puppetlabs.com/ubuntu-server-12042-x64-vbox4210-nocm.box
```
1. Clone the vagrant-puppet-harness:  
```
git clone https://github.com/Aethylred/vagrant-puppet-harness.git
```
1. Change into the vagrant-puppet-harness working directory:  
```
cd vagrant-puppet-harness
``` 
1. Initialise the vagrant-puppet-harness git submodules:  
```
git submodule sync
git submodule update --init --recursive
```
1. Create the `etc-puppet` shared directory (or clone or copy in an alternative Puppet configuration):
```
mkdir etc-puppet
```
1. Start the box:  
```
vagrant up
```
1. Log into the box as root (it's configured to use Vagrant's default connection on `127.0.0.1:2222`)
1. Check and/or install dependent Puppet modules, e.g. by running `librarian-puppet` in `/etc/puppet`.
1. The virtual machine is now ready for puppet development.

# Alternative usage

## Testing Puppet Manifests
Instead of creating an empty `etc-puppet` directory copy (or git clone) any existing puppet configuration into `etc-puppet` and run the `site.pp` manifest within the virtual machine with:  
```
puppet apply /etc/puppet/manivests/site.pp
```

## Testing Puppet Modules
Install the modules to be tested into `/etc/puppet/modules` either from within the virtual machine or from the host machine shared directory `etc-puppet/modules`. It is recommended that modules are installed with the `puppet module install` or using [`librarian-puppet`](https://github.com/rodjek/librarian-puppet) as this will install the modules with their dependencies. From there the module test manifests can be run from within the virtual machine with:  
```
puppet apply /etc/puppet/modules/<name>/tests/init.pp
```

# Installing Puppet Modules

This harness has been shown to work well with a number of methods of loading Puppet module dependencies. Methods that have been tested are:

* Include a `Puppetfile` and use [`librarian-puppet`](https://github.com/rodjek/librarian-puppet)
* Add Puppet modules as git submodules and run:  
```
git submodule sync
git submodule update --init --recursive
```
* Pull the modules down from the [Puppet Forge](http://forge.puppetlabs.com/) with:  
```
puppet module install <module>
```

# Questions & Answers

#### Why isn't dynaguppy a submodule?

In developing dynaguppy it was necessary to build the test harness, but not have it tied to a specific version or branch of dynaguppy. It was undesirable that endless and probably accidental commits that update, change, or otherwise tweak dynaguppy become part of vagrant-puppet-harness.

This has also made vagrant-puppet-harness more useful as it allows the harness to be used as a generic testing environment for Puppet.

#### Why is etc-puppet in `.gitignore`?

Give that it is undesirable that etc-puppet is a submodule, nor is it desirable that it is accidentally included in git commits.

# Licensing

This file is part of the vagrant-puppet-harness project.

The vagrant-puppet-harness is free software: you can redistribute it and/or modify it under the terms of the GNU General Public License as published by the Free Software Foundation, either version 3 of the License, or (at your option) any later version.

Foobar is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the GNU General Public License for more details.

A copy of the GNU General Public License is included with vagrant-puppet-harness in the `gpl.txt` file.  If not, see <http://www.gnu.org/licenses/>.

<a rel="license" href="http://www.gnu.org/licenses/"><img alt="Gnu General Public Licence 3" style="border-width:0" src="http://www.gnu.org/graphics/gplv3-88x31.png" /></a>
