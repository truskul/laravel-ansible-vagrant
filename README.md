# laravel-ansible-vagrant
The VM dedicated for a Laravel apps, provisioned by Ansible.

## The purpose
I needed the best and the most flexible solution, for develop my apps written in Laravel in the local environment. And that's the only reason, why i've decided to do it.

## Installed software
- Nginx
- MariaDB
- PHP 7.2 FPM
- Ansible
- Composer
In future, i'll add something else, according to needs. In most cases, i need only these ones.

## Default configuration
### Network configuration
The VM works on the default ports (80, 22), and uses `192.168.33.10` address as a private. The values to change are below:
```
    config.vm.network "forwarded_port", guest: 22, host: 22
    config.vm.network "forwarded_port", guest: 80, host: 80
    config.vm.network "private_network", ip: "192.168.33.10"
    config.vm.hostname = "laravel-vagrant-ansible"
```

### VM configuration
```
    config.vm.provider "virtualbox" do |vb|
        vb.memory = "2048"
        vb.cpus = "2"
    end
```

### Folder configration
I tried to design the most flat folder structure that is. The heart of the application is in the `app` folder. In addition, I have mapped the `vendor` folder to the default user, i.e.` vagrant`. All the rest remains supported by the http - nginx user.
```
  config.vm.synced_folder "./app", "/home/vagrant/laravel/app", type: "virtualbox", owner: "www-data", group: "www-data"
  config.vm.synced_folder "./app/vendor", "/home/vagrant/laravel/app/vendor", type: "virtualbox", owner: "vagrant", group: "vagrant"
```
If you would to add some new projects, just duplicate these two lines and change `app` directory.

## Installation

1. Clone repository
`git clone https://github.com/truskul/laravel-ansible-vagrant.git`

2. Install Vagrant
`https://www.vagrantup.com/`

3. Install vagrant-vbguest plugin, required to sync directories
`vagrant plugin install vagrant-vbguest`

4. Go to the cloned directory and run `vagrant up` command. Optionally, you can change the IP Address, or host name. Feel free to propose some customisations in the next versions. 

5. Add this record to `/etc/hosts` in your local machine. Of course, you've to remember about change a IP also, if you've changed it in a previous step.

`sudo echo '192.168.33.10   laravel.app' >> /etc/hosts`

6. If you need to do sth in your VM, log to the SSH by `vagrant ssh` command.

## What's next?

I've provisioned my VM, what can i do now? It's simple. Create your new project, or clone existing to `app` directory.

## License

[![MIT](https://img.shields.io/badge/license-MIT-0a0a0a.svg?style=flat&colorA=0a0a0a)](LICENSE)