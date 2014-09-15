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
$ vagrant pe-build copy <path_to_pe_tar.gz>
```

Set the version of Puppet Enterprise you will be installing
```ruby
PE_VERSION = '3.3.x'
```

Boot the envionment with the VMware Fusion provider
```
$ vagrant up --provider=vmware_fusion
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
