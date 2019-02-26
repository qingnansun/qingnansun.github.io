---
title: {{ title }}
date: {{ date }}
tags:
categories: 
permalink: :year/:month/:day/:title/
---

&emsp;&emsp;由于Theano从十月起停止更新（[LINK](https://www.jiqizhixin.com/articles/2017-09-29-5)），我开始着手把我使用Keras时的backend从Theano转到Tensorflow。以下是今天在同事LY的指导下进行backend转换的一点总结（同时对她表示感谢）。

**安装环境**：Linux服务器上的虚拟环境中（详见：[在linux系统上设置虚拟环境Virtual Environment](http://qingnansun.com/virtual-environment-on-linux/)）

&emsp;&emsp;首先我根据Keras官网的介绍对keras.json文件进行设置（[LINK](https://keras.io/backend/)）。在命令框中输入：

```
vi .keras/keras.json
```

&emsp;&emsp;然后按着如下代码编辑，主要是把backend改为tensorflow。（其实Keras默认的backend就是tensorflow，只是因为我之前改成了theano，所以现在要改回来。）

```
{ "image_data_format": "channels_last", 
```

&emsp;&emsp;另外如果你还没有安装GPU版本的tensorflow，则需要首先进行安装。由于我们实验室的server上不兼容1.3版本的tensorflow，我这里对安装的版本进行了控制

```
pip install tensorflow-gpu==1.2
```

&emsp;&emsp;成功安装之后，就可以在你的.py文件的代码里加入如下语句进行tensorflow的backend的调用和设置了，设置好之后像平常一样运行文件即可。

```
import tensorflow as tf
import keras.backend.tensorflow_backend as KTF

os.environ["CUDA_VISIBLE_DEVICES"] = "3"  #设置需要使用的GPU的编号
config = tf.ConfigProto()
config.gpu_options.per_process_gpu_memory_fraction = 0.4 #设置使用GPU容量占GPU总容量的比例
sess = tf.Session(config=config)
KTF.set_session(sess)
```

&emsp;&emsp;为了观察程序是否确实在使用GPU，可以使用在[《Linux上的一点小技巧》](http://qingnansun.com/linuxtricks/)中提到的命令`gpustat`或者`watch -n1 --color gpustat`进行查看程序是否真的运行在GPU上。

**—————–后记———————**

# Tensorflow无法完全实现实验的重复性

&emsp;&emsp;今天早些时候介绍了怎么在给keras设置使用tensorflow作为后端。晚上的时候发现使用tensorflow有个问题是无法确保实验的可重复性，换句话说，同样的代码，每次运行出来的结果是不一样的，即使已经设置了随机数的seed。而使用theano的后端是可以确保实验的可重复性的，至少在我之前的实验里，可以得到一模一样的结果。

&emsp;&emsp;对于这个问题，我在网上查阅了一下，发现也有人在讨论，比如在[1]中对各种可能的原因进行了探讨，并根绝theano和tensorflow后端各自给了设置seed的代码。对于tensorflow，要进行两次seed的设置，他们的值可以不同。代码如下，需要放在你的code的最顶端，不过此方法我试了没有起到效果。

```
from numpy.random import seed
seed(1)
from tensorflow import set_random_seed
set_random_seed(2) 
```

&emsp;&emsp;此外也有其他的帖子和文章对tensorflow作为backend时不能实现实验的重复性进行了讨论，比如在[2]中的帖子以及在[3]中keras的官方文档中都有提到建议的解决方案，不过我试了依然没有效果。[4]是对tensorflow的set_random_seed函数的具体介绍。

&emsp;&emsp;最后，由于tensorflow没法确保实验的可重复性，而我也没有找到适合我的解决方案，于是只好又切换为theano作为backend。不过今天的尝试也不是完全没有意义的，因为借着今天在tf上积累的一点经验，我想到了给theano后端也设定运行时占用GPU的容量比例，实践后发现代码运行速度大大提高。theano和Tensorflow有些不同，它默认只占用很少的GPU而tensorflow默认占用所有可用的GPU。比如我的代码在theano作为backend的时候，默认只占200M左右，我给人为把GPU的占比提高到0.4（约为5000M）之后，运行速度大大提高。具体的方法可以参考这篇文章 [LINK](https://www.weibo.com/ttarticle/p/show?id=2313501000014129139677341055)

[1] [用深度学习每次得到的结果都不一样，怎么办？](https://www.leiphone.com/news/201706/zt4Dm491Ol58C8Mc.html)
[2] [No reproducible using tensorflow backend #2280](https://github.com/fchollet/keras/issues/2280)
[3] [How can I obtain reproducible results using Keras during development?](https://keras.io/getting-started/faq/#how-can-i-obtain-reproducible-results-using-keras-during-development)
[4] [Tensorflow函数——tf.set_random_seed(seed)](http://blog.csdn.net/eml_jw/article/details/72353470)
***
本篇文章原发表于我的个人博客: [qingnansun.com](http://qingnansun.com/tensorflow-backend-on-gpu/)
