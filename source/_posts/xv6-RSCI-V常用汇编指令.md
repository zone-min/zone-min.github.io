---
title: xv6-RSCI-V常用汇编指令
date: 2021-12-20 15:19:45
tags: [OS,RSCI-V]
categories: XV6
---
## RISC-V REGS
下图为xv6的栈的结构图，其中每一个区域都是一个Stack Frame，每执行一次函数调用就会产生一个Stack Frame,它使得我们的函数变得有组织，且能够正常返回。
![stack frame](stack.png)
Caller Saved寄存器在函数调用的时候不会保存
Callee Saved寄存器在函数调用的时候会保存
![REGS](RISC-V_regs.png)

## INSTRACTIONS

```ASM
add rd, rs1, rs2  # X[rd] = X[rs2] + X[rs2]
```


![ins1](3.jpg)
![ins2](4.jpg)
