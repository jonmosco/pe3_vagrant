#Puppet Enterprise Vagrant Environment

##Dependencies
* VMware Fusion
* Vagrant

##Vagrant Plugins
* Vagrant PE Build
  https://github.com/adrienthebo/vagrant-pe_build
* Vagrant Hosts
 https://github.com/adrienthebo/vagrant-hosts

##Usage
Download PE from puppetlabs.com

Add PE with the vagrant pe_build plugin:
```
$ vagrant pe-build add <path_to_pe_tar.gz>
```

```
$ vagrant up --provider=vmware_fusion
```

After boot, in order to use the PE environment without specifying the full
path, add the following on each node:

```shell
export PATH=$PATH:/opt/puppet/bin
```

After the environment has booted, you can browse to the Enterprise Console at:

  https://192.168.34.10

##Logging in

  Puppet Master:
  $ vagrant ssh master

  Puppet Node:
  $ vagrant ssh agent1

###TODO
* Add /opt/puppet/bin to the $PATH permanently
