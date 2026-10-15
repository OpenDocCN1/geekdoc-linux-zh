
这完成了配置 HTTP 安装服务器。

## 使用网络安装服务器安装 RHEL

有几种方法可以使用前节介绍的网络安装服务器在客户端系统上安装 RHEL。在本节中，你将通过 USB 或 CD/DVD 进行本地启动，然后从安装服务器安装 RHEL。

## 客户端启动方法

有四种启动客户端并指向网络源安装 RHEL 方法。这些方法是：

1. 使用安装 CD 或 DVD 本地启动
2. 使用可启动 CD 本地启动
3. 使用可启动 USB 本地启动
4. 使用 PXE（预启动执行环境）远程启动

你可以使用任何一种方法开始安装。#2 和 #3 将在本章后面介绍。#4 是网络启动。

### 准备可启动 CD

准备可启动 CD，将 `/rhel52/install_media` 的内容复制到空白 CD 中。

### 准备可启动 USB 驱动器

准备可启动 USB 驱动器，将 `/rhel52/install_media` 的内容复制到 USB 驱动器中。

## 使用网络安装服务器安装 RHEL

使用网络安装服务器安装 RHEL，请遵循以下步骤：

1. 插入安装 CD 或 USB 驱动器或启动 CD/DVD。将出现如图 28-1 所示的启动菜单。选择 Removable Devices（可移动设备）以启动 USB 驱动器。
2. 如果使用了 CD，将出现 boot 提示符。在提示符输入“`linuxask`”并按回车。如果你使用了 USB 驱动器，跳转到第 6 步。

![](img/3f35ec29a294974bc1a4fdae3ae46652_608_0.png)

图 28-6 配置 TCP/IP

如图 28-7 所示，输入分配给此系统的 IP 地址、子掩码和网关地址。点击 OK 继续。

![](img/3f35ec29a294974bc1a4fdae3ae46652_608_1.png)

图 28-7 手动配置 TCP/IP

为 NFS、FTP 或 HTTP 服务器提供 IP 地址，以及安装文件或 ISO 镜像所在的路径。图 28-8、28-9 和 28-10 显示了 NFS、FTP 和 HTTP 设置屏幕。

![](img/3f35ec29a294974bc1a4fdae3ae46652_608_2.png)

图 28-8 NFS 设置

### FTP 设置

![](img/3f35ec29a294974bc1a4fdae3ae46652_609_0.png)

图 28-9 FTP 设置

![](img/3f35ec29a294974bc1a4fdae3ae46652_609_1.png)

图 28-10 HTTP 设置

10. 如果上一步提供的信息正确，RHEL 的安装将开始，你将看到连续出现图形化安装屏幕，显示与你在第 09 章“安装”中本地 CD 安装方法相同的进度。

## 通过 Kickstart 安装 RHEL

Kickstart 允许你进行无干预、完全自定义且更快的 RHEL 安装。你需要创建一个单独配置文件并将其名称提供给安装程序，该程序将使用文件中定义的配置信息在系统上安装并配置 RHEL。这消除了你原本需要经历的问答环节。以下是使用这种安装方法的主要优势：

- 全自动、无人值安装。
- 无需回答配置问题。
- 在多个系统上同时进行安装。
- 在多个系统上实现相同的配置。
- 快速部署任意数量的服务器。

为了成功执行 kickstart 安装，需要完成四个主要步骤。这些步骤是：

1. 使安装文件/镜像可用。
2. 创建 kickstart 配置文件。
3. 将 kickstart 配置文件拷贝到 USB、CD 或网络驱动器。
4. 开始安装过程。

以下小节解释了每个步骤。

## 使安装文件 / 镜像可用

此步骤是将安装文件或 ISO 镜像拷贝到目录，并通过 NFS、FTP 或 HTTP 协议通过网络提供该目录。详细信息请参见本章前面的“配置网络安装服务器”章节。

## 创建 Kickstart 配置文件

在开始自动 kickstart 安装之前，你需要创建一个文件并在其中捕获所有所需的配置。这些信息将由 kickstart 用于相应地安装和配置系统。你可以通过自定义 `/root/anaconda-ks.cfg` 文件或运行 Red Hat Kickstart 配置器 `system-config-kickstart`（或 `ksconfig`）来创建此文件。下面解释了两种方法。

### 使用 /root/anaconda-ks.cfg 文件

在第 09 章“安装”以及本章之前的 RHEL 安装期间，你输入了若干配置信息。安装程序将这些信息存储在 `/root/anaconda-ks.cfg` 文件中。你可以根据需求自定义此文件，并将其用于其他客户端部署。

以下显示了 `anaconda-ks.cfg` 文件的内容，该文件是从第 09 章“安装”中执行的安装生成的。将此文件拷贝为 `/root/ks.cfg` 并对其进行修改，以便安装到 IP 为 192.168.0.210 的新系统 rhel10 上。

```bash
# cp /root/anaconda-ks.cfg /root/ks.cfg

# nl /root/ks.cfg

1 由 anaconda 自动生成的 Kickstart 文件。

2 install

3 cdrom

4 key --skip

5 lang en_US.UTF-8

6 keyboard us

7 xconfig --defaultdesktop=GNOME --startxbonboot

8 network --device eth0 --protocol static --ip 192.168.0.210 --netmask 255.255.255.0 --gateway 192.168.0.1 --nameserver 192.060.1 --hostname noipv6

9 root --encrypted $1$Mh0dr$McLlyW1/JlzUg8zzI44mP1

10 firewall --enabled --port=22:tcp

11 authconfig --enableshadow --enablebmd5

12 selinux --enforcing

13 timezone --use America/New_York

14 reboot

15 reboot --disable

16 zerober

17 bootloader --location=mbr --driveorder=sda,sdb --append="rhgb quiet"

18 # 以下是你请求的分区信息

19 # 注意，任何删除的分区都未在此处表示

20 # 因此除非你清除了所有分区，否则

21 # 不保证有效

22 #clearpart --size=1000 --ondisk=sda --asprimary

23 #part/boot --fsype ext3 --size=4

24 #part.4 --size=0 --grow --ondisk=sda

25 #physical vg0=32768

26 #logvol --fsype ext3 --name=l1 --vname=vg0 --size=1984

27 #logvol/home --fsype ext3 --name=l2 --vname=vg0 --size=992

28 #logvol/tmp --fsype ext3 --name=l3 --vname=vg0 --size=1984

29 #logvol/usr --fsype ext3 --name=l4 --vname=vg0 --size=4992

30 #logvol/var --fsype ext3 --name=l5 --vname=vg0 --size=4992

31 #logvol/opt --fsype ext3 --name=l6 --vname=vg0 --size=8000

32 #logvol swap --fsype swap --name=l7 --vname=vg0

33 @packages

34 @editors

35 @base

36 @network

37 @server

38 @ftp

39 @http

40 @root

41 @encrypted

42 @server

43 @dev

44 @video

45 @system

46 @graphics

47 @xorg

48 @mail

49 @printing

50 @kde

51 @disabled

52 @soft

53 @config

54 @sound

55 @audio

56 @tools

57 @common

58 @bash

59 @python

60 @post

61 @chkconfig

62 @off
```

第 #22 行：告诉 Anaconda 清除 sda 驱动上之前 RHEL 安装留下的分区信息。或者，如果你希望删除 sda 上所有来自之前的 RHEL 安装或 Windows 的分区信息，请使用以下命令：
