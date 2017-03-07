---
layout: post
title: "MySQL Replication #1236 Error"
date: 2017-02-22 07:46:47 +0000
comments: true
categories: MySQL
---

<div class="alert alert-info">
Last_IO_Errno: 1236
<p>Last_IO_Error: Got fatal error 1236 from master when reading data from binary log: 'Client requested master to start replication from impossible position'
</p>
</div>
解决方案就是跳到下一个Log

```
slave stop;
CHANGE MASTER TO
    MASTER_LOG_FILE='master-bin.000073',
    MASTER_LOG_POS=0
;
slave start;
show slave statusG
```

via [筆記: MySQL replication 問題 Client requested master to start replication from impossible position 解法](http://blog.ez2learn.com/2011/11/28/mysql-1236-solution/)
