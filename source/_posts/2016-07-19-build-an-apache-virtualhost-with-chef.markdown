---
layout: post
title: "Build an Apache VirtualHost with Chef"
date: 2016-07-19 06:12:32 +0000
comments: true
categories: [Linux, Apache, Chef]
---

For this example, we need two Linux instances, I choose CentOS 7.

* mutiny-1.mylabserver.com 192.168.100.1 
* mutiny-2.mylabserver.com 192.168.100.100

#### Step 1 Build Chef Workstation

Download the `chef-starter.zip` to mutiny-1.mylabserver.com.

```bash
root$ hostname workstation
root$ exec bash

root$ cd
root$ unzip chef-starter.zip
root$ cd chef-repo

#-------------------------
#------Install Chef-------
#-------------------------
root$ curl -L https://www.opscode.com/chef/install.sh | sudo bash

#-------------------------
#------Install Node-------
#-------------------------
root$ knife bootstrap mutiny-2.mylabserver.com -x root -P __passwd__ -N linuxnode
```

#### Step 2 Create Cookbook

`knife cookbook create apache` Build a Cookbook based on apache

Just need install apache package

```ruby cookbook/apache/recipes/default.rb

package "httpd" do
  action :install
end

service "httpd" do
  action [:enable, :start]
end
```

`knife cookbook upload apache` Upload this cookbook to SaaS

`knife node run_list add linuxnode "recipe[apache]"` Add the recipes to run lists.

#### Step 3 At node, run chef-client

Just one command `chef-client`

#### Attributes & Template

We need setup two httpd.conf files for VirtualHost. So

```html templates/default/vhost.erb

#vhost template file
<% if @port == 80 -%>
  NameVirtualHost *:80
<% end -%>

<VirtualHost *:<%= @port %> >

  ServerName <%= @domain %>
  DocumentRoot <%= @document_root %>

  <Directory />
      Options FollowSymLinks
	  AllowOverride None
  </Directory>
  
  <Directory <%= @document_root %> >
      Options Indexes FollowSymLinks MultiViews
	  AllowOverride None
	  Order allow,deny
	  allow from all
  </Directory>

</VirtualHost>

```

```ruby attributes/default.rb

default["apache"]["sites"]["johnny-hsu19832"] = {
  "port" => 80,
    "domain" => "johnny-hsu19832.mylabserver.com"
	}
	
default["apache"]["sites"]["johnny-hsu19832b"] = {
  "port" => 80,
	"domain" => "johnny-hsu19832b.mylabserver.com"
	}
		
```

#### Run chef-client again!
