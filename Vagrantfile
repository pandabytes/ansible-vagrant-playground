Vagrant.configure("2") do |config|
  # ssh-keygen -t rsa
  # ssh-copy-id -i .ssh/id_rsa root@target_box

  # Master Ansible
  config.vm.define "ansible" do |ansible|
    ansible.vm.box = "bento/ubuntu-18.04"
    ansible.vm.hostname = 'ansible'

    ansible.vm.synced_folder "./ansible", "/vagrant_data"
    ansible.vm.network :private_network, ip: "192.168.56.101"

    ansible.vm.provision "shell", inline: <<-SHELL
      sudo apt update
      sudo apt install software-properties-common
      sudo apt-add-repository --yes --update ppa:ansible/ansible
      sudo apt install -y ansible
    SHELL

    ansible.vm.boot_timeout = 600

    ansible.vm.provider :virtualbox do |vb|
      vb.gui = false
    end
  end

  # Slave 1
  config.vm.define "slave1" do |slave1|
    slave1.vm.box = "bento/ubuntu-18.04"
    slave1.vm.hostname = 'slave1'

    slave1.vm.synced_folder "./slave1", "/vagrant_data"
    slave1.vm.network :private_network, ip: "192.168.56.102"

    slave1.vm.boot_timeout = 600
  end

  # Slave 2
  config.vm.define "slave2" do |slave2|
    slave2.vm.box = "ubuntu/trusty64"
    slave2.vm.hostname = 'slave2'

    slave2.vm.synced_folder "./slave2", "/vagrant_data"
    slave2.vm.network :private_network, ip: "192.168.56.103"

    slave2.vm.boot_timeout = 600
  end

	# @TODO: Windows VM
  # config.vm.define "win7" do |win7|
  #   win7.vm.box = "opentable/win-7-professional-amd64-nocm"
  #   win7.vm.hostname = 'slave2'

  #   win7.vm.synced_folder "./win7", "/vagrant_data"
  #   win7.vm.network :private_network, ip: "192.168.56.104"

  #   win7.vm.boot_timeout = 600
  #   win7.vm.provider :virtualbox do |vb|
  #     vb.gui = true
  #   end
  # end
end
