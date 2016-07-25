---
layout: post
title: "Make Chef supprot more Platform"
date: 2016-07-25 03:05:01 +0000
comments: true
categories: [Chef, Ubuntu]
---

First , Change the attribute, set two plotform on this.

```ruby

default["apache"]["sites"]["johnny-hsu198323"] = {
  "site_title" => "johnny-hsu198323 websites coming soon!",
  "port" => 80,
  "domain" => "johnny-hsu198323.mylabserver.com"
}
	  
case node["platform"]
  when "centos"
  default["apache"]["package"]="httpd"
  when "ubuntu"
  default["apache"]["package"]="apache2"
end

```

And ,change the Recipes

```ruby assign the node for platform

if node["platfomr"] == "ubuntu"
  execute "apt-get update -y" 
end
  
package "apache2"  do
    package_name node["apache"]["package"]
end
	
```

Change 

```ruby  templatr location is different

if node["platform"] == "ubuntu"
  template_localtion = "/etc/apache2/sites-enabled/#{sitename}.conf"
  elsif node["platform"] == "centos"
  template_localtion = "/etc/httpd/conf.d/#{sitename}.conf"
end

```

```ruby Service name is also different

service "httpd" do
  service_name node["apache"]["package"]
  action [:enable, :start]
end
	
#include_recipe "php::default"
	

```
