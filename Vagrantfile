# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  config.vm.box = "bento/ubuntu-22.04"
  config.vm.boot_timeout = 600  # Esperar 5 minutos

  config.vm.define :n1 do |node|
    node.vm.hostname = "n1"
    node.vm.network :private_network, ip: "192.168.75.6"
    
    node.vm.provider "virtualbox" do |vb|
      vb.memory = "1024" # 1GB
      vb.cpus = 2 # 2 Nucleos
    end

    node.vm.provision "ansible_local" do |ansible|
      # Playbook
      ansible.playbook = "client.yml"
      # Variables de Ansible
      ansible.extra_vars = {
        ipv4: "192.168.75.6"
      }
    end
  end

  config.vm.define :n2 do |node|
    node.vm.hostname = "n2"
    node.vm.network :private_network, ip: "192.168.75.7"
    
    node.vm.provider "virtualbox" do |vb|
      vb.memory = "1024"
      vb.cpus = 2
    end
    
    node.vm.provision "ansible_local" do |ansible|
      ansible.playbook = "client.yml"
      ansible.extra_vars = {
        ipv4: "192.168.75.7"
      }
    end
  end

  config.vm.define :haproxy do |server|
    server.vm.hostname = "haproxy"
    server.vm.network :private_network, ip: "192.168.75.5"
    
    # Limitar la maquina virtual
    server.vm.provider "virtualbox" do |vb|
      vb.memory = "1024"
      vb.cpus = 2
    end

    # Configuracion de aprovisionamiento con ansible
    server.vm.provision "ansible_local" do |ansible|
      # Definir Playbook de ansible a usar
      ansible.playbook = "server.yml"
      # Definir la IP de la variable de ansible para usar en los templates
      ansible.extra_vars = {
        ipv4: "192.168.75.5"
      }
    end
  end
end
