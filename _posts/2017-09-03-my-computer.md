---
layout: post
title: "我使用Linux，OS X，Windows系统的一种方式"
date: 2017-09-03
author: "张云霄"
---

作为一名计算机热爱者，打造一台适合自己的计算机系统一直是我所追求的目标。

从最初在PC上使用Windows，  
到PC上使用Linux，  
到PC上安装Windows和Linux双系统，  
再到使用MacBook的OSX，  
到MacBook上安装OSX和Linux双系统，  
到MacBook上安装OSX和Windows双系统，  
到MacBook上使用Linux，  
最后到MacBook安装OSX和Windows双系统并在OSX上虚拟Linux系统。

在尝试了Linux，Window，OSX不同组合后，我对自己的需求更加清晰。

Linux系统我推荐使用Debian发行版。

## 我的主要需求

* 编程
* 游戏
* 普通需要（浏览网页，听听歌，看看电影，做做表格，写写文章）

下面的表格是我对各操作系统的体验对比。

下文中，OSX特指Mac上OSX，不包括PC上的OSX。

|平台|编程|游戏|普通需求|爽|不爽|
|------|------|------|------|------|------|
|Windows|3分|10分|5分|游戏|广告多|
|Linux|10分|1分|5分|系统编程|桌面系统不友好|
|OSX|6分|5分|10分|工业设计|系统编程和游戏差强人意|

## 我的方式

就目前，没有一个操作系统可以满足我所有的需求。

经过大量体验与取舍，我作了如下选择。

1. 硬件选择MacBook
	
	如果不论操作系统，一部Dell或联想笔记本和一部MacBook让你选择，
	我想大多数人会选择MacBook。  
	反正我会选MacBook。
	
2. 使用MacBook的原装系统OSX，这可以满足我的普通需求和前端编程需求。

	OSX本身是UNIX系的操作系统，我喜欢。  
	而且，它与Linux（也是UNIX系）的结合使用比Windows更简单优雅。
	
3. 使用开源虚拟机管理器Virtual Box虚拟一个Linux系统，满足自己的系统编程需求。

	我使用它，主要因为Linux在服务器编程和系统编程方面的简单优雅。  
	桌面系统对Linux来说，就是一鸡肋。
	有了OSX系统后，Linux的桌面系统成了负担。  
	没有桌面系统的Linux安装在物理计算机和虚拟机中的性能差异几乎让人感觉不到。

4. 使用MacBook自带的BootCamp安装Windows，满足自己偶尔的游戏需求。

	MacBook对自身支持OSX和Windows双系统。


## OSX与Linux的共存的方式

接下来，我会介绍一下OSX和Linux系统共存的一种方式。在OSX上使用开源的虚拟机管理器Virtual Box（简称VBOX）虚拟出一个Linux系统，使用SSH访问虚拟Linux系统。

**VBOX让OSX和Linux共存成为可能。**

**OpenSSH使OSX和Linux的共存简单优雅。**


环境
1. MacBook Air（2015以后）
2. OS X 10.10.5
3. Debian GNU/Linxu 9.1
4. Virtual Box 5.1.26
5. OSX系统自带OpenSSH


### 使用Virtual Box虚拟Debian GNU/Linux系统

请读我的另一篇博客。

[图解使用VirtualBox创建Debian系统](/2017/09/02/setup-debian-using-virtualbox.html)

### 使用SSH访问虚拟Linux系统

为什么要使用SSH访问虚拟Linux系统？直接在在虚拟机里操作不行吗？

答案是：不够简单优雅。

如果直接在虚拟机里操作，就不可避免在OSX（Host OS）与Linux（Gest OS）之间切换。
这是件麻烦事。

另外，使用SSH访问会附带很多有用的功能。比如，

1. 文件上传下载
2. 无密码登录
3. 复制粘贴功能

如果，你要使用SSH访问虚拟Linux系统；

那么，请接着往下看；

否者，请关闭网页。

查看虚拟Linux系统的IP地址，我的Linux系统的IP是10.0.2.15。

结果如图。

![demo-linux ip adrress](/image/debian/demo-linux-ip.png)

