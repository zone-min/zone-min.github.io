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
### 4.Miniconda软件安装教程（Linux）
wget 包下载
```bash
wget https://mirrors.tuna.tsinghua.edu.cn/anaconda/miniconda/Miniconda3-py38_4.8.3-Linux-x86_64.sh
```
软件安装(安装软件：安装过程中根据提示输入enter或yes)
```bash
bash Miniconda3-py38_4.8.3-Linux-x86_64.sh
```
验证安装：重启终端（必须），运行下方命令，显示版本号则安装成功
```bash
conda -V
```
更换国内源,在用户目录（/home/xxx）下新建.condarc文件并添加如下内容
```bash
touch .condarc
```
```
channels:
  - defaults
show_channel_urls: true
channel_alias: https://mirrors.tuna.tsinghua.edu.cn/anaconda
default_channels:
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/r
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/pro
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/msys2
custom_channels:
  conda-forge: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  msys2: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  bioconda: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  menpo: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  pytorch: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  simpleitk: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
```
执行以下命令清除索引缓存,并查看配置确认换置完成
```
conda clean -i

conda config --show
```