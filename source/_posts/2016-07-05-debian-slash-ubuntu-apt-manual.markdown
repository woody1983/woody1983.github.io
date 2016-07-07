---
layout: post
title: "Debian/Ubuntu Apt Manual"
date: 2016-07-05 23:56:44 +0000
comments: true
categories: [Linux, Debian, Ubuntu]
---

### Update or Upgrade
```bash
apt-get update       #Update source
apt-get upgrade      #Update all installed packages
apt-get dist-upgrade #Update Distributions
```

### Install 
``` bash
apt-get install <pkg> #Install 
apt-get install --reinstall <pkg> #Install again
apt-get install -f <pkg> #Repair and install (dependency)
```

### Remove
``` bash
apt-get remove <pkg> # just remove 
apt-get purge <pkg>  #Remove include config files
```

### Download
``` bash
apt-get source <pkg>   #Download source code
apt-get download <pkg> #Download binary tar
apt-get source -d <pkg> #Download and Compile
apt-get build-dep <pkg> #Build pkg source code dependency environment (Compile Env?)
apt-get clean        #Cleanup Cache (/var/cache/apt/archives/{,partial}.)downloaded source code
apt-get autoclean #cleanup out of time source code within cache
apt-get autoremove  #Remove auto install dependency pkg
```

### Search
```bash
apt-cache status #Display system pkg total statistics information
apt-cache search <pkg>   #Search pkg by key words
apt-cache show <pkg_name> #display pkg more information
apt-cache depends <pkg> #Lookup pkg dependency software.
apt-cache rdepends <pkg> #View PKG is dependent on those packages
```


