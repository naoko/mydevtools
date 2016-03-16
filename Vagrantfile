# -*- mode: ruby -*-
# vi: set ft=ruby :

# Please don't change it unless you know what you're doing.
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  vm_ip = "192.168.20.12"

  # Every Vagrant development environment requires a box.
  config.vm.box = "debian/jessie64"
  config.vm.provision "file", source: "~/.ssh/id_rsa", destination: "~/.ssh/id_rsa"

  # create sync folder
  # let default sync do: ~/projects/crm/ => /vagrant
  # https://www.vagrantup.com/docs/synced-folders/
  # config.vm.synced_folder ".", "/vagrant", type: "nfs",  mount_options: ['rw', 'vers=3', 'tcp', 'fsc' ,'actimeo=2']

  config.ssh.insert_key = false
  config.ssh.username = "vagrant"
  config.ssh.private_key_path = ['~/.vagrant.d/insecure_private_key']
  config.ssh.forward_agent = true
  config.ssh.forward_env = ["AUTOSTART"]

  # config.vm.hostname = "dev.crm.localhost"
  # portforward won't work with private_network
  config.vm.network "private_network", ip: vm_ip

  config.vm.provider "virtualbox" do |vb|
  	vb.name = "naoko.io"
  	vb.gui = false
  	vb.customize ["modifyvm", :id, "--cpus", 1]
	  vb.customize ["modifyvm", :id, "--memory", 2048]
    vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    vb.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
  end

  # Enable provisioning with a shell script.
  config.vm.provision "shell", inline: <<-SHELL
    sudo apt-get update
    sudo apt-get install vim ntp ntpdate -y
    sudo apt-get install python-pip git-all -y
    sudo apt-get install libpq-dev python-dev libffi-dev -y
    # ffi.h
    sudo apt-get install libffi-dev -y
    # for lxml
    sudo apt-get install libxml2 libxslt-dev -y
    sudo apt-get install debhelper dh-virtualenv -y
    sudo pip install make-deb
  SHELL
  #
  # config.vm.provision "ansible" do |ansible|
  #   # run ```vagrant provision``` for re-run
  #   ansible.playbook = File.expand_path("ansible/dev-provision.yml")
  #   ansible.limit = 'all'
  #   ansible.verbose = "v"
  #   ansible.extra_vars = {
  #       servername: vm_ip,
  #       force_remote_user: false,
  #     }
  # end

end

