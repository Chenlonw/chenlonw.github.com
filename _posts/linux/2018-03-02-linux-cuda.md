---
layout: post
title:  "Ubuntu16.04 如何手动安装cuda toolkit"
date:   2018-03-02
categories: [linux]
excerpt: "安装cuda toolkit的坑"
tag:
- cuda
- Ubuntu 
comments: true
---

> 本post主要是记录在安装cuda toolkit的时候遇到的一些坑， 记录下来以备后用。

之前电脑ubuntu出现过登录界面登录不进去的情况，少不更事的我做了很多努力，发现网上的solutions如同用了美图秀秀一样
看着好用实际上不起作用。 以至于一怒之下重装了系统，吐槽骂爹了很久。 后来才发现是由于显卡驱动问题导致的， 得知真相的我泪如泉涌。
不过这次主要是在安装tensorflow的时候需要cuDNN的支持，所以需要安装cuda toolkit, 注意事项如下：

+ 驱动和toolkit要分别安装，而且要相互匹配
+ 有人建议用runfile安装， 所以采用deb安装的小伙伴可以绕开休息了, 附上下载地址: [cuda toolkit](https://developer.nvidia.com/cuda-downloads)  

1. 直接安装`sudo sh cuda**.run` 报错
```
It appears that an X server is running. Please exit X before installation. If you're sure that X is not running, but are getting this error, please delete any X lock files in /tmp.
```
[*解决方案*](https://devtalk.nvidia.com/default/topic/831880/installing-the-nvidia-display-driver-/):
```bash
sudo rm /tmp/.X*-lock
sudo apt-get purge nvidia-*
sudo reboot
sudo service lightdm stop
press alt+F1 
sudo rmmod nvidia
sudo sh cuda_8.0.61_375.26_linux.run 
sudo service lightdm start
reboot
```
这里错误提示有变化
```
the nouveau kernel driver is currently in use by your system nvidia
```

2. 处理上述错误的[方式](https://askubuntu.com/questions/841876/how-to-disable-nouveau-kernel-driver)
```
sudo apt-get remove nvidia* && sudo apt autoremove
sudo apt-get install dkms build-essential linux-headers-generic
sudo vim /etc/modprobe.d/blacklist.conf
```
加入下面几句话
```
blacklist nouveau
blacklist lbm-nouveau
options nouveau modeset=0
alias nouveau off
alias lbm-nouveau off
```
然后继续
```
echo options nouveau modeset=0 | sudo tee -a /etc/modprobe.d/nouveau-kms.conf
sudo update-initramfs -u
reboot
modify PATH and LD_Library_PATH in envs
```
