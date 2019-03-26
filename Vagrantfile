Vagrant.configure("2") do |config|
    config.vm.box = "williamyeh/ansible"
    config.vm.hostname = "laravel-ansible-vagrant"
    config.vm.box_check_update = true
    config.vm.network "private_network", ip: "192.168.33.10"
    config.vm.network :forwarded_port, guest: 22, host: 2244
    config.vm.network :forwarded_port, guest: 80, host: 80
  
    config.vm.network "public_network"
  
    config.vm.synced_folder ".", "/home/vagrant/laravel/app", :owner => "www-data", :group => "www-data"
    config.vm.synced_folder "./vendor", "/home/vagrant/laravel/app/vendor", :owner => "vagrant", :group => "vagrant"

    config.vm.provider "virtualbox" do |vb|
      vb.memory = "2048"
      vb.cpus = "2"
    end
    
    config.vm.provision "ansible" do |ansible|
      ansible.playbook = "ansible/playbook.yml"
    end
  end
  