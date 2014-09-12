# Download PE and add it with the following command:
# vagrant pe-build copy <pe>
#
# Console info:
# Username: admin@puppetlabs.com
# Password: puppetlabs
#
# TODO
# add export PATH=$PATH:/opt/puppet/bin
#
$script = <<SCRIPT1
/sbin/service iptables stop
SCRIPT1

Vagrant.configure('2') do |config|

  ## Version of PE we are installing
  config.pe_build.version = '3.3.2'

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