在OSX中，使用SSH登陆虚拟Linux系统。

命令行

> ssh demo@10.0.2.15

结果如图。

![ssh demo-linux](/image/debian/ssh-fail.png)

链接超时。

在VBOX默认的网络配置下，每一个虚拟机中的系统（Guest OS）通过NAT
访问主机系统（Host OS）的网络。
所以，OSX（Host OS）是无法访问虚拟Linux系统（Guest OS）的。

为使Host OS与Guest OS互联，需要更改VirtualBox的网络配置。

详情可参考VirtualBox User Manual的Virutal Network章节。

以下是我配置网络的步骤。

### 配置Host-only网络

打开VirtualBox虚拟机管理器的网络配置界面（OSX菜单栏的"VirtualBox"菜单 => "Preferences..."菜单项 => "Network"标签页），选择“Host-only Networks”，点击在窗体的右边缘的“＋”按钮，新建一个名为“vboxnet0”的网络。

结果如图。

![Virtual Box Network Manager](/image/virtualbox/vb-netm.png)

选择vboxnet0，点击右边缘的起子形的按钮，打开主机系统（Host OS）的网卡配置
界面。

填入下面的值（默认值）。

* IPv4 Address：192.158.56.1
* IPv4 Network Mask：255.255.255.0

结果如下图。

![Virtual Box Network Adapter](/image/virtualbox/vb-netm-adapter.png)

点击“DHCP Server”，切换到DHCP配置。

这里我关掉“Enable Server”开关，因为Linux作为服务器，需要一个固定的IP。

结果如下图。

![Virtual Box Network DHCP Server](/image/virtualbox/vb-netm-dhcp.png)

### 配置虚拟Linux系统网卡

关闭虚拟Linux系统，更改Linux虚拟机的网络配置。

为Linux虚拟机添加另一块网卡Adapter 2，让它附加到刚创建的vboxnet0网络。

结果如图。

![demo-linux adapter2](/image/debian/demo-linux-adapter2.png)

启动虚拟Linxu系统，发现系统多出了一张网卡enp0s8。

结果如图。

![demo-linux ip address](/image/debian/demo-linux-ip2.png)

修改Debian系统的网卡配置文件/etc/network/interfaces，
添加网卡enp0s8的相关配置。

配置如下。

1. 系统启动，立即配置enp0s8
2. 为网卡分配静态IP地址
3. IP地址为192.168.56.100
4. 子网掩码为255.255.255.0

**记住一定不要配置网卡的网关。  
否则，enp0s8的网关配置会覆盖NAT网络网卡enp0s3的网关配置，
导致虚拟Linux系统无法访问Internet。**

/etc/network/interfaces内容如下。

![linux interfaces](/image/debian/demo-linux-iface.png)

重启demo-linux，查看网卡enp0s8的配置，一切顺利。

结果如图。

![linux ip address](/image/debian/demo-linux-ip3.png)

在OSX中，使用SSH访问虚拟Linux系统。

命令行

> ssh demo@192.168.56.100
	
连接成功，结果如图。

![ssh success](/image/debian/ssh-succ.png)

### 为虚拟Linux系统分配一个名字

修改OSX的hosts文件“/etc/hosts”, 添加一行

> 192.168.56.100    demo-linux

修改后的/etc/hosts内容如图。

![osx hosts](/image/debian/osx-hosts.png)

使用主机名登陆

> ssh demo@demo-linux

结果如图。

![ssh hostname success](/image/debian/ssh-hostname.png)

### SSH无密码登录

SSH支持私钥登陆。

配置步骤

1. 使用ssh-genkey生成公私钥对。
2. 使用scp将公钥“~/.ssh/id_rsa.pub”拷贝到虚拟Linux系统。
3. 登陆虚拟Linux系统。
4. 将公钥“id_rsa.pub”写入“~/.ssh/authorized_keys”文件
5. 登出虚拟Linux系统。

如图。

![ssh with no password config](/image/debian/ssh-nopwd.png)

再次登陆虚拟Linux系统，已经不需要输入密码。

如图。

![ssh with no password](/image/debian/ssh-nopwd2.png)

这就是我使用OSX和Linux的方式。
