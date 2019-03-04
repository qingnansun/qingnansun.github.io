---
title: Ubuntu上安装python3-6以及设置为系统默认
date: 2018-07-05
tags:
categories: 
permalink: 
---

这篇文章记录了如何在Ubuntu上安装python3.6以及将其设置为系统默认。


# 查看Ubuntu版本

由于python3.6在不同的Ubuntu版本中的安装是不一样的，这里我们先来看一下的Ubuntu的版本，在terminal中输入`lsb_release -a`即可查看，例如我的Ubuntu版本为16.04.4.

{% asset_img 1_version.png %}

# 不同Ubuntu版本上的python3.6的安装

文末的参考资料[1]中的高赞回答列举了python3.6在不同版本的Ubuntu上的安装，这里摘抄如下:

## Ubuntu 14.04 and 16.04

```
sudo add-apt-repository ppa:deadsnakes/ppa
sudo apt-get update
sudo apt-get install python3.6
```

或者

```
sudo add-apt-repository ppa:jonathonf/python-3.6
sudo apt-get update
sudo apt-get install python3.6
```

安装完成后使用`python3.6`命令运行

## Ubuntu 16.10 and 17.04

```
sudo apt-get update
sudo apt-get install python3.6
```

安装完成后使用`python3.6`命令运行

## Ubuntu 17.10

在Ubuntu17.10中已经默认使用python3.6，所以可以直接用`python3`运行

# 设置python3.6为系统默认

安装好python3.6之后，我的系统中有python2.7，python3.5和python3.6三个版本的python。为了避免每次使用`python3.6`命令，希望把python3.6设置为系统默认。在设置之前，我们首先来看一个系统中python命令，python3命令以及不同版本python的路径，之后的操作中我们也需要其中的部分路径：

{% asset_img 2_python.png %}

## 设置`python`命令默认使用python3.6

```
sudo rm python的路径
sudo ln -s python3.6路径 python的路径
```

## 设置`python3`命令默认使用python3.6

```
sudo rm python3的路径
sudo ln -s python3.6路径 python3的路径
```
