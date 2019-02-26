---
title: Windows10下安装Python,Tensorflow和Keras
date: {{ date }}
tags:
categories: 
permalink: 
---

2018年4月更新：
这篇文章原写于2017年10月。据称目前（2018年4月）Tensorflow在windows上已经支持3.6版本，我还没有自己尝试，相关讨论请参考https://stackoverflow.com/questions/40884668/installing-tensorflow-on-windows-python-3-6-x.
***
&emsp;&emsp;今后做实验要开始接触深度学习了，那当然免不了要安装Python和Tensorflow，另外因为需要LSTM方法，我也需要安装Keras。这篇文章就是关于最近安装这些东西的一个小结。

 **如果你懒得看后文，我其实就一句话，从头开始就用Anaconda吧！！！ （直接跳转到“最简安装过程”部分）**

## 目录
1 用Windows遇到的坑
2 我的坎坷经历
3 最简安装过程
4 附加知识

##用Windows遇到的坑

首先总结一下用windows过程中的坑：
1.  **Tensorflow目前在windows上只支持Python3.5版本（高了低了都不行）**
2.  **Scipy在windows上用命令行安装出错。因为安装Keras时会安装Scipy，所以无法成功安装Keras**

## 我的坎坷经历

&emsp;&emsp;不卖关子了，简而言之，在windows上最好是使用Scientific Python distributions来安装和管理各种库，这是我后来才发现的。由于始终没法成功安装Scipy，我找到了Scipy的这个[官网安装介绍](https://scipy.org/install.html)，windows系统的同学可以直接拖到最后看下。而Scientific Python distributions的介绍在页面的开头，我直接使用的第一个，也就是Anaconda.

&emsp;&emsp;使用Anaconda要注意，因为它的首页上是下载集成了3.6版本的Python的，而tensorflow在windows上只支持3.5版本，所以这个要想办法解决。根据Anaconda的介绍（[How do I get the latest Anaconda with Python 3.5?](https://docs.continuum.io/anaconda/faq#id6)）可以用以下三种方法：

**A)** We recommend downloading the latest version of Anaconda and [making a Python 3.5 environment](https://conda.io/docs/py2or3.html).

**B)** A second option is to download the latest version of Anaconda and then run this command to install Python 3.5 in the root environment: `conda install python=3.5`

**C)** A third option is to download the most recent Anaconda Installer that had Python 3.5 by default. This is Anaconda 4.2.0\. You can download it from our [archive](https://repo.continuum.io/archive/). Scroll down the page until you find version 4.2.0 for your platform.

&emsp;&emsp;我用的第二种方法，也就是在开始界面先找到Anaconda Prompt，然后在里边输入命令 `conda install python=3.5`

&emsp;&emsp;注意在这个过程中不要开着Anaconda的用户界面，否则会报错说Anaconda正在被使用，关闭Anaconda界面之后使用上述命令就好用。安完之后再Anaconda Prompt的界面输入python后发现版本变成3.5.3了。

&emsp;&emsp;tensorflow的安装可以参见莫烦写的教程和视频([LINK](https://morvanzhou.github.io/tutorials/machine-learning/tensorflow/1-2-install/))。重点注意选择好是CPU版本还是GPU版本，另外再就是Python3和Python2用的命令的微小差别。我在进行完之前的Python版本降到3.5.3之后，在Anaconda Prompt里使用命令 `pip3 install tensorflow` 成功安装了tensorflow（太让人激动了！！！）

&emsp;&emsp;遇到的问题是为了检测tensorflow是否安装成功，我实验了import tensorflow，可是在Python 3.5.3自己的shell里是可以用，可是在Anaconda Prompt里的python下不能用，不知道为什么。可能因为我在使用上边说的第二种方法转换Python之前，自己手动安装了一次Python3.5.3的缘故，悲催，做了无用功还影响了之后的功能。用了最笨的办法，卸载了python3.5.3，结果Anaconda Prompt打不开了，最后干脆把所有Python和Anaconda都卸载了。

## 最简安装过程

&emsp;&emsp;有了前边的经验铺路，现在大致知道怎么做比较方便了。这段开始我基本就是从头做起了。首先按照前边说的第三种方法，到Anaconda官网的Achiv里下载了Anaconda3-4.2.0版本。安装完之后发现pip3命令没法使用，不过检查了Anaconda里pip包已经安装了的，所以试了下用pip命令，可以。于是使用如下命令进行安装：

    pip install tensorflow
    pip install keras

&emsp;&emsp;两个都成功安装了，接下来用一下两个命令测验一下是否真的安装成功，当然首先要在命令行用python命令进入python控制界面，然后

    import tensorflow
    import keras
&emsp;&emsp;两个都没有报错，keras默认使用TensorFlow作为backend。总算大功告成，可以去吃午饭了，哈哈。![](https://upload-images.jianshu.io/upload_images/4815334-9bdded1ebd96991d.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


* * *

## 附加知识

[WINDOWS 下 PYTHON 双版本共存解决方案](http://xiaoyc.com/multi-version-solution-of-python-on-windows/)
当电脑里有多个python版本时，通常的做法是要修改环境变量，不过这篇文章中的方法只需要在不想用的版本的根文件夹中加入一个bat文件即可，巧妙的解决了问题，推荐大家看看。如果大家想知道怎么通过修改环境变量来更改默认的python版本，可以看[这里](http://blog.csdn.net/qq_25579889/article/details/52895683)

安装Keras可以部分参考这篇文章：
[windows 10 64bit下安装Tensorflow+Keras+VS2015+CUDA8.0 GPU加速](http://www.jianshu.com/p/c245d46d43f0)

***
本篇文章原发表于我的个人博客: [qingnansun.com](http://qingnansun.com/pythonkerasunderwindows)
