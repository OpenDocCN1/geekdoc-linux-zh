
## 图 9.8

添加打印机向导可以

![](img/38aae1e03db8863dab67582599f6fc83_293_0.png)

用于打印的另一种方法是打印机管理器，如图 9.9 所示。

## 图 9.9

打印机管理器提供了

![](img/38aae1e03db8863dab67582599f6fc83_293_1.png)

无论使用哪种方法添加打印机，都会发生一些事情：

- 打印队列被添加到 `/etc/cups/printers.conf`。
- 打印机的 `ppd` 文件被放置 `/etc/cups/`。
- 打印队列被添加到 `printcap`。

## 图 9.10

你可以选择 CUPS 作为类型。

![](img/38aae1e03db8863dab67582599f6fc83_294_0.png)

## 基础配置文件

打印服务工作需要几个文件。其中最重要的是 `printcap`、`lpd.perms` 和 `lpd.conf`。`/etc/printcap` 文件是定义每台打印机能力的数据库。使用 `LPRng`（此处原文为 LPRng）添加打印机后，该文件的默认版本所示：

```
# /etc/printcap：打印机数据库。参见 printcap(5)。

sd=/var/pool/lpd/%P

# 用于临时存储打印作业的溢池目录%。P 将扩展打印队列扩展。每个打印队列必须有不同的溢池目录，通过使用 %P 保证了这一点。

#:sh - 抑制 banner 或标题页

#mx=0 - 最大作业大小，单位为 K 字节（0 为无限制）

#:mc=0 - 最大副本数（0 为无限制）

# 管理打印

第 9 章

# LPD 打印队列定义：定义打印队列
# 并行端口上的打印机（即 - /dev/lpt0）
#lp:lp-DEVICE:tc=.common
#  示例：
#  lp:tc=.common:lp=/dev/lpt0
#  [翻译:
#   lp 打印队列的名称
#   tc=.common 包含 .common 文件中的选项
#   printcap 条目中的 'tc' 选项将被放在
#   printcap 条目的开头
#   lp=/dev/lpt0 - 打开并写打印作业写入
#   /dev/lpt0
#  ]
# 串口端口上的打印机（即 - /dev/tty00）
# 使用 setty 通过 'tty(1)' 选项设置速度、位和奇偶校验。
# 注意：几乎所有打印机都使用 8 位
# 且无奇偶校验。
#lp:tc=.common:lp=DEVICE:STTY OPTIONS
#  示例：
#  lp:tc=.common=/dev/tty0:tty=19200 crw crtscs
#  [翻译:
#   :tc 如上文 A。
#   :tty= 选项用于配置串口
#  ]
# 网络打印服务器上的打印机（即 - HP JetDirect）
# 通过 TCP/IP 套接字连接。IPADDR 是打印服务器的
# IP 地址或完全域名，PORT 是
# TCP/IP 端口。
# HP Jetdirect 默认使用端口 9100。
# 警告：请检查网络打印服务器文档以获取
# 正确端口号。大多数非 HP 网络打印服务器
# 和非 HP 打印机不使用端口 9100。
#lp:tc=.common:lp=IPADDR:PORT
#  示例：
#  lp:tc=.common:lp=10.0.0.2%9100
#  [翻译: lp, :tc, 如上文 A。]
```

# Novell 认证 Linux 专业学习指南

```
# lp=10.0.0.2%9100 - 打开到 10.0.0.2 端口 9100 的连接
# 并将打印作业写入此端口。
# ]
```

# 网络打印服务器上的打印机（即 - HP JetDirect 或 LPD 服务器）

# 通过 LPD 打印协议连接。QUEUE

# 是打印队列的名称，IPADDR 是打印

# 服务器的 IP 地址或完全域名。

# 警告：检查网络打印服务器文档以获取

# 正确的 QUEUE 名称。HP JetDirect 使用 'lp' 队列

# 作为默认打印队列。如果设备上有

# 多个打印机端口，则使用 QUEUE 名称

# 来选择端口。

# 警告：在 JetDirect 设备上使用此协议将

# 始终导致 JetDirect 设备生成“标题页”（banner page）。

# 请查看 HP 文档了解如何禁用

