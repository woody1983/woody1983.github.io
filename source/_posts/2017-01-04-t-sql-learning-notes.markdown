---
layout: post
title: "T-SQL Learning notes"
date: 2017-01-04 09:03:26 +0000
comments: true
categories: T-SQL
---

讲真，这也算是一种温习.

``` sql
SELECT orderid,orderdate,custid,empid  
From Sales.Orders where YEAR(orderdate) = 2007 and MONTH(orderdate) = 6;
-- 练习1 返回2007年6月的订单

SELECT orderid,orderdate,custid,empid From Sales.Orders where orderdate = eomonth(orderdate);
-- 练习2 返回每个月的最后一天的订单

SELECT custid, country,region,city FROM Sales.Customers WHERE region = N'WA'; 
-- 这种写法我也实在不理解!! 不会return null的列 也不会return任何WA的列 仅此而已 直接写 ='WA'结果一样

SELECT custid, country,region,city FROM Sales.Customers WHERE region <> N'WA'; -- 非null和非WA的

-- 字符排序
select * from hr.Employees where lastname = N'davis'; -- 不区分大小写
select * from hr.Employees where lastname collate Latin1_General_CS_AS =  N'davis'; -- return null

-- 字符串连接
select empid, firstname + N' ' + lastname As fullname from hr.Employees;
select custid,country,region,city, country+N','+region+N','+city As location from Sales.Customers;
/*
-- 标准SQL规定 连接NULL的结果应为NULL 所以只要任何一个row为null的话 location就会为null
所以需要一个自动将null变为空字符串的函数来做这个拼接动作
*/
select custid,country,region,city, CONCAT(country,N',',  region,N',',  city) from Sales.Customers;
-- 提取一个字符串
select SUBSTRING('abcde',1,3); -- 从第一个开始取3个  abc...
-- 左边3个 右边3个
SELECT LEFT('abcde',3);
-- len datalength 都会返回字符数量 后者不忽略空格
SELECT DATALENGTH(N'ABCDE '); -- 12
SELECT DATALENGTH(N'abcde '); -- 12 字节数
SELECT LEN(N'abcde '); -- 5 字符数 and 忽略空格
SELECT LEN(N'abcde f'); -- 7 不会忽略中间的空格!!!!!!

-- 返回某个字符串在目标字符中第一次出现的位置
SELECT CHARINDEX('y','woody'); -- 5
-- 返回某种模式第一次出现的位置 所谓模式就似乎 0-9 a-z 或者其他正则
select PATINDEX('%[0-9]%','abcde800efghijklmn');-- 6
-- replace
SELECT REPLACE('2016-12-12','-','/'); -- 2016/12/12
-- 计算lastname中e出现的次数 // thinking 将e变成空 len出来的字数会自动缩水 再由原来的长度来减
SELECT lastname, LEN(lastname) - LEN(REPLACE(lastname,'e','')) AS numoccur from HR.Employees;
```

>未完 持续更新中
