# -*- mode: ruby -*-
# vi: set ft=ruby :
VAGRANTFILE_API_VERSION = "2"

proxy = ENV['http_proxy'] || ""
proxys = ENV['https_proxy'] || ""
password = "ab55f208e802d03fc2f38a0d282b73f5"
hosts = {
  "server1" => "192.168.199.2",
  "server2" => "192.168.199.3",
  "server" => "192.168.199.10",
  "client" => "192.168.199.101"
}
servers = {
  "server1" => {
    "priority": 150,
    "interface": "enp0s8"
  },
  "server2" => {
    "priority": 100,
    "interface": "enp0s8"
  }
}

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "ubuntu/xenial64"

  config.vm.provider "virtualbox" do |vb|
    vb.memory = 1024
    vb.cpus = 1
  end

  config.vm.provision "shell",
    inline: "sudo apt-get -y install python",
    env: {
      http_proxy: proxy,
      https_proxy: proxys
    }

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "playbook.yml"
    ansible.groups = {
        "server" => ["server1", "server2"]
    }
    ansible.extra_vars = {
      servers: servers,
      password: password,
      hosts: hosts,
      proxy_env: {
        http_proxy: proxy,
        https_proxy: proxys
      }
    }
  end

  config.vm.define "server1" do |host|
      host.vm.hostname = "server1"
      host.vm.network "private_network", ip: hosts["server1"]
      host.vm.provider "virtualbox" do |vb|
        vb.name = "server1"
      end
  end

  config.vm.define "server2" do |host|
      host.vm.hostname = "server2"
      host.vm.network "private_network", ip: hosts["server2"]
      host.vm.provider "virtualbox" do |vb|
        vb.name = "server2"
      end
  end

  config.vm.define "client" do |host|
      host.vm.hostname = "client"
      host.vm.network "private_network", ip: hosts["client"]
      host.vm.provider "virtualbox" do |vb|
        vb.name = "client"
      end
  end

end
