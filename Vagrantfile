# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.

spacewalk_server_ip = "192.168.33.70"
spacewalk_admin_password = "KapimdakiNarMidur"

Vagrant.configure("2") do |config|

  config.vm.define "spacewalk_server" do |server|
    server.vm.box = "centos/7"
    server.vm.network "private_network", ip: spacewalk_server_ip
    server.vm.provision "ansible" do |ansible|
      ansible.playbook = "spacewalk-server.yml"
      ansible.extra_vars = {
        spacewalk_ip: "#{spacewalk_server_ip}",
        spacewalk_admin_password: "#{spacewalk_admin_password}",
      }
    end
  end

  config.vm.define "client" do |client|
    client.vm.box = "ubuntu/xenial64"
    client.vm.network "private_network", ip: "192.168.33.71"
    client.vm.provision "ansible" do |ansible|
      ansible.playbook = "spacewalk-client.yml"
      ansible.extra_vars = {
        spacewalk_ip: "#{spacewalk_server_ip}",
      }
    end
  end
end
