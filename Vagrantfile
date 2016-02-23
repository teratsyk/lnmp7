# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure(2) do |config|
  config.vm.box = "centos67"
  config.vm.box_url = "https://github.com/CommanderK5/packer-centos-template/releases/download/0.6.7/vagrant-centos-6.7.box"

  if Vagrant.has_plugin?("vagrant-vbguest") then
    config.vbguest.auto_update = false
  end

  config.vm.network :private_network, ip: '192.168.33.101'
  config.vm.hostname = "api.localhost"

  config.vm.provider :virtualbox do |vb|
    vb.gui    = false
    vb.memory = 2048
    vb.cpus   = 2
    # 共有ディレクトリ(synced_folder)でシンボリックリンクを許可する
    vb.customize ["setextradata", :id, "VBoxInternal2/SharedFoldersEnableSymlinksCreate/v-root", "1"]
  end

  config.vm.provision :ansible do |ansible|
    ansible.playbook = "./ansible/main.yml"
    ansible.inventory_path = "./ansible/hosts"
    ansible.raw_arguments  = [
      #"--extra-vars=\\\"target_host=development\\\"",
      "--private-key=./.vagrant/machines/default/virtualbox/private_key"
    ]
    ansible.limit = "all"
    ansible.verbose = "vvvv"
  end

end
