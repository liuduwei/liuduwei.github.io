---
title: Git操作备忘
date: 2020-10-21 16:08:32
tags: Git man
---

# push 到仓库

- git init
- git add .
- git commit
- git remote add [远程主机名] [url]
- git push origin

# 子仓库 push 只有箭头

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
