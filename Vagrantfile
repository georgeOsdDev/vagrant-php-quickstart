# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  # All Vagrant configuration is done here. The most common configuration
  # options are documented and commented below. For a complete reference,
  # please see the online documentation at vagrantup.com.

  # Every Vagrant virtual environment requires a box to build off of.
  config.vm.box = "centos63"

  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  # config.vm.network "private_network", ip: "192.168.33.10"
  config.vm.network :private_network, ip: "192.168.3.10"
  config.vm.hostname = "php.localhost"
  config.hostsupdater.aliases = ["php.localhost.com","php.localhost", "php.localhost.com"]
  # sync host OS's source directory with guest OS
  config.vm.synced_folder "/path/to/myapp", "/opt/src/myapp"
  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  config.vm.provider :virtualbox do |vb|
    vb.customize ["setextradata", :id, "VBoxInternal2/SharedFoldersEnableSymlinksCreate/v-root", "1"]
    vb.customize ["modifyvm", :id, "--memory", "1024"]
  end

  # Enable provisioning with chef solo, specifying a cookbooks path, roles
  # path, and data_bags path (all relative to this Vagrantfile), and adding
  # some recipes and/or roles.
  #
  config.omnibus.chef_version = :latest
  config.berkshelf.enabled = true
  config.vm.provision "chef_solo" do |chef|
    chef.cookbooks_path = [
      File.join(Dir.pwd, "site-cookbooks")
    ]
    chef.add_recipe "git"
    chef.add_recipe "iptables::disabled"
    chef.add_recipe "nginx"
    chef.add_recipe "php"
    chef.add_recipe "php-fpm"
    chef.add_recipe "yum-mysql-community::mysql56"
    chef.add_recipe "mysql-community-server"

    # You may also specify custom JSON attributes:
    chef.json = {
      "mysql-community-server" => {
        :root_password => "password"
      }
    }
  end

end
