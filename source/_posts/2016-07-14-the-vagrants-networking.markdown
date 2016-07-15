---
layout: post
title: "The Vagrant's Networking"
date: 2016-07-14 01:37:44 +0000
comments: true
categories: Vagrant
---

You can Setup Private network or Public network on vagrant.

### Private networking

``` ruby Vagrantfile
Vagrant.configure("2") do |config|
  config.vm.network "private_network", type:"dhcp"
end
```

### Public networking

``` ruby Vagrantfile
#STATIC IP
config.vm.network "public_network",ip: "192.168.1.1"

#Default Interface
config.vm.network "public_network",bridge: 'eb1: Wi-Fi(AirPort)'
```