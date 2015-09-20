# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  if Vagrant.has_plugin?("vagrant-cachier")
    config.cache.scope = :box
  end
  if Vagrant.has_plugin?("vagrant-vbguest")
    config.vbguest.auto_update = true
  end

  # Vagrant Box information
  config.vm.box = "centos7"
  config.vm.box_url = "https://github.com/holms/vagrant-centos7-box/releases/download/7.1.1503.001/CentOS-7.1.1503-x86_64-netboot.box"
  config.ssh.insert_key = false
  config.ssh.forward_agent = true

  # Virtualbox provider information
  config.vm.provider :virtualbox do |vb|
    vb.name = "mysql"
    vb.memory = 512
    vb.cpus = 1
    vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    vb.customize ["modifyvm", :id, "--ioapic", "on"]

    database_vdi = "#{Dir.home}/.database.vdi"

    unless File.exist?(database_vdi)
      vb.customize ['createhd', '--filename', database_vdi, '--size', 20 * 1024]
    end
    vb.customize ['storageattach', :id, '--storagectl', 'SATA Controller', '--port', 1, '--device', 0, '--type', 'hdd', '--medium', database_vdi]

  end

  # Networking
  config.vm.hostname = "mysql"
  config.vm.network :private_network, ip: "192.168.56.101"

  # Set the name of the VM. See: http://stackoverflow.com/a/17864388/100134
  config.vm.define :mysql do |mysql|
  end

  # Ansible provisioner.
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "playbook.yml"
    ansible.inventory_path = "inventory"
    ansible.limit = "db"
    # Having trouble? Uncomment below to troubleshoot.
    # ansible.verbose = "vvvv"
  end

end
