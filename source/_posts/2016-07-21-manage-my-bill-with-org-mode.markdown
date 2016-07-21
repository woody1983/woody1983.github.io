---
layout: post
title: "Manage My Bill with Org mode"
date: 2016-07-21 20:16:27 +0800
comments: true
categories: Emacs 
---

![orgmode](http://orgmode.org/img/org-mode-unicorn-logo.png)

Yeah, The [Org-mode](http://orgmode.org) is really awesome!
In this case, I want use the org-mode to manage my two credit card's information, So

####  First, I made the basic bill table

In Normal days, I choose using credit card or cash as my payment method, I also using Wechat-Pay and Ali-Pay, But in fact these are bound by the credit card.

```lisp
#+TBLNAME: 2016bill
| Date             | Category       | Amount | Payment     |
|------------------+----------------+--------+-------------|
| <2016-06-12 Sun> | Lunch          |  43.97 | Cash        |
| <2016-06-15 Wed> | Lunch          |  56.48 | Credit(BCM) |
| <2016-06-13 Mon> | Book           |  17.99 | Credit(BCM) |
| <2016-06-18 Sat> | Flico Keyboard | 289.18 | Credit(BCM) |
| <2016-06-19 Sun> | By Coffce      |  99.96 | Cash        |
| <2016-06-20 Mon> | Supplies       |  58.26 | Cash        |
| <2016-06-21 Tue> | Books          |  18.99 | Credit(CMB) |
| <2016-06-22 Wed> | Cookie         |   7.50 | Credit(CMB) |
| <2016-06-25 Sat> | Books          |  21.49 | Credit(CMB) |
| <2016-06-28 Tue> | VPS Service    |     10 | Credit(BCM) |
|------------------+----------------+--------+-------------|
|                  | Total:         | 623.80 |             |
#+TBLFM: @>$3=vsum(@2..@-1);%.2f
```

#### The `2016bill` table 

It just records the June 2016 payment info. And I make a other table `my-bull_bcm` to record The BCM Credit Card payment details.

```lisp
#+NAME: my-bill_bcm
#+BEGIN_SRC elisp :var tbl=2016bill val="Credit(BCM)" val2="<2016-06-15 Wed>" :colnames y
    (cl-loop for row in tbl
          when (equal (nth 3 row) val)
          collect row into newtbl
          finally return newtbl)
#+END_SRC

#+TBLNAME: my-bill_bcm
| Date             | Category         | Amount | Payment     |
|------------------+------------------+--------+-------------|
| <2016-06-15 Wed> | Supplies         |  56.48 | Credit(BCM) |
| <2016-06-13 Mon> | Book             |  17.99 | Credit(BCM) |
| <2016-06-18 Sat> | Kinesis Keyboard | 289.18 | Credit(BCM) |
| <2016-06-28 Tue> | Toner Service    |     10 | Credit(BCM) |
```

When I got the BCM Credit Card Payment information for the entire June. I need to know How much more money I will give to the Bank next month.

```lisp
| Year/Month       | amount |
|------------------+--------|
| [2016-June]      | 373.65 |
#+TBLFM: @>$2=vsum(remote(my-bill, @2$3..@>$3));%.2f
```

But It's not enough, Emacs and Org-mode is Powerfull. I need to learn more skills about Emacs.

#### Thanks SACHA, Thanks for your shared information and knowledge.

[Sacha Blog](http://sachachua.com/blog/) Living an Awesome Life.
