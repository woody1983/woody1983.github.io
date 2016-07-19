---
layout: post
title: "Attribute Precedence"
date: 2016-07-19 07:20:01 +0000
comments: true
categories: Chef
---

![Levels of precedence](http://7xllrf.com1.z0.glb.clouddn.com/attributes.PNG)

## Key Concepts

>Attributes are specific details about a node.

### Attributes describe

* The current state of the node
* What the state of the node was at the end of the previous chef-client run
* What the state of the node should be at the end of the current chef-client run

After the node object is rebuilt in the chef run,all attributes loaded in the chef-client are then compared. The node is updated based on attribute precedence and at the very end of the convergence(chef-client)the node object is uploaded to the chef server

* Node object defines the current state of the node(made up of attributes)
* Node object is stored on the chef server so that can be searched
* Node object is updated at each convergence

If there are attributes with the same names then attributes precedence determines which attribute is applied to the node and the node object.

>Thanks Linux Academy.
