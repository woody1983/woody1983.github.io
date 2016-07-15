---
layout: post
title: "Install Jenkins on CentOS 7"
date: 2016-07-15 04:22:21 +0000
comments: true
categories: [Linux, Jenkins] 
---

### First thing, ensure your server'8080 port is free

``` bash Download JDK by wget
wget --no-check-certificate --no-cookies --header "Cookie: oraclelicense=accept-securebackup-cookie" \
 http://download.oracle.com/otn-pub/java/jdk/8u25-b17/jdk-8u25-linux-x64.rpm
```

sudo root

``` bash Installing JDK
$rpm -Uvh jdk-8u25-linux-x64.rpm
```

Configuration JDK

``` bash
alternatives --install /usr/bin/java java /usr/java/latest/bin/java 200000
alternatives --install /usr/bin/javac javac /usr/java/latest/bin/javac 200000
alternatives --install /usr/bin/jar jar /usr/java/latest/bin/jar 200000

alternatives --config java
#Enter

#---Check or Verify
java -version
javac -version

```

``` bash /etc/rc.d/rc.local
#!/bin/bash
# THIS FILE IS ADDED FOR COMPATIBILITY PURPOSES
#
# It is highly advisable to create own systemd services or udev rules
# to run scripts during boot instead of using this file.
#
# In contrast to previous versions due to parallel execution during boot
# this script will NOT be run after all other services.
#
# Please note that you must run 'chmod +x /etc/rc.d/rc.local' to ensure
# that this script will be executed during boot.

touch /var/lock/subsys/local
export JAVA_HOME="/usr/java/latest"
```

### Installing Jenkins

``` bash Get Repo for Jenkins
sudo wget -O /etc/yum.repos.d/jenkins.repo http://pkg.jenkins.io/redhat-stable/jenkins.repo
sudo rpm --import http://pkg.jenkins.io/redhat-stable/jenkins.io.key
yum install jenkins

#Setup
systemctl enable jenkins.service

#Restart
systemctl restart jenkins.service
```

Take a look at http://localhost:8080