---
layout: post
bootstrap_theme_url: http://bootswatch.com/flatly/bootstrap.min.css
title: "Dockerの仕事の記録"
date: 2016-12-01 08:34:51 +0000
comments: true
categories: [Octopress, Ruby]
---

>今天遇到了一些比较古怪的事情，要记录下来免得以后再浪费我时间.

## Pick a Theme for Only One Page 
这个功能很有意思 应该是这个theme作者留的一个彩蛋

`source/_includes/custom/head.html` 修改这个文件

{% gist 152806322884b65ded244daff2faba5c %}

#### Example 

``` ruby example front 
---
layout: post
bootstrap_theme_url: http://bootswatch.com/flatly/bootstrap.min.css
title: "pick a theme for only one page"
comments: true
categories: octopress
---
```
<!-- more -->
## Docker container 关闭后再进入丢失path的问题

我今天重启了一下Docker的主机 然后重新login到container的时候报错 

```
root@f6d3b13b9967:/# rvm list
bash: rvm: command not found
```

Exo me? 逗我呢... `stackoverflow`查了一圈都没看到 估计是问题太easy了 然后回顾了一下`rvm`安装过程 可能是丢失了一个步骤 最后得知

```
root@f6d3b13b9967:/# source /etc/profile.d/rvm.sh
root@f6d3b13b9967:/# rvm list

rvm rubies

   ruby-1.9.3-p551 [ x86_64 ]
=* ruby-2.1.2 [ x86_64 ]
   ruby-2.3.0 [ x86_64 ]

# => - current
# =* - current && default
#  * - default
```

## Docker 编码|乱码问题

```
root@f6d3b13b9967:/# locale
LANG=
LANGUAGE=
LC_CTYPE="POSIX"
LC_NUMERIC="POSIX"
LC_TIME="POSIX"
LC_COLLATE="POSIX"
LC_MONETARY="POSIX"
LC_MESSAGES="POSIX"
LC_PAPER="POSIX"
LC_NAME="POSIX"
LC_ADDRESS="POSIX"
LC_TELEPHONE="POSIX"
LC_MEASUREMENT="POSIX"
LC_IDENTIFICATION="POSIX"
LC_ALL=
root@f6d3b13b9967:/# export LANG="en_US.UTF-8"
root@f6d3b13b9967:/# locale
LANG=en_US.UTF-8
LANGUAGE=
LC_CTYPE="en_US.UTF-8"
LC_NUMERIC="en_US.UTF-8"
LC_TIME="en_US.UTF-8"
LC_COLLATE="en_US.UTF-8"
LC_MONETARY="en_US.UTF-8"
LC_MESSAGES="en_US.UTF-8"
LC_PAPER="en_US.UTF-8"
LC_NAME="en_US.UTF-8"
LC_ADDRESS="en_US.UTF-8"
LC_TELEPHONE="en_US.UTF-8"
LC_MEASUREMENT="en_US.UTF-8"
LC_IDENTIFICATION="en_US.UTF-8"
LC_ALL=
```

懒得描述了~
