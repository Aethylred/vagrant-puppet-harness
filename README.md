# dynaguppy-harness

This is a Vagrant based development and testing harness for the [dynaguppy](dynaguppy) project. It
[dynaguppy]:https://github.com/Aethylred/dynaguppy

# Vagrant

This harness sets up dynaguppy using [Vagrant](vagrant) to provisions virtual machines into [VirtualBox](vbox), though it could be configured to use a different Vagrant provisioner. Vagrant and VirtualBox will need to be installed and configured for your development and testing environment before the dynaguppy-harness can run.
[vagrant]:http://www.vagrantup.com/
[vbox]:https://www.virtualbox.org/

## Vagrant Puppet Bootstrap Scripts

The Puppet bootstrap scripts in the `bootstrap` directory are from from the [Vagrant](vagrant) [puppet-bootstrap scripts](bootstraps) provided by [Hashicorp](http://www.hashicorp.com/).
[bootstraps]:https://github.com/hashicorp/puppet-bootstrap

The current `Vagrantfile` is configured to use the box [Ubuntu NoCM Virtualbox](http://puppet-vagrant-boxes.puppetlabs.com/ubuntu-server-12042-x64-vbox4210-nocm.box) from the [PuppetLabs box repository](http://puppet-vagrant-boxes.puppetlabs.com/)

## Using the current Vagrant configuration

1. Add the Vagrant box to your collection:   
```
vagrant box add ubuntu-64-x64-vbox4210-nocm http://puppet-vagrant-boxes.puppetlabs.com/ubuntu-server-12042-x64-vbox4210-nocm.box
``` 
1.  Start the box:  
```
vagrant up
```

# Licensing

This file is part of the dynaguppy-harness project.

The dynaguppy-harness is free software: you can redistribute it and/or modify it under the terms of the GNU General Public License as published by the Free Software Foundation, either version 3 of the License, or (at your option) any later version.

Foobar is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the GNU General Public License for more details.

A copy of the GNU General Public License is included with dynaguppy-harness in the `gpl.txt` file.  If not, see <http://www.gnu.org/licenses/>.

<a rel="license" href="http://www.gnu.org/licenses/"><img alt="Gnu General Public Licence 3" style="border-width:0" src="http://www.gnu.org/graphics/gplv3-88x31.png" /></a>
