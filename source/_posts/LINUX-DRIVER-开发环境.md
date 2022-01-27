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
step2: 查看当前宿主机所有源码版本
```
 apt-cache search linux-source
```
step3:根据宿主机内核版本号下载相应内核源码
```
sudo apt-get install linux-source-$(shell uname -r)
```
step4:配置内核,默认即可，也可采用原始配置单内存占用可能比较大
```
make menuconfig //图形配置

make oldconfig //原始配置
```
step5: 编译Modules
```
make modules
```
step6: 安装 modules
```
make modules_install
```


