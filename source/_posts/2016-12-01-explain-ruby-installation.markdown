---
layout: post
bootstrap_theme_url: http://bootswatch.com/flatly/bootstrap.min.css
title: "Explain Ruby Installation"
date: 2016-12-01 00:20:15 +0000
comments: true
categories: Ruby
---
<!-- more -->
<div class="alert alert-info">
    <p>
      <span class="glyphicon glyphicon-info-sign"></span>
在irb启动的时候加载一个rrbconfig的Ruby库 而RbConfig则是一个API接口，可以得到很多关于Ruby安装的内部变异的配置信息。
    </p>
</div>

`RbConfig::CONFIG` 是一个Hash类型的常量

```
root@mutiny:~# rvm 2.1.0
root@mutiny:~# ruby --version
ruby 2.1.0p0 (2013-12-25 revision 44422) [x86_64-linux]
root@mutiny:~# irb --simple-prompt -rrbconfig
>> RbConfig::CONFIG["bindir"]
=> "/usr/local/rvm/rubies/ruby-2.1.0/bin"
>> RbConfig::CONFIG["rubylibdir"]
=> "/usr/local/rvm/rubies/ruby-2.1.0/lib/ruby/2.1.0"
>> RbConfig::CONFIG["archdir"]
=> "/usr/local/rvm/rubies/ruby-2.1.0/lib/ruby/2.1.0/x86_64-linux"
>> RbConfig::CONFIG["sitedir"]
=> "/usr/local/rvm/rubies/ruby-2.1.0/lib/ruby/site_ruby"
>> RbConfig::CONFIG["vendordir"]
=> "/usr/local/rvm/rubies/ruby-2.1.0/lib/ruby/vendor_ruby"
>> RbConfig::CONFIG["sitelibdir"]
=> "/usr/local/rvm/rubies/ruby-2.1.0/lib/ruby/site_ruby/2.1.0"
>> RbConfig::CONFIG["sitearchdir"]
=> "/usr/local/rvm/rubies/ruby-2.1.0/lib/ruby/site_ruby/2.1.0/x86_64-linux"
```

Ruby标准库子目录rubylibdir 里面都是用ruby编写的小工具的源代码 没事可以上去看看
C语言扩展目录 RbConfig::CONFIG[“archdir“]
site_ruby是用来存储用户和管理员安装的第三方扩展库文件 该目录中也有用户自己写的程序文件以及下载的工具包
gems目录 如果找到了site_ruby其实也找到了gems的安装目录

#### 检查加载目录的方法

```
root@mutiny:~# ruby -e "puts $:"
/usr/local/rvm/rubies/ruby-2.1.0/lib/ruby/site_ruby/2.1.0
/usr/local/rvm/rubies/ruby-2.1.0/lib/ruby/site_ruby/2.1.0/x86_64-linux
/usr/local/rvm/rubies/ruby-2.1.0/lib/ruby/site_ruby
/usr/local/rvm/rubies/ruby-2.1.0/lib/ruby/vendor_ruby/2.1.0
/usr/local/rvm/rubies/ruby-2.1.0/lib/ruby/vendor_ruby/2.1.0/x86_64-linux
/usr/local/rvm/rubies/ruby-2.1.0/lib/ruby/vendor_ruby
/usr/local/rvm/rubies/ruby-2.1.0/lib/ruby/2.1.0
/usr/local/rvm/rubies/ruby-2.1.0/lib/ruby/2.1.0/x86_64-linux
```

<!-- more -->

再谈Load和require
严格来说require是请求一个功能 load更像是请求加载一个文件 从两者的使用风格上就可以看出来

``` ruby
load "loadee.rb"
require "./loadee.rb"
require_relative "loadee"
```

第三种方式 是搜索相对于所在文件的目录来加载功能。

### 常用Ruby工具

* ruby 解释器
* irb Ruby交互式解释器
* rdoc/ri Ruby文档工具
* rake Ruby的make工具 一套任务管理实用工具
* gem 一套Ruby库和应用程序包管理实用工具
* erb 一套模板系统
* testrb 一个用于测试框架的高级工具

### 解释器的命令行开关

* ruby -c 不执行 但检查语法
* ruby -w 运行中给出警告信息
* ruby -e “puts “Code” 执行引号内的代码
* ruby -v 显示版本信息并执行详细模式

### rake工具

`一个例子` Rakefile.rb rake必须使用Ruby语法定义的任务

``` ruby
namespace :admin do
    desc "Interactively delete all files in /tmp"
    task :clean_tmp do
        Dir["/tmp/*"].each do |f|
            next unless File.file?(f)
            print "Delete #{f}? "
            answer = $stdin.gets
            case answer
            when /^y/
                File.unlink(f)
            when /^q/
                break
            end
        end
    end							
end
```

还可以通过rake –tasks来查看已经定义过的任务列表，其实没有namespace也是可以的。
但是如果你任务比较多的话，可以用命名空间的方法来区分不同类型的tasks
