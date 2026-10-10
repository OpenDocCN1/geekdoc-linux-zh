
- [http://world.std.com/~corey/raylink.html](http://world.std.com/~corey/raylink.html)
  Raytheon 和 Webgear 无线网卡最新驱动程序的主页。

- [http://www.hpl.hp.com/personal/Jean_Tourrilhes/Linux/](http://www.hpl.hp.com/personal/Jean_Tourrilhes/Linux/)
  关于 Linux 和无线局域网的详细概述。权威的 Linux 无线局域网 HOWTO。

- [http://www.webgear.com/support/software_top.html](http://www.webgear.com/support/software_top.html)
  Webgear, Inc. 的支持页面，包含指向 Aviator 2.4 无线局域网卡 Linux 驱动程序的链接。

- [http://www.computer.org/students/looking/summer97/ieee802.htm](http://www.computer.org/students/looking/summer97/ieee802.htm)
  关于无线网络的简短教程。

- [http://www.metricom.com/](http://www.metricom.com/)
  Ricochet 调制解调器无线服务的主页。

- [http://www.panix.com/~dfoster/prog/linux/pppoe.html](http://www.panix.com/~dfoster/prog/linux/pppoe.html)
  Dave Foster 关于 Bell Atlantic、Linux 和 DSL 的页面。包含大量优质信息和指向 Linux DSL 软件的链接。

- [http://www.roaringpenguin.com/pppoe.html](http://www.roaringpenguin.com/pppoe.html)
  Roaring Penguin Software 的主页，这是一家使用 Linux 的小型咨询公司，因其免费的 Linux PPPoE 客户端（当然包含源代码）而值得获得大量的虚拟啤酒。

- [http://sidhe.folkwolf.net/~chris/pppoe-howto/](http://sidhe.folkwolf.net/~chris/pppoe-howto/)
  一个 PPPoE Linux HOWTO。它详细介绍了比使用 Roaring Penguin 的 PPPoE 客户端更为复杂的设置。

- [http://www.rodbooks.com/network/network-dsl.html](http://www.rodbooks.com/network/network-dsl.html)
  Rod Smith 关于 Linux 和 DSL 的综合指南。它包含许多指向其他 PPPoE 软件客户端和 Linux DSL 页面的优质链接。

- `/usr/doc/ppp/README.linux`
  关于在 Linux 中使用 pppd 守护进程的直白讨论（内部标题为“Linux 的 PPP”，版本 2.3.10）。它是一个带有逐步说明的优秀教程。

## 第 16 章：时区和区域设置

- Linux、时间和时区
- 显示和设置时间
- 追踪你所在的位置
- TZ 环境变量
- 获取准确时间
- 有用的客户端
- 资源信息

本章关于时间：Linux 如何使用时间，你如何使用时间，以及如何在你的笔记本上保持准确的时间追踪。时间是一种宝贵的资源。我们似乎永远都不够时间，如果我们失去了对时间的掌握，可能会陷入麻烦。很少有涉及 Linux 的书会详细涵盖时间问题。原因之一是，大多数用户在安装 Linux 之后很少需要思考或调整时间和时区设置。此外，大多数默认设置已经足够好用了。

然而，在某些情况下，时间定时问题可能至关重要。例如，如果你在旅途中，离家数千英里，你的移动 Linux 环境很可能具有错误的时间，甚至可能具有错误的日期。你生成的文档或发送的电子邮件消息可能包含不正确的日期和时间信息。你也可能错过约会、日程安排或旅行安排。

如果你的工作要求你密切追踪时间，那么时间也很重要。按可计费小时追踪的工作对于使用技术员、计算机顾问或律师的公司来说变得非常有价值（且昂贵）。

网络管理员知道时间有多么重要，特别是在制作全网备份脚本或计划时。本地连接的计算机都必须设置为相同的日期和时间，以便在备份操作期间按命令或顺序正常执行这一点至关重要。如果日期和时间不同步，协调脚本或程序的同步处理将变得不可能。其他问题包括保持准确的日期和时间，特别是在具有密码过期的系统上。

影响移动 Linux 用户的问题包括 APM，它可能会或不可能会偏移、重置、禁用或以其他方式破坏 Linux 或（更糟糕的是）计算机硬件时钟的正确时间设置（后者将是 BIOS 的故障，而不是 Linux 的）。

## Linux、时间和时区

Linux 使用的日期和时间（称为系统时间）与你的笔记本的实时时钟或硬件时钟使用的日期和时间之间存在差异。许多经验丰富的移动 Linux 用户将笔记本时钟设置为协调世界时，即 UTC（或者，在军事中称为 ZULU）。然后他们设置 Linux 系统时间作为 UTC 的偏移量。这样做的优势是提供了一个基础时间值，你可以轻松地在旅行时在系统中调整或更新它。

## 地球时间还是原子时间？

大多数人认为 GMT 或更准确地说是 UTC 是基于英国格林威治的时间。然而，UTC 是基于全球维护的原子钟并通过无线电分发。时间的另一个变体是 UT1，它基于地球的旋转角度。这些时间可能不同！当这种情况发生时（大约每 18 个月一次），根据美国海军天文台，会在 UTC 中引入一个闰秒。关于详细讨论，请访问 [http://tycho.usno.navy.mil/leapsec.html](http://tycho.usno.navy.mil/leapsec.html)

如你所知，世界被划分为许多不同的时区。这些时区以经度 0 为基准，向东和向西按小时（在某些情况下为 30 分钟）递增，该经线穿过英国格林威治（因此常用但技术上未使用的术语是格林威治平均时间，即 GMT）。例如，美国时区以一小时为增量负偏移（因为它们位于经度 0 以西）。

Linux 在 `/usr/share/zoneinfo` 目录下维护时区信息的数据库。这些信息，连同系统时间，可以由几乎每个 Linux 发行版中包含的各种命令进行操纵和使用。这些命令列在表 16.1 中。

Linux 系统时间基于自 1970 年 1 月 1 日以来经过的秒数。秒数目前存储为 long 数据类型（32 位无符号值），但这个值（与 MacOS 不同；见下文侧边栏）在 2038 年 1 月 19 日之前将不足以容纳正确的秒数。虽然大多数时间计算不受影响，但有些会受到影响，并且这可能由于在计算日期差异时做出的错误假设而导致问题。

### 苹果电脑的时间

Apple MacOS 对 Y2K 问题免疫，因为时间存储为 64 位值，表示自 1904 年 1 月 1 日午夜以来经过的秒数。地理和时区数据存储在 Mac 的硬件（PRAM）中。这些信息包括纬度、经度、夏令时（DST）和 UTC（在 Apple 的编程手册中口语化地指定为 GMT）。

Red Hat, Inc. 已认证至少基于 Intel 的 Linux 系统中，其发行版的核心 15 个时间相关命令、6 个时间相关守护进程和 6 个相关软件库符合 Y2K 标准。

**表 16.1** Linux 时间、时区、日期和日历命令

| 命令 | 描述 |
| :--- | :--- |
| asclock | AfterStep 微型数字时钟 |
| astime | AfterStep 微型模拟时间客户端 |
| bash (time) | bash  shell 的 `time` 功能 |
| cal | 日历命令 |
| convdate | 转换日期和时间信息 |
| date | 设置系统日期和时间 |
| ddate | 转换日期 |
| find | 包含时间功能的搜索实用程序 |
| gtt | GNOME 时间追踪客户端 |
| hwclock | 显示和设置系统或硬件时钟 |
| ical | 日历和约会调度器 |
| karm | KDE 个人时间追踪客户端 |
| kcmclock | KDE 时区、日期和时间客户端 |
| kmoon | KDE 月相面板客户端 |
| korganizer | KDE 个人约会调度器 |
| kteatime | KDE 泡茶计时器面板客户端 |
| kworldwatch | KDE 墨卡托太阳投影仪 |
| newer | 比较文件修改时间 |
| nwfstime | 获取和设置 NetWare 服务器日期和时间 |
| rclock | 带有约会调度的 X11 时钟客户端 |
| rdate | 通过网络获取和设置系统日期和时间 |
| ruptime | 显示联网计算机的状态 |
| sleep | 让进程以秒为单位休眠 |
| time | 计时进程 |
| timed | timed 守护进程 |
| timetool | Red Hat 的图形客户端，用于设置日期和时间 |
| touch | 更新或设置文件或目录的时间戳 |
| tzselect | 选择时区 |
| uptime | 显示系统状态 |
| xclock | X11 时钟客户端 |
| xearth | 显示太空中的地球 |
| xfclock | XFCE 时钟和日历客户端 |
| zdump | 倾倒时区信息 |
| zic | 编译时区信息 |
