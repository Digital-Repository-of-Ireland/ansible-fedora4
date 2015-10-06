# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant::configure(VAGRANTFILE_API_VERSION) do |global_config|
  global_config.ssh.forward_agent = true
  global_config.ssh.insert_key = false  #new version of vagrant generates new key on vagrant up, we need to turn this off
  global_config.ssh.private_key_path = [ "~/.ssh/id_rsa", "~/.vagrant.d/insecure_private_key" ] #vagrant needs to be told of location of its private keys apparently
  global_config.hostmanager.enabled = true

  # below we configure single VM for full stack
  global_config.vm.define("fedora1.internal.tld") do |config|
    config.hostmanager.enabled = true
    config.hostmanager.manage_host = true
    config.hostmanager.ignore_private_ip = false
    config.hostmanager.include_offline = true
    config.vm.network :private_network, ip: "10.0.1.201"
#    config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"
    config.vm.hostname = "fedora1.internal.tld"
    config.vm.box_url = "https://vagrantcloud.com/ubuntu/boxes/trusty64/versions/14.04/providers/virtualbox.box"
    config.vm.box = "ubuntu/trusty64"

    config.vm.provider :virtualbox do |vb|
      vb.customize [
        "modifyvm", :id,
        "--name", "fedora1.internal.tld",
        "--memory", "1024",
        "--cpus", "1",
        "--natdnsproxy1", "off",
        "--natdnshostresolver1", "off"
      ]
      vb.customize ["setextradata", :id, "VBoxInternal1/SharedFoldersEnableSymlinksCreate/v-root", "1"]
      vb.customize [ "createhd", "--filename", "disk-fedora1", "--size", "5000" ]
      vb.customize [ "storageattach", :id, "--storagectl", "SATAController", "--port", 4, "--device", 0, "--type", "hdd", "--medium", "disk-fedora1.vdi" ]
    end

     # Here we need to create enough swap space in box. Its not there in default box
#    config.vm.provision "shell", path: "files/create_swap.vagrant.sh"

   end
   
   global_config.vm.define("fedora2.internal.tld") do |config|
    config.hostmanager.enabled = true
    config.hostmanager.manage_host = true
    config.hostmanager.ignore_private_ip = false
    config.hostmanager.include_offline = true
    config.vm.network :private_network, ip: "10.0.1.202"
    config.vm.hostname = "fedora2.internal.tld"
    config.vm.box_url = "https://vagrantcloud.com/ubuntu/boxes/trusty64/versions/14.04/providers/virtualbox.box"
    config.vm.box = "ubuntu/trusty64"

    config.vm.provider :virtualbox do |vb|
      vb.customize [
        "modifyvm", :id,
        "--name", "fedora2.internal.tld",
        "--memory", "1024",
        "--cpus", "1",
        "--natdnsproxy1", "off",
        "--natdnshostresolver1", "off"
      ]
      vb.customize ["setextradata", :id, "VBoxInternal2/SharedFoldersEnableSymlinksCreate/v-root", "1"]
      vb.customize [ "createhd", "--filename", "disk-fedora2", "--size", "5000" ]
      vb.customize [ "storageattach", :id, "--storagectl", "SATAController", "--port", 4, "--device", 0, "--type", "hdd", "--medium", "disk-fedora2.vdi" ]
    end
   


   # Here we need to create enough swap space in box. Its not there in default box
#    config.vm.provision "shell", path: "files/create_swap.vagrant.sh"

       #start ansible provisioning
    config.vm.provision :ansible do |ansible|
      ansible.raw_ssh_args = "-o ConnectionAttempts=3"
      ansible.playbook =  "site.yml"
      ansible.inventory_path = "inventory/hosts.vagrant"
      ansible.limit = 'all'
#      ansible.limit = 'fedora1.internal.tld' #limit to just vagrant VM incase other IPs might be present and cause damage to production etc
      ansible.verbose = 'vvvv'
    end

  
  end

end
