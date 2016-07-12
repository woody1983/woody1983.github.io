---
layout: post
title: "Rush Vagrant on Ubuntu14.04 LTS"
date: 2016-07-12 06:33:38 +0000
comments: true
categories: [Vagrant, Ubuntu]
---

### Installing Virtualbox & Vagrant

``` bash
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
```

### Start Environment

``` bash
~/vagrant_project_64$ vagrant up
```
