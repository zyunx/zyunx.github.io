---
layout: post
title: "打造一台适合自己的计算机"
date: 2017-08-02
author: "张云霄"
---

作为一名计算机热爱者，打造一台适合自己的计算机一直是我的目标。

从最初在PC上使用Windows，到PC上使用Linux，到PC上装Windows和Linux双系统，
再到使用MacBook的OSX，到MacBook上装OSX和Linux双系统，
到MacBook上装OSX和Windows双系统，到MacBook上只安装Linux，
最后还原到MacBook的OSX上。

过程中，对自己的需求更加的清晰。

## 我的主要需求
1. 编程
2. 游戏
3. 普通需要（浏览网页，听听歌，看看电影，做做表格，写写文章）

## 各个平台的对比

|平台|编程|游戏|普通需求|爽|不爽|
|------|------|------|------|------|------|
|Windows|3分|10分|5分|游戏|广告多|
|Linux|10分|1分|5分|编程|桌面系统不友好|
|OSX|6分|5分|10分|颜值高|后端开发和游戏差强人意|

要同时满足我的三大需求，目前还没有一个解决方案。

最后，我作了如下

1. 放弃游戏的需求（玩玩手机游戏）
2. 使用MacBook
3. Linux不使用桌面系统
4. 不安装双系统

1. 使用MacBook的OSX满足普通需要和前端开发
2. 使用Linux满足服务器和底层编程需求


使用MacBook的OSX，并安装开源的虚拟机管理器VirtualBox，
将Linux安装在虚拟机里，Linux不用安装桌面系统
使用ssh访问虚拟机里Linux

环境
1. MacBook Air（2015以后）
2. VirtualBox 5.1.26
3.

## 下载，安装VirtualBox

