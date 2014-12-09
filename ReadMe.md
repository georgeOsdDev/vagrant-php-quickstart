For Start Nginx + PHP + MySQL

### Download

* Vagrant 1.6.5
 https://www.vagrantup.com/downloads.html

* ChefDK
 http://downloads.getchef.com/chef-dk/mac/#/


```
vagrant plugin install vagrant-berkshelf
vagrant plugin install vagrant-hostsupdater
vagrant plugin install vagrant-omnibus
vagrant box add centos63 https://s3.amazonaws.com/itmat-public/centos-6.3-chef-10.14.2.box
```

```
cd path/to/vagrant_workspace
# vagrant init centos65
gem install berkshelf
berks
vagrant up
vagrant ssh
```

Server application source code (`../../../cw-talk-mgmt` at host OS) will be synced as `/opt/src/nttcw/mgmtsv-cms` to guest OS(http://php.localhost).

This vagrant box provide only
* Nginx
* PHP
* PHP-FPM
* MySQL(with root user identified by `password`)
* Disable iptables

You need install some php-module, create database, configure nginx and php-fpm, etc depends on your project.
