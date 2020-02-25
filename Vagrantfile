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

  config.vm.define "client-ubuntu-1604" do |c|
    c.vm.box = "ubuntu/xenial64"
    c.vm.hostname = "vagrant-ubuntu-test-client-01"
    c.vm.network "private_network", ip: "192.168.33.71"
    c.vm.provision "ansible" do |ansible|
      ansible.playbook = "spacewalk-client.yml"
      ansible.extra_vars = {
        spacewalk_ip: "#{spacewalk_server_ip}",
      }
    end
  end

  config.vm.define "client-centos-7" do |c|
    c.vm.box = "centos/7"
    c.vm.hostname = "vagrant-centos-test-client-02"
    c.vm.network "private_network", ip: "192.168.33.72"
    c.vm.provision "ansible" do |ansible|
      ansible.playbook = "spacewalk-client.yml"
      ansible.extra_vars = {
        spacewalk_ip: "#{spacewalk_server_ip}",
      }
    end
  end
end
