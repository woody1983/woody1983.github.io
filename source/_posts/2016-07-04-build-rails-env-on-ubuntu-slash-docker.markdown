---
Layout: post
title: "Build Rails Env on Ubuntu/Docker"
date: 2016-07-04 04:25:56 +0000
comments: true
categories: [Rails, Env, Ubuntu, Docker]
---
#### For PPA
``` bash
$ sudo apt-get install python-software-properties
$ sudo apt-get install software-properties-common
```

#### Ruby 2.2
``` bash
$ sudo apt-add-repository ppa:brightbox/ruby-ng
$ sudo apt-get update
$ sudo apt-get install ruby2.2
```

##### RedCloth 
``` bash
apt-get install make g++
gem install RedCloth -v '4.2.9'
```

### Octopress

Take a look on Offical site[Octopress](http://octopress.org/docs/blogging/)
