# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure(2) do |config|

    # k8s etcd 
    config.vm.define "k8s-etcd" do |etcd|

        ## the config
        # the box adn version
        etcd.vm.box = "geerlingguy/debian9"
        etcd.vm.box_version = "1.0.2"

        # Create a private network, which allows host-only access to the machine
        # using a specific IP.
        etcd.vm.network "private_network", ip: "192.168.33.10"

        # the host name 
        etcd.vm.hostname = "etcd"
        # the machine 
        etcd.vm.provider "virtualbox" do |e|
  
            # Customize the amount of memory on the VM:
            e.name = "k8s-etcd"
       
            # Display the VirtualBox GUI when booting the machine
            e.gui = false
           
            # Customize the amount of memory on the VM:
            e.memory = "256"
            e.cpus = "1"
        end
        # hosts
        etcd.vm.provision :hosts, :sync_hosts => true
        #etcd.vm.provision "shell", inline: <<-SHELL
        #SHELL
    end
    
    # k8s master
    config.vm.define "k8s-master" do |master|
        # the box name and version
        master.vm.box = "geerlingguy/debian9"
        master.vm.box_version = "1.0.2"
        # Create a private network, which allows host-only access to the machine
        # using a specific IP.
        master.vm.network "private_network", ip: "192.168.33.11"

        # the host name 
        master.vm.hostname = "master"
        # the machine 

        master.vm.provider "virtualbox" do |m|
  
            # Customize the amount of memory on the VM:
            m.name = "k8s-master"
       
            # Display the VirtualBox GUI when booting the machine
            m.gui = false
           
            # Customize the amount of memory on the VM:
            m.memory = "256"
            m.cpus = "1"
        end
        # hosts
        master.vm.provision :hosts, :sync_hosts => true
    end
    # k8s node 
    NODE_NUM = 3
    NODE_NUM.times do |hostno|
        config.vm.define "k8s-node#{hostno + 1}" do |host|
            host.vm.box = "geerlingguy/debian9"
            host.vm.box_version = "1.0.2"
            host.vm.hostname = "node#{hostno}"
            host.vm.network 'private_network', ip: "192.168.33.#{20 + hostno}"
            host.vm.provider 'virtualbox' do |vb|
                # Customize the amount of memory on the VM:
                vb.name = "k8s-node#{hostno + 1}"
                # Display the VirtualBox GUI when booting the machine
                vb.gui = false
                # Customize the amount of memory on the VM:
                vb.memory = "256"
                vb.cpus = "1"
            end
            host.vm.provision :hosts, :sync_hosts => true
        end
    end

    # for old versions
    Vagrant::DEFAULT_SERVER_URL.replace('https://vagrantcloud.com')  
  end