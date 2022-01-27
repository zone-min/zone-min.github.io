---
title: linux device driver
date: 2022-01-04 14:23:15
tags: [LINUX-5.04.70, DRIVER]
cateories: LINUX
---

## 概念
Linux内核从3.x开始引入设备树的概念，用于实现驱动代码与设备信息相分离。如在ARM-Linux内，一个.dts(device tree source)文件对应一个ARM的machine，一般放置在内核的"arch/arm/boot/dts/"目录内，比如exynos4412参考板的板级设备树文件就是"arch/arm/boot/dts/exynos4412-origen.dts"。这个文件可以通过$make dtbs命令编译成二进制的.dtb文件供内核驱动使用。基于同样的软件分层设计的思想，由于一个SoC可能对应多个machine，如果每个machine的设备树都写成一个完全独立的.dts文件，那么势必相当一些.dts文件有重复的部分，为了解决这个问题，Linux设备树目录把一个SOC公用的部分或者多个machine共同的部分提炼为相应的.dtsi文件。这样每个.dts就只有自己差异的部分，公有的部分只需要"include"相应的.dtsi文件, 这样就是整个设备树的管理更加有序。

## LINUX 驱动开发之HELLO WORLD！

hello.c

```c
#include <linux/module.h>
#include <linux/init.h>

// 当驱动被加载的时候，执行此函数
static int __init hello_init(void)
{
    printk(KERN_ALERT "welcome, hello\n");
    return 0;
}

// 当驱动被卸载的时候，执行此函数
static void __exit hello_exit(void)
{
    printk(KERN_ALERT "bye, hello\n");
}

// 版权声明
MODULE_LICENSE("GPL");

// 以下两个函数属于 Linux 的驱动框架，只要把驱动两个函数地址注册进去即可。
module_init(hello_init);
module_exit(hello_exit);
```

Makefile

```Makefile
ifneq ($(KERNELRELEASE),)
        obj-m := hello.o
else
        KERNELDIR ?= /home/workspace/linux-5.4.70
        PWD := $(shell pwd)
default:
        $(MAKE) -C $(KERNELDIR) M=$(PWD) modules
clean:
        $(MAKE) -C $(KERNEL_PATH) M=$(PWD) clean
endif
```
指定架构及编译选项（可修改Makefile, 之后补充）
```shell
make ARCH=arm CROSS_COMPILE=arm-linux-gnueabi-
````
## LINUX 驱动开发之SCULL