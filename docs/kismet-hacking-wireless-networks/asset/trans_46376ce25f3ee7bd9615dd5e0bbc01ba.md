

现在，你已具备支持驱动漫游（wardrive）和执行无线渗透测试所需的所有内核支持。

## 安装合适的工具

一旦你生成了支持监听模式的内核并编译了相应的驱动程序，就可以开始安装执行驱动漫游所需的必要工具了。要完成此目标，你需要安装两个工具：Kismet 和 GPSD (www.pygps.org/gpsd/downloads)。

## 安装 Kismet

本节将简要介绍如何安装 Kismet。完整的安装说明请参见第 2 章。Kismet 的安装过程非常直接。只需从 www.kismetwireless.net/download.shtml 下载最新版的 Kismet，并将其保存到你选择的目录中。（旧版本的 Kismet 可以从 www.kismetwireless.net/code. 获取。）解压并解包该文件，然后进入它创建的目录，并执行以下命令：

```
# ./configure
# make
# make install
```

**注意**

这三个命令是从源码配置和编译 Linux 程序的标准方法。在本章剩余部分，除非另有说明，否则“编译程序”指的就是这三个步骤。

这将 Kismet 安装到默认目录（/usr/local/bin/kismet），并将 Kismet 配置文件安装到（/usr/local/etc/kismet）。

## 从源码编译或使用软件包

本章中的编译示例展示了如何首先从开发者的网站获取源码，然后手动编译程序来从源码编译安装程序。这只是编译和安装程序的一种方式。大多数发行版都拥有某种包管理系统，可用于安装程序，或获取并安装它们。Red Hat 和 Fedora 使用 Red Hat 包管理器（RPM）包管理系统，Gentoo 使用 emerge，而 Slackware 的软件包为 .tgz 格式。有时，使用发行版的包管理系统来安装程序会很有益；但需要注意的是，当使用包管理器来编译和安装程序时，它可能会将二进制文件和配置文件放置到非标准目录中。本章假设你已从源码编译，或者你的包管理器已将二进制文件和配置文件放置在标准位置。如果包管理器未这样做，你可以使用 find 命令搜索配置文件或二进制文件：

```
# find / -name kismet.conf -print
```

此命令在整个文件系统中搜索 kismet.conf 文件并在屏幕上显示结果。在 Linux 系统中，-print 开关很少是必需的；然而，添加它不会改变命令的功能。

## 安装 GPSD

GPSD 是一个与你的 GPS 单元进行交互的程序，它进而将数据传递给 Kismet，以提供发现接入点时你所在位置的 GPS 坐标。GPSD 的安装与普通的 Linux 安装过程略有不同，因为没有 "make install" 选项。执行 ./configure 和 make 命令，然后运行你编译所在位置的 gpsd，或者将 gps 和 gpsd 文件复制到路径中的目录，例如 /usr/bin 或 /usr/local/bin。

## 配置系统以进行驱动漫游

一旦你编译并安装了 Kismet 和 GPSD，就需要编辑 Kismet 配置文件，以便 Kismet 在你的系统上正常工作。除非你（或你的包管理器）更改了位置，否则配置文件会放在 /usr/local/etc。需要编辑两个文件：kismet.conf 和 kismet_ui.conf。

kismet_ui.conf 文件控制 Kismet 的用户界面选项。在大多数情况下，你可以将这些选项保留为默认值，除非你想调整界面外观。Kismet 确实有一个每次启动 Kismet 时都显示的欢迎窗口（见图 1.4）。

# 图 1.4 Kismet 欢迎窗口

![](img/d6ac176c353d2b7687c1186a140180a1_34_0.png)

要在 Kismet 启动时去除欢迎窗口，将 *showintro* 选项更改为 false：

```
# Do we show the intro window? 
showintro=false
```

*kismet.conf* 文件是设置 Kismet 重要选项的地方。为了使 Kismet 正常工作，必须编辑此文件以反映你的环境和硬件。首先，你需要编辑 *suider* 变量：

```
# User to setuid to (should be your normal user) 
suiduser=roamer
```

接下来你需要设置 *source* 变量。该选项告诉 Kismet 你正在使用什么类型的驱动和网卡，以及你的网卡配置在什么界面上。下面的例子告诉 Kismet 使用 Host 接入点驱动，并且你的网卡被配置为 *wlan0*。第三个选项 *wlan* 可以设置为任何值。

```
source=hostap,wlan0,wlan
```

以下是一些针对不同网卡和驱动的较常见的 source 选项：

```
# Source line for Intel Pro Wireless 2100 
source=ipx2100,eth0,ipx2100source 
# Source line for wlan-ng Prism2 driver 
source=prism2,wlan0,prism 
# Source line for Cisco (dependent on Cisco driver used) 
source=cisco,eth0,cisco 
# Alternate Source line for Cisco (dependent on Cisco driver used) 
source=cisco_cvs,eth1,wifi0,ciscoxfs 
# Source line for Hermes based cards (Orinoco) 
source=orinoco,eth0,orinocosource
```

除非你计划启用多个源，否则无需更改 *enable-sources* 变量，除非更改，否则该变量被注释掉。

默认情况下，Kismet 会跳频（hops channels）。这使得 Kismet 能够检测在 2.4GHz 频段不同信道上工作的接入点。除非你只想检测特定信道上的接入点，否则应保持此设置不变：

```
# Do we channelhop 
channelhop=true
```

如果你想识别特定信道上的接入点，请禁用跳频并在 source 变量中设置初始信道。例如，仅识别信道 8 上的接入点：

```
source=hostap,wlan0,wlan,8 
channelhop=false
```

下一个需要调整选项是信道速度（channel velocity）。它控制 Kismet 每秒应循环多少个信道。默认设置为每秒三个信道。这是一个可接受的，尽管保守的选项。要增加 Kismet 跳频的速度，请增加此数字。要降低速度，请减少此数字：

```
# How many channels per second do we hop? (1-10)
# The following option scans each channel for 1/5 of a second
channelvelocity=5
# The following option scans each channel for 1/2 of a second
channelvelocity=2
```

跳频和 GPS 配置之间的选项默认设置正确，通常不需要编辑。如果你使用 GPS 单元来捕获报告坐标，则应设置 GPS 配置选项。除非更改端口，否则 GPSD 监听端口 2947；因此，kismet.conf 中 GPS 的选项应设置为反映此情况：

```
# Do we have a GPS?
gps=true
# Host:port that GPSD is running on. This can be localhost OR remote!
gpshost=localhost:2947
```

下一个需要查看的选项是日志文件的写入间隔。默认设置是每 5 分钟写入一次日志。对于随意的驱动漫游，这可能是可以接受的；但是，对于专业人士，在系统或程序崩溃的情况下定期写入日志是个好主意（每分钟是一个安全的选择）：

```
# How often (in seconds) do we write all our data files (0 to disable)
writeinterval=60
```

Kismet 生成非常全面的日志文件集，如表 1.1 所示。

# 表 1.1 Kismet 日志文件类型

| 文件类型 | 描述 |
|---|---|
| Dump | 原始数据包转储，可以在 Ethereal 或其他数据包分析器中打开。 |
| Network | 列出已检测到的网络的文本文件。 |
| CSV | 检测到的网络的逗号分隔列表 |
| XML | 检测到的网络的可扩展标记语言（XML）格式日志。这对于导入其他应用程序很有用。 |
| Weak | 以 AirSnort 格式检测到的弱初始化向量（IV）数据包。 |
| Cisco | Cisco 设备产生的 Cisco 发现协议（CDP）广播日志。 |
| GPS | 检测到的接入点的 GPS 坐标日志。 |

