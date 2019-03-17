---
layout: post
title:  "How to customize you ubuntu system"
date:   2017-03-01
categories: [linux]
excerpt: "Ubuntu系统推荐软件和个性化配置"
tag:
- Linux
- Ubuntu 
comments: true
---

>This note records basic software need to be installed when you initialize 
your Ubuntu system for applied geophysicist and data scientist

说实话，系统习惯这种事情，千人千面各有所爱, 这里呢只是分享一点我自己使用的软件列表，
以供大家参考(不会告诉你是我自己怕忘）。

**系统安装**：
+ 如何包含uefi固态硬盘，一般给该系统efi 500M的存储空间

**去处左边的launcher:**
```
setting system-appearance-behavior-auto-hide the launcher on . then select
reveal location top left corner reveal sensitivity extremely low
```

**建议安装的基本软件:**
+ 输入法： sogou input
+ 办公软件： wps
+ 文献管理软件： Mendeley
+ 云盘:
    + Nutstore
    + Dropbox (Maybe blocked in China)
+ 娱乐 Spotify 
+ shell: [oh my zsh](https://github.com/robbyrussell/oh-my-zsh)
```
sudo apt-get install zsh
cat /etc/shells
chsh -s /usr/bin/zsh
```
+ autojump: 先apt-get install autojump 然后 在.zshrc 中plungin中加入autojump
+ 聊天: wechat

**建议安装的专业软件：**
+ 编译器
    + gcc
    + gfortran
    + g++ 
+ Latex文本： 
    + texlive
    + texlive-latex-extra
+ 临时terminal： guake
+ pdf处理神器：[cpdf](http://community.coherentpdf.com/)
+ editor：
    + vim-gtk better than vim-gnome
    + atom
    + vim-latexsuite 
+ 终端: terminator
+ 傅里叶： FFTW --enable-float
+ MPI: 
    +MPICH2
    + openmpi
+ 地震开源软件：
    + MADAGASCAR
    + SU: libx11-dev libxt-dev
+ 线性代数库：
    + LAPACK
    + BLAS
    + Atlas
+ C语言内存检验工具：Valgrind
+ 思维导图： XMind
+ 系统管理: indicator
+ screen recorder: Kazam
+ 美化:
    + [monaca font](https://github.com/cstrap/monaco-font) 
    + [icon and system theme](http://www.linuxidc.com/Linux/2016-09/135165.htm)
    + reveal.js
+ python必备： anaconda
+ 快速搜索： ag `apt-get install silversearcher-ag`
+ 系统管理： [htop](https://github.com/hishamhm/htop) 
+ shadowsocks-qt5
```
sudo add-apt-repository ppa:hzwhuang/ss-qt5
sudo apt-get update
sudo apt-get install shadowsocks-qt5
```
