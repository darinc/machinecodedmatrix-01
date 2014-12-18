# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  
  config.vm.box = "hashicorp/precise32"

  config.ssh.forward_agent = true

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  config.vm.network :private_network, ip: "192.168.100.2"

  # web forwarding
  config.vm.network :forwarded_port, host: 10080, guest: 80
  config.vm.network :forwarded_port, host: 13000, guest: 3000

  # mongo forwarding
  config.vm.network :forwarded_port, host: 17017, guest: 27017
  config.vm.network :forwarded_port, host: 18017, guest: 28017

  #syncs entire project directory to ~/application on target machine
  config.vm.synced_folder "web", "/data/web"

  config.vm.provider "virtualbox" do |v|
    v.customize ["modifyvm", :id, "--memory", "2048"]
  end

  #provisions the environment
  config.vm.provision "ansible" do |ansible|
    ansible.raw_arguments = "-i provisioning/hosts"
    ansible.playbook = "provisioning/setup.yml"
  end
end