# 这个最烦人的功能。通常你只需要

# telnet 到 JetDirect，然后使用在首次

# 建立连接时呈现的简单配置菜单。

```
# lp:tc=.common:lp=QUEUE@IPADDR
# 示例：
# lp:tc=.common:lp=lp6@10.0.0.2
# [翻译: lp ,tc 如上文]。
# lp=10.0.0.2 - 打开到 10.0.0.2 端口
# 515 的连接，并使用 RFC1179 (LPD) 协议将
# 作传输到 QUEUE 打印队列。
# ]
```

## 步骤 4：需要格式转换（过滤器）吗？

# 你可能会发现你的打印机不支持

# PostScript 或需要进行特殊的初始化。

# 这由过滤器程序处理。'ifhp'

# 过滤器程序由 LPRng 提供，支持大量的

# 打印机。如果你需要过滤器，

# 请在 printcap 条目中添加以下行：

```
# :filter=PATH_TO_IFHP_FILTER
# :ifhp=IFHP_OPTIONS
```

# 注意：LPRng 的 :filter= 选项替换了旧的

# BSD :if, :vf, ...，这些用于指定

# 'f' 格式、'v' 格式等的过滤器（是的,:if

# 用于 'f' 格式，别问）。:filter 选项指定

# 所有作业格式的默认过滤器。大多数现代过滤器

# 如 IFHP、Magicfilter 和 Red filters

# 足够判断作业格式并执行

# 适当的转换。

```
# 示例：
# lpc=:common:lp=/dev/lp0
# :filter=/usr/libexec/ifhp
# :ifhp-model=hp4simx
```

```
# lpc=:common:lp=10.0.0.2%9100
# :filter=/usr/libexec/ifhp
# :ifhp-model=hp4simx
```

```
# lpc=:common:lp@10.0.0.2
# :filter=/usr/libexec/ifhp
# :ifhp-model=hp4simx
```

# IFHP 选项：

# 对于几乎所有的简单配置，你都需要

# 提供你所连接的打印机型号。

# 请查看 `/etc/ifhp.conf` 文件获取支持模型的

# 列表。默认型号是 HP

# LaserJet 4，它支持 PostScript、PCL 和

# PJL。

```
# 警告：
# 如果：
# 你的打印机通常通过 TCP/IP 链路提供
# 状态和报告
# 并且：
# 你正在使用 lp=IPADDR%PORT 连接到
# 打印机
#那么：
# IFHP 过滤器通常期望获得打印机
# 返回的状态以告知打印机
# 处于工作状态。这将对作业吞吐量产生
# 小但显著的开销，但你也能获得错误信息。
# 但是：
# 如果打印机应该返回状态但无法通过
# 硬件配置，或者它位于单向而非双向
# 端口，那么你必须使用 :model=...,status@
# 告诉 IFHP 过滤器不要等待状态。
# 示例：
# lp=tc=.common:lp=10.0.0.2
```

# 管理打印

## 第 9 章

| | V | SA | SA | SA |
| :--- | :--- | :--- | :--- | :--- |
| FORWARD | V | SA | SA | SA |
| SAMEHOST | V | SA | SA | SA |
| SAMEUSER | V | SA | SU | SU | SU |
| SERVER | V | SV | SV | SV | SV |
| LPC | S | | LPC | | |
| AUTH | V | AU | AU | AU | AU |
| AUTHTYPE | S | AU | AU | AU | AU |
| AUTHUSER | S | AU | AU | AU | AU |
| AUTHFROM | S | AU | AU | AU | AU |
| AUTHSAMEUSER | S | AU | AU | AU | AU |

`REMOTEIP` 是 `REMOTEHOST` 的别名

- `REMOTEPORT` 是 `PORT` 的别名
- `IP` 是 `HOST` 的别名

## 密钥：

- `JH` = 控制文件中主机的 IP 地址/DNS 名称
- `RH` = 连接的远程主机 IP/DNS 名称
- `JUSR` = 控制文件中的 USER 用户
- `CUSR` = 发起控制请求的 REMOTEUSER 用户
- `JIP` = 控制文件中主机的 IP 地址/DNS 名称
