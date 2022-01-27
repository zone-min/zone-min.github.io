---
title: ARM-LINUX之开发环境
date: 2021-12-20 09:36:51
tags: [ARM,LINUX]
categories: ARM
---

## LINUX 常用开发工具

### 1.git安装配置

``` zsh
$ sudo apt-get install git
$ git config --global user.name "xxx"
$ git config --global user.email "xxx@email.com"
```

xxx 替换成自己用户名和绑定邮箱

### 2.生成SSH秘钥

```zsh
$ ssh-keygen -t rsa -C "xxx@email.com" 
$ cat  ~/.ssh/id_rsa.pub
```
在github账号添加SSH密钥[GitHub](https://github.com/settings/keys).

### 3.some notes for hexo error

ttp://localhost:4500 本地host无法打开

原因：端口号被占用，hexo默认端口为4000

解决方案：指定hexo为其他端口

``` bash
hexo s -p 4500
```