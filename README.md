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

After boot, in order to use the PE environment, you have to add
/opt/puppet/bin to your $PATH

```shell
export PATH=$PATH:/opt/puppet/bin
```


###TODO
* Add /opt/puppet/bin to the $PATH permanently
