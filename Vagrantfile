# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "server-ready"
  #config.vm.box = "precise64"
  #config.vm.box_url = "http://files.vagrantup.com/precise64.box"

  config.ssh.forward_agent = true

  config.vm.define :web do |web_config|
    web_config.vm.host_name = 'web'
    web_config.vm.network :private_network, ip: "10.0.0.1"
    web_config.vm.synced_folder "./dota2rails", "/webapps/dota2rails"
    web_config.vm.network :forwarded_port, guest: 80, host: 8080

  end

  config.vm.define :mq do |mq_config|
    mq_config.vm.host_name = 'mq'
    mq_config.vm.network :private_network, ip: "10.0.0.1"
    mq_config.vm.synced_folder "./alacrity", "/mqapps/alacrity"
    #mq_config.vm.network :forwarded_port, guest: 80, host: 8080

  end

  config.vm.provision :ansible do |ansible|
    ansible.playbook = "ansible/playbook.yml"
    ansible.inventory_path = "ansible/hosts"
    ansible.verbose = true
    ansible.ask_sudo_pass = true
  end

end
