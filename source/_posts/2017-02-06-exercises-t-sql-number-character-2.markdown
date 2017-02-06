---
layout: post
title: "Exercises T-SQL #Character 2"
date: 2017-02-06 08:00:41 +0000
comments: true
categories: t-sql
---

Exercises sample Query 

<!-- more -->

``` sql
-- 练习1
-- 返回2007年6月份的订单
SELECT orderid,orderdate,custid,empid 
FROM Sales.Orders where YEAR(orderdate) = 2007 and MONTH(orderdate)=6;

-- 练习2
-- 返回每个月最后一天的订单
SELECT orderid,orderdate,custid,empid FROM Sales.Orders where orderdate = EOMONTH(orderdate);

-- 练习3
-- 返回姓氏包含字母a两次以上的雇员
SELECT * FROM HR.Employees where (LEN(lastname) - LEN(REPLACE(lastname,'a',''))) > 1;

-- 练习4 
-- 返回总价大于10 000 的订单 按照总价排序
exec sys.sp_help @objname = N'Sales.OrderDetails';

select orderid, sum(qty * unitprice) as totalvalue  from Sales.OrderDetails 
group by orderid  having sum(qty * unitprice)> 10000 order by sum(qty * unitprice) desc;

-- 练习5
-- 返回2007年中平均运费最高的3个国家
select top(3) shipcountry, avg(freight) AS avgfreight   
from Sales.Orders 
where   YEAR(orderdate) = 2007 group by shipcountry order by avg(freight) desc;

-- 练习6
-- 分别对每个客户的订单按订单日期排序
-- 要用到窗口函数 
select custid,orderdate,orderid,
ROW_NUMBER() OVER(partition by custid order by orderdate, custid ) as rownum 
from Sales.Orders;

-- debug // ROW_NUMBER() OVER(order by custid) // 按照custid排序 rownum为连续计数 1-830
select custid,orderdate,orderid,ROW_NUMBER() OVER(order by custid) as rownum  from Sales.Orders;
-- debug // partition 按照custid分别计算行号 每一个custid对应的order 则需要单独order by排序
select custid,orderdate,orderid,ROW_NUMBER() OVER(partition by custid order by orderid) as rownum  from Sales.Orders;

-- 练习7
-- 推测性别 Ms. Mrs.-Female / Mr - Male
SELECT empid,firstname,lastname,titleofcourtesy,
case 
when titleofcourtesy = 'Mr.' then 'Male'
when titleofcourtesy = 'Ms.' then 'Female'
when titleofcourtesy = 'Mrs.' then 'Female'
else 'Unknown'
END AS gender from hr.Employees;

-- 练习8
-- 查询customers 返回id和地区 按地区排序输出行 具有null标记的行最后进行排序
-- region 要作为第二个排序列 第一个0和1 只是用来降序null
select custid,region from Sales.Customers order by case when region is null then 1 else 0 end ,region;
```
