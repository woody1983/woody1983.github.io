---
layout: post
title: "About Preview on Octopress"
date: 2016-11-30 03:58:51 +0000
comments: true
categories: octopress
tags: octopress
---

>If I wanted to preview my OctoPress Blog on the An other client.

So I made one very minor change to the Rakefile. I had to change:

``` diff
-server_port     = "4000"      # port for preview server eg. localhost:4000
+server_host     = ENV['IP'] ||= '0.0.0.0'     # server bind address for preview server
+server_port     = ENV['PORT'] ||= "4000"      # port for preview server eg. localhost:4000

-  rackupPid = Process.spawn("rackup --port #{server_port}")
+  rackupPid = Process.spawn("rackup --host #{server_host} --port #{server_port}")
```

Take a try

Thank for [Max Lincoln Blog's post](http://devopsy.com/blog/2012/10/04/octopress-on-cloud9/)
 
