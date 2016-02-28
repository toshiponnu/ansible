# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  # https://cloud-images.ubuntu.com/
  config.vm.box = "ubuntu-trusty"
  config.vm.box_url = "https://cloud-images.ubuntu.com/vagrant/trusty/current/trusty-server-cloudimg-amd64-vagrant-disk1.box"
  config.vm.network :private_network, ip: "192.168.33.100"

  config.vm.synced_folder "./src", "/share", type: "rsync", rsync__auto: true, rsync__exclude: [".git/"]

  config.vm.provider :virtualbox do |vb|
    vb.gui = false
    vb.customize ["modifyvm", :id, "--memory", "1024"]
  end

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "./app1/site.yml"
    ansible.inventory_path = "./app1/development"
    ansible.limit = "all"
  end
end