[VirutalBox官网](https://www.virtualbox.org/)

VirtualBox的下载和OSX平台上安装软件就不用介绍了。

安装成功后，启动VirutalBox。VirutalBox虚拟机管理器主界面如下图

![virtualbox main window](/image/virtualbox/vb-main.png "VirtualBox主界面")

d9是我以前建的一个虚拟机，刚安装的VirtualBox是没有的。

## 下载Debian

[Debian官网](https://www.debian.org/)

进入官网，点击右上方的 "Download Debian 9.1"，下载Debian系统镜像文件

![debian index](/image/debian/d9-index.png "Debian首页")

## 新建虚拟机

回到VirutalBox虚拟机管理器主界面， 点击工具栏第一个按钮 "New"

![virtualbox new window](/image/virtualbox/vb-new.png "VirtualBox新建界面")

名字：demo－linux（可自定义）

类型：linux

版本：Debian (64 bit)

内存：256M，因为我的Linux系统，不安装桌面系统，256M足够了。

硬盘：选择创建一个新虚拟硬盘

点击 "Create" 按钮

![virtualbox new2 window](/image/virtualbox/vb-new2.png "VirtualBox新建界面2")

选择虚拟硬盘文件路径，虚拟硬盘大小，文件类型和虚拟硬盘存储空间分配模式。
什么都不用改，点击 "Create" 按钮。

这样虚拟机就创建好了。

回到VirutalBox虚拟机管理器主界面，发现左边虚拟机列表多出一个我们刚刚创建
的虚拟机条目。

![virtualbox guests](/image/virtualbox/vb-guests.png "VirtualBox客户机列表")

## 安装Debian系统

紧接着上一步，在VirutalBox虚拟机管理器主界面的左边虚拟机列表中，选择新建的虚拟机demo－linux。在右边的的配置详情的"Storage"面板的Controller：IDE －> IDE Secondary Master  项下，点击"[Optical Disk] Empty"，并在弹出的菜单中，选择"Choose disk image..."。在弹出的文件选择框，选择下载好的Debian安装镜像文件debian-9.1.0-amd64-netinst.iso，结果如下图。

![virtualbox insert debian iso](/image/virtualbox/vb-iso.png "为虚拟机配置光驱镜像文件")

点击工具栏的"Start"按钮，启动虚拟机。虚拟机就这样启动起来了，它会读取光驱，
发现这里有一个可启动的光盘debian-9.1.0-amd64-netinst.iso，于是执行Debian系统
安装程序。

![debian install step 1](/image/debian/debian-ins1.png "Debian安装程序第一步")

选择第二项"Install"，Enter键下一步。

![debian install step 2](/image/debian/debian-ins2.png "Debian安装程序第二步")

选择安装程序的语言，该语言会默认为安装完成后Debian系统的语言。这里选"English",
因为Debian系统终端不支持中文。Enter键下一步。

![debian install step 3](/image/debian/debian-ins3.png "Debian安装程序第三步")

选择时区，我现在在深圳，我们这里选"Hong Kong"。Enter键下一步。

![debian install step 4](/image/debian/debian-ins4.png "Debian安装程序第四步")

配置键盘，默认选择"American English"。Enter键下一步。

接下来，安装程序会加在一些必要程序，扫描虚拟机的硬件，并自动配置一些硬件。
过了一会儿，安装程序显示如下界面。

![debian install step 5](/image/debian/debian-ins5.png "Debian安装程序第五步")

配置主机名，输入demo-linux。Enter键下一步。

![debian install step 6](/image/debian/debian-ins6.png "Debian安装程序第六步")

配置域名，默认为空。Enter键下一步。

### 配置用户

接下来，就开始配置用户了。

![debian install step 7](/image/debian/debian-ins7.png "Debian安装程序第七步")

输入root用户的密码1234567。

![debian install step 8](/image/debian/debian-ins8.png "Debian安装程序第八步")

重复密码1234567。

![debian install step 9](/image/debian/debian-ins9.png "Debian安装程序第九步")

创建一个新的用户，这里我会新建一个用户名为demo的用户。

输入用户全称demo。

![debian install step 10](/image/debian/debian-ins10.png "Debian安装程序第十步")

输入用户名demo。

![debian install step 11](/image/debian/debian-ins11.png "Debian安装程序第十一步")

输入用户密码654321。

![debian install step 12](/image/debian/debian-ins12.png "Debian安装程序第十二步")

确认用户密码654321.

### 配置硬盘（分区）

接下来配置硬盘（分区），为了演示简单，我选择使用整个硬盘。

![debian install step 13](/image/debian/debian-ins13.png "Debian安装程序第13步")

选择"Guided - use entire disk"。Enter键下一步。

![debian install step 14](/image/debian/debian-ins14.png "Debian安装程序第14步")

选择要使用的硬盘，我们的虚拟机只有一个硬盘。Enter键下一步。

![debian install step 15](/image/debian/debian-ins15.png "Debian安装程序第15步")

选择"All files in one partition (recommended for new users)",
所有文件都放在一个分区下。 Enter键下一步。

![debian install step 16](/image/debian/debian-ins16.png "Debian安装程序第16步")

选择"Finish partitioning and write changes to disk",
完成分区，并将改变写入硬盘。Enter键下一步。

![debian install step 17](/image/debian/debian-ins17.png "Debian安装程序第17步")

选择Yes，最后一次确认分区操作。Enter键下一步。

### 配置包管理器

接下来配置包管理器，我们会使用debian包仓库的中国镜像仓库。

![debian install step 18](/image/debian/debian-ins18.png "Debian安装程序第18步")

是否扫描其他CD或DVD，因为我们只下载debian-9.1.0-amd64-netinst.iso，所以选择No。
Enter键下一步。

![debian install step 19](/image/debian/debian-ins19.png "Debian安装程序第19步")

选择Debian包仓库的镜像所在国家，China，中国。
Enter键下一步。

![debian install step 20](/image/debian/debian-ins20.png "Debian安装程序第20步")

选择中国某个Debian包仓库的镜像。建议选择ftp.cn.debian.org。
Enter键下一步。

![debian install step 21](/image/debian/debian-ins21.png "Debian安装程序第21步")

输入HTTP代理，留空。
Enter键下一步。

![debian install step 22](/image/debian/debian-ins22.png "Debian安装程序第22步")

安装程序正在配置Debian的包管理器apt...

![debian install step 23](/image/debian/debian-ins23.png "Debian安装程序第23步")

安装程序询问你是否要参加"包使用调查"。如果你选择参加，Debian系统会每周向Debian开发者
发送一次使用最频繁的软件包。为了Debian变的更好，我选择Yes。
Enter键下一步。

![debian install step 24](/image/debian/debian-ins24.png "Debian安装程序第24步")

选择额外需要安装的包。

由于我们下载的Debian安装镜像debian-9.1.0-amd64-netinst.iso是一个网路安装镜像，
里面只包含了核心的包。

这里，我只选择了"SSH server"和"standard system utilities".

Enter键下一步。

安装程序会自动下载需要的包，并安装。

### 配置GRUB

GRUB是Debian系统的引导程序（boot loader），计算机启动后会将控制交给引导程序。
引导程序再决定将控制交给哪一个操作系统。

![debian install step 25](/image/debian/debian-ins25.png "Debian安装程序第25步")

是否将GRUB安装在主引导纪录，选择Yes。

Enter键下一步。

![debian install step 26](/image/debian/debian-ins26.png "Debian安装程序第26步")

选择将GRUB安装到哪个硬盘的主引导纪录。

我们的虚拟机只有一块，选择"/dev/sda ..."。

Enter键下一步。

![debian install step 27](/image/debian/debian-ins27.png "Debian安装程序第27步")

恭喜你， Debian系统安装成功。

Enter键，重启计算机。

### 安装完成

到这里，Debian系统已经安装完整了。

虚拟机启动后，会将控制交给GRUB引导程序。

![debian GRUB](/image/debian/debian-grub.png "Debian引导程序界面")

在GRUB选择使用的操作系统。

目前我们的虚拟机只有一个操作系统Debian。

选择"Debian GNU/Linux", 按下Enter键。

![debian GRUB](/image/debian/debian-login.png "Debian引导程序界面")

这个是Debian系统的登陆界面。

输入用户名"demo",密码"654321"。

按下Enter键，一个未知的世界正在等待你的探索。
