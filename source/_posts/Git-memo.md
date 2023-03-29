---
title: Git操作备忘
date: 2020-10-21 16:08:32
tags: Git
---

# push 到远端

- git init
- git add .
- git commit
- git remote add [远程主机名] [url]
- git push origin [branch]

# push 到远端子文件夹显示为箭头

1. 删掉本地文件夹，备份
2. 正常 push 操作
3. 放入文件夹再进行 push（git add _)
   git add _ 忽略.gitgnore

# git 免密 push

## 方法一：https 记住密码

         git config --global credential.helper store

## 方法二：ssh

         git init
         git config --global user.name ''
         git config --global user.email ''
         ssh-keygen -t rsa
         cat ~/.ssh/id_rsa.pub

主页 setting 加入公钥

         git clone git@github.com:'project url'


# 从远端恢复本地删除的文件

> 今天误删了几个博客的子文件夹，以为很简单 git pull 就可以了，结果还是折腾了一番才恢复成功的,过程中也加深了对 git 的认识

      git reset --hard [v]把本地仓库暂存去全部修改为上一次commit（默      认)这个用来回复误删文件是最方便的了
