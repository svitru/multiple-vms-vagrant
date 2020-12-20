# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "centos/7"

  config.vm.provision "shell" do |s|
    ssh_pub_key = File.readlines("#{Dir.home}/.ssh/id_rsa.pub").first.strip
    s.inline = <<-SHELL
      echo #{ssh_pub_key} >> /home/vagrant/.ssh/authorized_keys
    SHELL
  end

  (1..30).each do |i|
    config.vm.define "vm_#{i}" do |node|
      node.vm.hostname = "vm#{i}"
      node.vm.provider "virtualbox" do |v|
        v.name = "vmbox#{i}"
        v.cpus = 1
        v.customize ["modifyvm", :id, "--memory", "256"]
        v.customize ["modifyvm", :id, "--graphicscontroller", "vmsvga"]
        v.customize ["modifyvm", :id, "--vram", "16"]
        v.customize ["modifyvm", :id, "--vrde", "off"]
        v.customize ["modifyvm", :id, "--audio", "none"]
      end 
    end
  end

end
