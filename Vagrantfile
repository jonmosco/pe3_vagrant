# -*- mode: ruby -*-
# vi: set ft=ruby
#
# Download PE and add it with the following command:
# vagrant pe-build copy <pe>
#
# Console info:
# Username: admin@puppetlabs.com
# Password: puppetlabs
#

## Version of Puppet Enterprise we are going to install
PE_VERSION='3.3.2'

$script = <<SCRIPT
echo 'export PATH=$PATH:/opt/puppet/bin' > /etc/profile.d/pe_path.sh
/sbin/service iptables stop
SCRIPT

## This environment requires a working and semi-sane DNS
## vagrant-hosts plugin will provide this
unless Vagrant.has_plugin?("vagrant-hosts")
  raise "This environment requires a sane DNS setup.  Please install
  the vagrant-hosts plugin"
end

Vagrant.configure('2') do |config|
  ## Increase our memory
  config.vm.provider "vmware_fusion" do |v|
    v.vmx["memsize"] = "1024"
  end

  ## Pupppet Master
  config.vm.define 'master' do |master|
    master.vm.box = 'centos64'
    ## Plugin defaults to 'master' as the hostname
    master.vm.hostname = 'master'
    master.vm.network :private_network, ip: "192.168.34.10"

    master.vm.provision "shell", inline: $script

    master.vm.provision :hosts do |provisioner|
      provisioner.autoconfigure = true
      provisioner.add_host '192.168.34.10', [
        'master',
        'master.example.com',
      ]
    end

    ## Version of PE we are installing
    config.pe_build.version = "#{PE_VERSION}"

    ## Install PE master, console, and DB
    master.vm.provision :pe_bootstrap do |provisioner|
      provisioner.role = :master
    end
  end

  ## Agent
  config.vm.define 'agent1' do |node|
    node.vm.box = 'centos64'
    node.vm.hostname = 'agent1.example.com'
    node.vm.network :private_network, ip: "192.168.34.11"

    node.vm.provision "shell", inline: $script

    node.vm.provision :hosts do |provisioner|
      provisioner.autoconfigure = true
      provisioner.add_host '192.168.34.10', [
        'master',
        'master.example.com',
        'puppet'
      ]
    end

    ## Install PE agent
    node.vm.provision :pe_bootstrap
  end
end
