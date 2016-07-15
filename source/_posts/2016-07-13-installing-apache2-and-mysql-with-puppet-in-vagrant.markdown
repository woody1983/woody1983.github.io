---
layout: post
title: "Installing Apache2 &amp; MySQL with Puppet in Vagrant"
date: 2016-07-13 08:52:01 +0000
comments: true
categories: [Vagrant, Puppet, Ubuntu]
---

``` ruby Vagrantfile
Vagrant.configure("2") do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://atlas.hashicorp.com/search.
  config.vm.box = "precise32"
  config.vm.box_url = "http://files.vagrantup.com/precise32.box"

  # Setup for Web Server
  config.vm.define "web" do |web|
    web.vm.hostname = "web"
    web.vm.box = "apache"
    web.vm.network "private_network", type: "dhcp"
    web.vm.network "forwarded_port", guest: 80, host: 8080
    web.vm.provision "puppet" do |puppet|
      puppet.manifests_path = "manifests"
      puppet.manifest_file = "default.pp"
    end
  end

  # Setup for MySQL DB Server
  config.vm.define "db" do |db|
    db.vm.hostname = "db"
    db.vm.box = "mysql"
    db.vm.network "private_network", type: "dhcp"
  end


end
```

``` ruby manifests/default.pp
exec { "apt-get update":
        command => "/usr/bin/apt-get update",
}

package { "apache2":
        require => Exec["apt-get update"],
}

file { "/var/www":
         ensure => link,
         target => "/vagrant",
         force => true,
}
```
