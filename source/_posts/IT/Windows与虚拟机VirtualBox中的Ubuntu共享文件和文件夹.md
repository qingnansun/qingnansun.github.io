---
title: Windows与虚拟机VirtualBox中的Ubuntu共享文件和文件夹
date: 2018-06-03
tags: [windows,虚拟机,ubuntu]
categories: 
permalink:
---

最近因为实验需要，重新启用了好久不用的Virtual Machine，做好基本的设置之后觉得有必要实现windows系统与VirtualBox中的Ubuntu系统的文件共享。尝试了网上说的很多方法都一直报错，最后终于在合并了几个方法的不同步骤之后实现了，现在总结和分享一下。

*   1 Windows端
*   2 Linux端
    *   2.1 设置VirtualBox中虚拟系统的共享信息
    *   2.2 在Terminal中下载所需镜像并安装
    *   2.3 挂载共享文件夹
    *   2.4 其他代码
    *   2.5 其他信息
## Windows端

Windows端需要建立一个用来进行文件分享的文件夹，比如我在D盘建了一个ShareWithVM文件夹。在这个文件夹的图标上用鼠标右键单击，然后选择**属性–>分享**，然后选择“**高级分享（Advanced Sharing）**”并勾选“**分享这个文件夹**”，然后单击“**确定”**即可。

![](https://upload-images.jianshu.io/upload_images/4815334-393d331956bf5abd.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## Linux端

设置的重点在linux端，也就是虚拟机上的Ubuntu上，网上有很多教程，可是我使用后并不成功，以下是我的设置过程。

### 设置VirtualBox中虚拟系统的共享信息

在VirtualBox Manager界面中选择需要设置的Ubuntu虚拟系统，然后按下图的顺序添加刚才在Windows端建立的共享文件夹的信息。这一步可能需要先关闭虚拟机再设置，我不太记得我设置的时候虚拟机是关闭还是运行状态了。

![](https://upload-images.jianshu.io/upload_images/4815334-91eeab532782e155.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 在Terminal中下载所需镜像并安装

这一步可以用参考链接[1]中的方式在windows系统下载然后再虚拟机选择相应镜像，不过我是通过以下的代码实现的。

首先运行Ubuntu并打开一个terminal，然后输入以下代码：

```
sudo apt-get install virtualbox-guest-additions-iso

```

接下来在图形界面里的以下位置找到这个映像，并用鼠标右键单击，选择Open With Disk Image Mounter，它就会自动安装了，直到安装成功后按enter键退出。

```
/usr/share/virtualbox/VBoxGuestAdditions.iso
```

![](https://upload-images.jianshu.io/upload_images/4815334-cd03409725533b5a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


### 挂载共享文件夹

在Ubuntu的Terminal里输入如下命令：

```
sudo mkdir /mnt/shared
```

```
sudo mount -t 
```

shareFolder是windows中要共享的文件夹的名字，由于我第一步在windows创建的分享文件夹角ShareWithVM，所以我在我这输入的代码实际为：

```
sudo mount -t vboxsf ShareWithVM /mnt/shared
```

如果一切顺利的话，现在就可以互传文件了。补充一下，你的共享文件夹在windows端的位置在本文开头已经说了，在ubuntu的位置是在/mnt文件夹下的shared里，如果你想查看这个共享文件夹里的内容，可以用如下代码定位到共享文件夹：

```
cd /mnt/shared
```

### 其他代码

以下部分均转自参考资料[1]，我并没有实际操作，因为自动挂载已经在前边说的Linux端的第一步勾选了，我觉得不必再设置了。

> 要想自动挂载的话，可以在/etc/fstab中添加一项
> ```
> share /mnt/shared vboxsf rw,gid=100,uid=1000,auto 0 0
> ```
> 
> 5、卸载的话使用下面的命令：
> ```
> sudo umount -f /mnt/shared
> ```
> 
> 注意：
> 共享文件夹的名称千万不要和挂载点的名称相同。比如，上面的挂载点是/mnt/shared，如果共享文件夹的>名字也是shared的话，在挂载的时候就会出现如下的错误信息：
>```
>/sbin/mount.vboxsf: mounting failed with the error: Protocol error
>```

### 其他信息

除了上边写的我最终成功使用的方法，网上还比较流行的是用代码安装open-vm-tools并配合使用一个从gitlab下载的补丁进行安装。看网上的评论应该是很多人都用这个方法成功了，可是我就是不行，始终提示`mounting failed with the error: No such device.`如果大家感兴趣的话，可以尝试这种方法。

此外需要说明的是我在成功安装之前，实验了很多方法，虽然都没有成功，但是其中用到的一些代码可能为最后的成功安装做了铺垫，所以如果你按照我前边说的步骤不能成功安装的话，可以尝试一下链接[3]中的各种代码，以及如下两句。

```
sudo apt-get update
sudo apt-get install virtualbox-guest-dkms 
```
今天为了弄这个文件共享花了很多时间，因为找不到对应的方法，而网上说的解决方案在我这又不太管事。希望这篇文章可以帮到和我遇到相似问题的朋友们。

**参考链接**

[1] [http://www.cnblogs.com/linjiqin/p/3615477.html](http://www.cnblogs.com/linjiqin/p/3615477.html)
[2] [https://askubuntu.com/questions/792832/how-to-install-virtualbox-guest-additions-for-ubuntu-16-04](https://askubuntu.com/questions/792832/how-to-install-virtualbox-guest-additions-for-ubuntu-16-04)
[3] [https://blog.csdn.net/fukaibo121/article/details/73129584](https://blog.csdn.net/fukaibo121/article/details/73129584)
