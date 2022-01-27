---
title: linux device driver 环境搭建指北
date: 2022-01-04 14:23:15
tags: [LINUX-5.4.0, DRIVER]
cateories: LINUX
---
# NOTICE 
LINUX 驱动开发必须在搭载LINUCX系统或虚拟机上进行，WIN10自带WSL不支持。
## 本机开发环境搭建
本机开发指宿主机和目标机是一台主机，即在本机上开发编译然后在本机 上加载运行（Linux设备驱动也可以直接编译进内核，但为了开发工作方便，一般采用动态加载的方式）
step1:查看当前主机内核版本号
```
uname -r
```


