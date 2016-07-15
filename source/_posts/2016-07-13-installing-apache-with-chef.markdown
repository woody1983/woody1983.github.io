---
layout: post
title: "Installing Apache with Chef"
date: 2016-07-13 03:48:11 +0000
comments: true
categories: [Vagrant, Ubuntu, Linux, Chef]
---

``` ruby Vagrantfile
  config.vm.provision "chef_solo" do |chef|
    chef.add_recipe "vagrant_la"
  end
```

#### Tree of Cookbooks

``` 
cookbooks:/
---/vagrant_la
   ---/recipes
      ---/default.rb
```

``` ruby default.rb
execute "apt-get update"
package "apache2"
execute "rm -rf /var/www"
link "/var/www" do
       to "/vagrant"
end
```