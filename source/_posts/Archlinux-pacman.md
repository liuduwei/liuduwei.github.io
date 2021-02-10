---
title: Archlinux卸载软件
date: 2021-02-07 16:05:17
tags: Archlinx
---

# 安全卸载软件包及其依赖

sudo pacman -Rs
sudo pacman -R \$(pacman -Qdtq)
sudo pacamn -Rsu
