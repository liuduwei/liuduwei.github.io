---
title: Arch从gnome更换到Kdej
date: 2021-02-06 21:31:29
tags: Archlinux Kde
---

## 安装

sudo pacman -S sddm plasma kde-applications
sudo systemctl disable gdm
sudo systemctl enable sddm

先这样吧，暂时还有点问题，plasma 启动只显示桌面，折腾了一晚上，没有解决。。，本来说晚上学习的，结果搞成这样了
不得不说 sddm+gnome 真的丑到爆，中文字体扭的看都看不清楚
