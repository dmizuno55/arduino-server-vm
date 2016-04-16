# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  config.vm.box = "ARTACK/debian-jessie"

  config.vm.network "private_network", ip: "192.168.33.10"

  config.vm.provider "virtualbox" do |vb|
    vb.customize ["modifyvm", :id, "--usb", "on"]
    vb.customize ["modifyvm", :id, "--usbehci", "off"]
    vb.customize ["modifyvm", :id, "--usbxhci", "off"]
    vb.customize ["usbfilter", "add", "0",
                  "--target", :id,
                  "--name", "Arduino Nano",
                  "--vendorid", "0x1A86",
                  "--productid", "0x7523"]
  end

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "playbooks/site.yml"
    ansible.inventory_path="playbooks/hosts"
    ansible.limit = "all"
  end
end
