---
layout: post
title: "Rush Vagrant on Ubuntu14.04 LTS"
date: 2016-07-12 06:33:38 +0000
comments: true
categories: [Vagrant, Ubuntu]
---

### Installing Virtualbox & Vagrant

``` bash
$ wget -q http://download.virtualbox.org/virtualbox/debian/oracle_vbox.asc
$ sudo apt-key add oracle_vbox.asc
$ sudo apt-get install virtualbox
$ sudo apt-get install vagrant
```

Install the dkms package to ensure that the VirtualBox host kernel modules

``` bash
$ sudo apt-get install virtualbox-dkms
```

### Get First Vagrant Machine

``` bash
$ vagrant box add precise32 http://files.vagrantup.com/precise32.box
$ vagrant box add precise64 http://files.vagrantup.com/precise64.box
```

### Configure Project

``` bash
$ mkdir vagrant_project
$ cd vagrant_project
$ vagrant init
```

And Edit the `Vagrantfile` file

``` bash
config.vm.box = "precise64"
#Synced Folder
config.vm.synced_folder "src/", "/vagrant_data"
#Forward Port
config.vm.network "forwarded_port", guest: 80, host: 8080
#Provision
config.vm.provision "shell", path: "provision.sh"
```

### Start Environment

``` bash
~/vagrant_project_64$ vagrant up
```

Shell Script

``` bash provision.sh
#!/usr/bin/env bash

echo "Installing Apache and setting apache up... please wait"
apt-get update > /dev/null 2>&1
apt-get install -y apache2 > /dev/null 2>&1

rm -rf /var/www
ln -fs /vagrant /var/www
```
