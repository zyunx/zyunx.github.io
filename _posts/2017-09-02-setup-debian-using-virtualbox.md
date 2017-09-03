---
layout: post
title: "图解使用VirtualBox创建Debian系统"
date: 2017-09-02
author: "张云霄"
---

## 结果

* 安装VirutalBox 5.1.26虚拟机管理器
* 在VirutalBox中创建一台虚拟机
* 在创建的虚拟机里安装Debian 9.1操作系统（Guest OS）

## 演示环境

* 笔记本 MacBook Air 2015以后
* 操作系统 OS X 10.10.5 （Host OS）

## 下载，安装VirtualBox

[VirutalBox官网](https://www.virtualbox.org/)

VirtualBox的下载和OS X系统中安装软件就不用介绍了。

安装成功后，启动VirutalBox。VirutalBox虚拟机管理器主界面如图。

![virtualbox main window](/image/virtualbox/vb-main.png "VirtualBox主界面")

d9是我以前创建的一台虚拟机，刚安装的VirtualBox的虚拟机列表是没有这一项的。

## 下载Debian网络版安装镜像文件

[Debian官网](https://www.debian.org/)

进入官网，点击右上方的 "Download Debian 9.1"，下载Debian系统网络版安装镜像文件。

![debian index](/image/debian/d9-index.png "Debian首页")

网络版安装镜像文件的优点是文件小，下载时间短。

镜像文件中只包含Debian系统的一些核心包，在Debian系统安装过程中可以选择额外需要安装的包。

## 创建虚拟机

回到VirutalBox虚拟机管理器主界面， 点击工具栏第一个按钮 "New"。

![virtualbox new window](/image/virtualbox/vb-new.png "VirtualBox新建界面")

填写要创建的虚拟机的一些基本信息。

* 名字：demo-linux
* 类型：linux
* 版本：Debian (64 bit)
* 内存：256M （由于我的Linux系统，不安装桌面系统，256M已足够。）
* 硬盘：Create a virtual hard disk now (选择创建一个新虚拟硬盘)

点击 "Create" 按钮。

![virtualbox new2 window](/image/virtualbox/vb-new2.png "VirtualBox新建界面2")

配置虚拟硬盘，包括虚拟硬盘文件路径，虚拟硬盘大小，虚拟硬盘文件文件类型和虚拟硬盘存储空间分配方式。

使用默认值，点击 "Create" 按钮。

这样虚拟机就创建好了。

回到VirutalBox虚拟机管理器主界面，发现左边虚拟机列表多出一条我们刚刚创建
的虚拟机。

![virtualbox guests](/image/virtualbox/vb-guests.png "VirtualBox客户机列表")

## 在虚拟机里安装Debian系统

从这里开始，我们将开始安装Debian系统了。

### 插入Debian安装镜像文件到虚拟机的光驱

紧接着上一步，在VirutalBox虚拟机管理器主界面的左边虚拟机列表中，选择新建的虚拟机demo－linux。

在右边的的配置详情的"Storage"面板的Controller：IDE －> IDE Secondary Master  项下，点击"[Optical Disk] Empty"，并在弹出的菜单中，选择"Choose disk image..."。

在弹出的文件选择框，选择下载好的Debian安装镜像文件debian-9.1.0-amd64-netinst.iso。

结果如图。

![virtualbox insert debian iso](/image/virtualbox/vb-iso.png "为虚拟机配置光驱镜像文件")

点击工具栏的"Start"按钮，启动虚拟机。

虚拟机启动后，会读取光驱里的镜像文件debian-9.1.0-amd64-netinst.iso，
发现这是一个可启动的光盘，于是将控制交给光盘中的引导程序，引导程序再将控制
交给光盘里的Debian系统安装程序。

Debian系统安装程序如图。

![debian install step 1](/image/debian/debian-ins1.png "Debian安装程序第一步")

使用方向键选择第二项"Install"。

Enter键下一步。

### 配置系统语言、时区

![debian install step 2](/image/debian/debian-ins2.png "Debian安装程序第二步")

选择安装程序的语言，该语言会默认为安装完成后Debian系统的语言。

这里选"English", 因为Debian系统终端不支持中文。

Enter键下一步。

![debian install step 3](/image/debian/debian-ins3.png "Debian安装程序第三步")

选择时区。

我现在在深圳，我们这里选"Hong Kong"。

Enter键下一步。

![debian install step 4](/image/debian/debian-ins4.png "Debian安装程序第四步")

选择键盘类型。

默认选择"American English"。

Enter键下一步。

### 配置基本网络

接下来，安装程序会加载一些必要程序，扫描虚拟机的网卡，如果可以，会自动配置网卡IP。

过一会儿，安装程序显示如下界面。

![debian install step 5](/image/debian/debian-ins5.png "Debian安装程序第五步")

配置主机名。

输入demo-linux。

Enter键下一步。

![debian install step 6](/image/debian/debian-ins6.png "Debian安装程序第六步")

配置域名。

默认为空。

Enter键下一步。

### 配置用户

接下来，就开始配置用户了。

![debian install step 7](/image/debian/debian-ins7.png "Debian安装程序第七步")

设置root用户密码

输入"123456"。

Enter键下一步。

![debian install step 8](/image/debian/debian-ins8.png "Debian安装程序第八步")

确认root用户密码

重复输入密码"123456"。

Enter键下一步。

接下来，我们会创建一个新的普通用户，这里我会新建一个用户名为demo的用户。

![debian install step 9](/image/debian/debian-ins9.png "Debian安装程序第九步")

输入用户全称"demo"。

Enter键下一步。

![debian install step 10](/image/debian/debian-ins10.png "Debian安装程序第十步")

输入用户名"demo"。

用户全称和用户名的区别是昵称与账号的区别。

Enter键下一步。

![debian install step 11](/image/debian/debian-ins11.png "Debian安装程序第十一步")

输入demo用户密码"654321"。

Enter键下一步。

![debian install step 12](/image/debian/debian-ins12.png "Debian安装程序第十二步")

确认demo用户密码"654321".

Enter键下一步。

### 配置硬盘（分区）

接下来将配置硬盘（分区），为了演示简单，我选择使用整个硬盘。

![debian install step 13](/image/debian/debian-ins13.png "Debian安装程序第13步")

选择分区方法。

为了演示简单，选择"Guided - use entire disk"，使用分区向导，并使用整个硬盘。

Enter键下一步。

![debian install step 14](/image/debian/debian-ins14.png "Debian安装程序第14步")

选择要使用的硬盘。

我们的虚拟机只有一个硬盘。

Enter键下一步。

![debian install step 15](/image/debian/debian-ins15.png "Debian安装程序第15步")

选择分区方案。

为了演示简单，选择"All files in one partition (recommended for new users)",
所有文件都放在一个分区（根分区）下。

Enter键下一步。

![debian install step 16](/image/debian/debian-ins16.png "Debian安装程序第16步")

检查安装程序生成的分区方案。

安装程序将唯一的硬盘分成两个主分区。
一个主分区挂载到"/"目录。
另一个主分区作为扩展分区。
在扩展分区中穿件了一个逻辑分区，作为swap分区。

检查分区方案信息后，
选择"Finish partitioning and write changes to disk",
完成分区，并将改变写入硬盘。

Enter键下一步。

![debian install step 17](/image/debian/debian-ins17.png "Debian安装程序第17步")

最后一次确认分区操作。

选择Yes。

Enter键下一步。

### 配置包管理器

接下来配置包管理器，我们会使用Debian包仓库的中国镜像仓库。

![debian install step 18](/image/debian/debian-ins18.png "Debian安装程序第18步")

是否扫描其他CD或DVD。

因为我们只下载debian-9.1.0-amd64-netinst.iso，所以选择No。

Enter键下一步。

![debian install step 19](/image/debian/debian-ins19.png "Debian安装程序第19步")

选择Debian包仓库的镜像所在国家。

选择"China"，中国。

Enter键下一步。

![debian install step 20](/image/debian/debian-ins20.png "Debian安装程序第20步")

选择中国某个Debian包仓库镜像的主机名。

建议选择"ftp.cn.debian.org"。

Enter键下一步。

![debian install step 21](/image/debian/debian-ins21.png "Debian安装程序第21步")

配置HTTP代理。

我未使用HTTP代理，留空。

Enter键下一步。

![debian install step 22](/image/debian/debian-ins22.png "Debian安装程序第22步")

安装程序正在配置Debian的包管理器apt...

![debian install step 23](/image/debian/debian-ins23.png "Debian安装程序第23步")

是否要参加"包使用调查"？

如果你选择参加，Debian系统会每周向Debian开发者发送一次操作系统中使用最频繁的软件包。

为了Debian变的更好，我选择Yes。

Enter键下一步。

![debian install step 24](/image/debian/debian-ins24.png "Debian安装程序第24步")

选择需要安装的额外的包。

由于我们下载的Debian安装镜像debian-9.1.0-amd64-netinst.iso是一个网路安装镜像，
里面只包含了核心的包。

这里，我只选择了"SSH server"和"standard system utilities".

Enter键下一步。

安装程序会自动下载需要的包，并安装。

### 配置GRUB

GRUB是Debian系统的引导程序（boot loader），计算机启动后会将控制交给引导程序。
引导程序再决定将控制交给哪一个操作系统。

![debian install step 25](/image/debian/debian-ins25.png "Debian安装程序第25步")

是否将GRUB安装在主引导纪录？

选择Yes。

Enter键下一步。

![debian install step 26](/image/debian/debian-ins26.png "Debian安装程序第26步")

选择将GRUB安装到哪个硬盘的主引导纪录。

我们的虚拟机只有一块硬盘。

选择"/dev/sda ..."。

Enter键下一步。

![debian install step 27](/image/debian/debian-ins27.png "Debian安装程序第27步")

恭喜你， Debian系统安装成功。

Enter键，重启计算机。

### 安装完成

到这里，Debian系统已经安装完整了。

虚拟机启动后，会将控制交给GRUB引导程序。

![debian GRUB](/image/debian/debian-grub.png "Debian引导程序界面")

在GRUB中选择要使用的操作系统。

目前我们的虚拟机只有一个操作系统Debian。

选择"Debian GNU/Linux"。

按下Enter键。

![debian GRUB](/image/debian/debian-login.png "Debian引导程序界面")

这是Debian系统的登陆界面。

输入用户名"demo",密码"654321"。

按下Enter键，一个未知的世界正在等待你的探索。
