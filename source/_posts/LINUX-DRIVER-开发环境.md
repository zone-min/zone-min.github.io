---
title: linux device driver 环境搭建指北
date: 2022-01-04 14:23:15
tags: [LINUX-5.4.0, DRIVER]
categories: LINUX
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

## 嵌入式开发环境搭建
这种开发中一般目标机为带有嵌入式处理器的开发板，而宿主机为PC，开发环境需要在宿主机上搭建，嵌入式Linux设备驱动开发的步骤如下(Cortex-A9架构的ARM开发板为例)：
step1:
在宿主机上下载嵌入式开发板对应版本Linux的源码，并解压：https://www.kernel.org/
tips：最好用开发板或核心板附带的源码包
```
# tar xvf linux-5.4.70.tar.gz
```
step2:编译内核
```
# apt install gcc-arm-linux-gnueabi make libncurses-dev bison flex
# cd linux-5.4.70
# make ARCH=arm vexpress_defconfig
# make ARCH=arm menuconfig
# make ARCH=arm CROSS_COMPILE=arm-linux-gnueabi- uImage LOADADDR=0x60003000
```
step3:编译生成设备树
```
# make ARCH=arm CROSS_COMPILE=arm-linux-gnueabi- dtbs
```
step4: 在当前源码目录编译Modules
```
make ARCH=arm CROSS_COMPILE=arm-linux-gnueabi- modules
```
step5: 安装 modules
```
make modules_install
```
