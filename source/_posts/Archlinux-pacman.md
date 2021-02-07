---
title: Archlinux垃圾清理
date: 2021-02-07 16:05:17
tags: Archlinx Pacman
---

# 安全卸载软件包及其依赖

sudo pacman -Rs
sudo pacman -R \$(pacman -Qdtq)
