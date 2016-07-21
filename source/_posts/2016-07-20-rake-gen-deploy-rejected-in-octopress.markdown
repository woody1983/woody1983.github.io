---
layout: post
title: "rake gen_deploy rejected in Octopress"
date: 2016-07-20 23:07:53 +0800
comments: true
categories: [Ruby, git] 
---

I cloned my octopress blog Repository based on the github.pages. 
So , When i run `rake deploy` then I got a Error about 

```bash

## Pushing generated _deploy website
To https://github.com/woody1983/woody1983.github.io.git
 ! [rejected]        master -> master (non-fast-forward)
error: failed to push some refs to 'https://github.com/woody1983/woody1983.github.io.git'
hint: Updates were rejected because the tip of your current branch is behind
hint: its remote counterpart. Integrate the remote changes (e.g.
hint: 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.

```

I Googled a lot and finally solved this problem.

Change the current directory

```bash
cd octopress/_deploy
git pull origin master
cd ..
rake deploy
```