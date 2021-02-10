---
title: Grub-memo
date: 2020-10-21 13:45:34
tags: Grub
---
> 不小心把Archlinux弄挂了

# Grub修复引导
1.**_进入 normal 模式:_**

-     set
-     ls (hdx,y)/boot/grub/
-     set root=(hdx,y)
-     set prefix=(hdx,y)/boot/grub/
-     insmod normal
-     normal
  2.**_启动 arch 重装 grub:_**
-     grub-install --target=x86_64-efi --efi-directory=/boot/EFI --bootloader-id=GRUB

-     grub-mkconfig -o /boot/grub/grub.cfg

3.**_重启结束_**

# 更换主题

直接下载主题，解压进入目录执行:

    sudo ./install.sh

# win10+arch 双引导:

挂在 win10 所在的 efi 目录,直接重新生 grubconfig 文件
