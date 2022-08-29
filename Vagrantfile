# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  # General configuration
  config.vm.box = "generic/rocky8"
  config.vm.synced_folder ".", "/opt/vagrant", disabled: true
  
  # Provision of PostgreSQL servers from MIN_VERSION to MAX_VERSION
  MIN_VERSION = 12
  MAX_VERSION = 14
  ansible_inventory_hosts_vars = {}

  (MIN_VERSION..MAX_VERSION).each do |version|
    config.vm.define "pgsql-#{version}" do |node|
      node.vm.provider "virtualbox" do |vm|
        vm.memory = 2048
        vm.cpus = 2
        vm.name = "pgsql-#{version}"
      end
      node.vm.hostname = "pgsql-#{version}"
      node.vm.network "private_network", ip: "192.168.56.#{version}"
      node.vm.network "forwarded_port", guest: "5432", host: "543#{version}"

      ansible_inventory_hosts_vars["pgsql-#{version}"] = "pg_version=#{version}"
      # Only execute once the Ansible provisioner
      if version == MAX_VERSION
        node.vm.provision :ansible do |ansible|
          ansible.playbook = "playbook.yml"
          ansible.limit = "all"
          ansible.host_key_checking = false
          ansible.host_vars = ansible_inventory_hosts_vars
        end
      end
    end
  end
end
