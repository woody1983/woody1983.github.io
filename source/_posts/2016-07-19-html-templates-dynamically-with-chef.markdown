---
layout: post
title: "HTML Templates Dynamically with Chef"
date: 2016-07-19 07:42:33 +0000
comments: true
categories: Chef
---

Change the Recipes file

```ruby recipes/default.rb

template "/content/sites/#{sitename}/index.html" do
    source "index.html.erb"
	mode "0644"
	variables(
	    :site_title => data["site_title"],
		:comingsoon => "Coming Soon!"
	)
end

```

Adding something about HTMl element

```ruby attributes/default.rb

default["apache"]["sites"]["johnny-hsu19832"] = {
  "site_title" => "johnny-hsu19832 websites coming soon",
  "port" => 80,
  "domain" => "johnny-hsu19832.mylabserver.com"
}
	  
default["apache"]["sites"]["johnny-hsu19832b"] = {
  "site_title" => "johnny-hsu19832b websites coming soon!",
  "port" => 80,
  "domain" => "johnny-hsu19832b.mylabserver.com"
}			

```

```erb templates/default/index.html.erb

<html>
  <head>
      <title><%= @site_title %></title>
  </head>

<body>
  <h1><%= @site_title %></h1>
  <h2><%= @comingsoon %></h2>
</body>
</html>
			
```


