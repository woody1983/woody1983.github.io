---
layout: post
title: "Mastering Github notes"
date: 2016-12-08 08:31:53 +0000
comments: true
categories: [CodeSchool, git, github]
---

![codeschool](https://d1ffx7ull4987f.cloudfront.net/images/achievements/large_badge/443/complete-mastering-github-e998c0ab56c79b9074ad5e3c1427691a.png)

## Level 1

相对比较Easy ,先fork [deadlyvipers/](https://github.com/deadlyvipers/dojo_rules)这个Repo先
然后提交一个 `introduction.md`的文件到`github/master`上 内容随便写写 不要为空即可

## Level 1.6

#### Task1/2
比较简单 就是提一个PR到[deadlyvipers/](https://github.com/deadlyvipers/dojo_rules) create完毕以后直接sumit答案.

#### Task 2/2
这关比较容易stuck 留意一下你刚才提的PR中 codeschool-kiddo是怎么评论你的

>Looks good! Could you also please mention your favorite Code School path in your introduction? This could be Ruby, JavaScript, HTML & CSS, iOS or Electives.

所以要在introduction,md文件里面添加一些课程的path进去   比如 Ruby （下次试试不加 * 号  否则 Level2.2 Task 3/4会自动submit）
update introduction.md 

```
git commit -am "Updated introduction.md"
git push origin master
```

<!-- more -->

然后1.6就过了

1.8 & 1.9 
就是练习常用的CL命令   git remote add  & git merge upstream/master

----------------------Level 2-----------------------
先添加codeschool家的kiddo一个process权限
In your fork of "dojo_rules", add the user "codeschool-kiddo" as a collaborator by granting Mastering Github access. Due to a change in the GitHub collaborator process, we'll need you to use this link rather than using the "Collaborators" section on GitHub.


2.2 Task2/4 
checkout一个新的branch  deadly_skills 不做任何改动  保持和master一致即可
然后push up 

Task 3/4 再更新一下introduction.md
git commit -am "Added deadly skills"
push up

Task 4/4 提一个PR 
在自己的repo里面   base:master  form deadly_skills

提完PR以后  submit以后   留意PR页面上  kiddo的一个comment
“Since you're becoming a GitHub master, could you also add "Killing history using git rebase" as one of your deadly skills?”
这句留在2.4的task去做的

提交后 task过关

2.4 就一个Task
Open up the "introduction.md" file, add rebase to your list of deadly skills and save the file.
Add and commit the file to your local git repository.
dojo_rules (deadly_skills) $ git commit -am "Added rebase to my list of deadly skills."
这个上一关的task 4/4就做了 所以直接提交后 过关。  但此时的PR还没有merge！！！

2.5 New Rules
task 1/3 We'll do all the work for this one! Just let us know your username.
所以直接提交submit answer 以后  过一会儿后 你会发现你多了一个PR # 先不要记得merge
Too many people are spilling coffee  #2  #####这个到底要不要merge掉？ 因为后面task 3/3 是让你关闭这个的 shit 做错了

task 2/3 kiddo已经把所有的文件修改已经提交到你repo的new_rules这个branch中  
checkout master ,pull down以后  多了一个branch在origin

root@f6d3b13b9967:~/github/dojo_rules# git branch -a
  deadly_skills
* master
  remotes/origin/HEAD -> origin/master
  remotes/origin/deadly_skills
  remotes/origin/gh-pages
  remotes/origin/master
  remotes/origin/new_rules

然后fixed掉  dojo_rules.md 里面的错误
git commit -am "Fixed spelling errors"
git push origin new_rules

task 2/3 过关

task 3/3 
你会发现 Too many people are spilling coffee  #2  这个PR里面你可以看到2次的commit
merge掉以后submit 过关

2.7 Closing Pull Reuqests By Merging
就一个task  checkout master & git pull 
然后将deadly_skills merge 到 master中

dojo_rules (master)$ git merge --no-ff deadly_skills -m "Merging in deadly_skills"
git push
这个时候  git lg

*   061ed99 (HEAD, origin/master, origin/HEAD, master) Merging in deadly_skills
|\
| * 41bc851 (origin/deadly_skills, deadly_skills) Added rebase to my list of deadly ski
| * 7363494 Added deadly skills
* |   6c4f609 Merge pull request #2 from woody1983/new_rules
|\ \
| |/
|/|

你会发现 #1 Added deadly skills 这个PR已经被closed掉了

看一下之前git log的线路

* 4db3fc6 (origin/new_rules, new_rules) Fixed spelling errors
* b87fa05 Added new rule about coffee
| * 41bc851 (origin/deadly_skills, deadly_skills) Added rebase to my list of deadly ski
| * 7363494 Added deadly skills
|/
* b39552c (HEAD, origin/master, origin/HEAD, master) Updated introduction.md
* d03a1b9 Added introduction.md
*   4a2cee3 Merge pull request #11 from githubteacher/master

Level 2结束了

---------------------Level 3 Tag----------------------
这个是目前的log tree
*   061ed99 (HEAD, origin/master, origin/HEAD, master) Merging in deadly_skills
|\
| * 41bc851 (origin/deadly_skills, deadly_skills) Added rebase to my list of deadly ski
| * 7363494 Added deadly skills
* |   6c4f609 Merge pull request #2 from woody1983/new_rules
|\ \
| |/
|/|
| * 4db3fc6 (origin/new_rules, new_rules) Fixed spelling errors
| * b87fa05 Added new rule about coffee
|/
* b39552c Updated introduction.md
* d03a1b9 Added introduction.md

所以3.2的Task 是要找的
`*   061ed99 (HEAD, origin/master, origin/HEAD, master) Merging in deadly_skills`  ???

root@f6d3b13b9967:~/github/dojo_rules# git log
commit 061ed990496611ef5e61e455f317bad3725870f3
Merge: 6c4f609 41bc851
Author: woody1983 <unix1983@gmail.com>
Date:   Thu Dec 8 03:02:26 2016 +0000

    Merging in deadly_skills

git checkout master 
git log  #061ed990496611ef5e61e455f317bad3725870f3
git checkout 061ed990496611ef5e61e455f317bad3725870f3
root@f6d3b13b9967:~/github/dojo_rules# git tag -a v1.2.0 -m "Creating v1.2.0 tag."
root@f6d3b13b9967:~/github/dojo_rules# git push origin --tags
Username for 'https://github.com': woody1983
Password for 'https://woody1983@github.com':
Counting objects: 1, done.
Writing objects: 100% (1/1), 164 bytes | 0 bytes/s, done.
Total 1 (delta 0), reused 0 (delta 0)
To https://github.com/woody1983/dojo_rules.git
 * [new tag]         v1.2.0 -> v1.2.0

submit !!! YES!!! 成功了!!!

3.4
Task 1/5
---------Checkout the v1.0.0 tag, use it to create release branch release_branch_1.0, and push to GitHub.

| | *   61fef70 (tag: v1.0.0) Merge pull request #3 from deadlyvipers/kill_list
| | |\
| | | * 73f81f9 We dont need to kill Budd
| | | * 0f85e77 Initial kill list

git checkout v1.0.0
git checkout -b release_branch_1.0
git push origin release_branch_1.0

Task 2/5
replace the assassin names in kill_list.md

git commit -m "replace the assassin names in kill_list.md"
git push origin release_branch_1.0

Task 3/5
Tag the fixed commit as v1.0.1, and push the tag up to GitHub.

git tag -a v1.0.1 -m "Tagging for release."
git push origin --tags

Task 4/5
Now that you've created the v1.0.1 tag, merge the release branch into master.
git checkout master
git merge release_branch_1.0
git push origin master

Task 5/5
Now that you've merged release_branch_1.0 you can tidy up your repo by deleting the branch locally and pushing that change to GitHub.

github branch -d release_branch_1.0
git push origin :release_branch_1.0

or

git branch -D release_branch_1.0

3.6  Releases in Github
Go to the releases tab, click on the v1.2.0 (deadly skills) tag, click on "Edit tag" button, add a release title and description for the release. Save this badge locally and upload it in the binaries section (not attached to the description!). Once you're happy with your changes, hit "Publish release".


----------------------------------- Level 4 Issues----------------------------------- 
4.2
Task 1/4
去 settings and checking the "Issues" checkbox

Task 2/4 
多了一个issue by kiddo
Go to your "dojo_rules" repository and you'll notice that we've created an issue for you. Create a local feature branch named "kill_list".
Make the fix to our issue on this branch and be sure to include "fixes #" in your commit message, using the issue number from GitHub.

git commit -am "fixes # Contribute to the Kill List #3"
git push origin kill_list

Task 3/4
Create a pull request from your new "kill_list" branch back to "master".

Task 4/4
We left a comment on your pull request giving you the A-OK. Go ahead and merge it back into master. You can use the Pull Request page on GitHub to make this easy. This will close the issue as well when your commit is added to master due to your commit message.

fixes # 后面跟着的是 issue numbers
PR一旦merge以后  该issue直接closed

4.4  Wiki Integration 
Task 1/3
Make sure the Wiki feature is enabled for your "dojo_rules" repository. It was enabled in the "deadlyvipers/dojo_rules" repository, so it should be for yours as well.
wiki这个功能应该跟随 deadlyvipers/dojo_rules 这个repo下来的 没有的话 自己去setting

Task 2/3
update README.md

Our "README.md" file on the master branch of our "dojo_rules" repository isn't very helpful. Update "README.md" to mention that "All members should read the rules".

Also include a link back to the deadlyvipers organization which started it all ("https://github.com/deadlyvipers").

Markdown 语法参考
https://help.github.com/articles/markdown-basics

Task 3/3
[![Build Status](https://secure.travis-ci.org/rails/arel.svg?branch=master)](http://travis-ci.org/rails/arel)
添加到wiki的homepage里面

4.6 Create a Github Page

4.7 woody1983.github.io/dojo_rules

---------------------- Level 5 ----------------------
5.2 Renaming a Repository 
If you rename a repository, collaborators will have to update their:
Nothing, they won’t have to update anything.

5.3 Default Settings
With the default settings, anyone can:
Create and comment on issues and Modify your wiki

5.4 Collaborators 
Collaborators  can Push to the project and merge pull requests.

Planned or In-Progress Work
If you want to see the work that needs to be done, you should check out the __issues___. If you want to see all the work that is being done and discussed you should check out the _pull requests__.

If you want to stop someone from being able to commit to the master branch, instead of adding them as a collaborator you must ask them to   fork the repository to make changes.
