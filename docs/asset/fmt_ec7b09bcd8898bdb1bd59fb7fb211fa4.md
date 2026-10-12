
- http://www.winehq.org—Wine 项目总部。请确保在“应用程序数据库”部分为你喜爱的使用 Wine 移植的 Windows 投票。

- http://www.von-thadden.de/Joachim/WineTools—WineTools 提供了相对简便的 Wine 安装方法以及许多知名的免费应用程序，包括 Internet Explorer。

- http://www.codewavers.com—Codewavers 公司，Crossover Linux 的制作者。

- http://frankson.org—此网站帮助你充分利用 Wine。它包含了常见问题解答（FAQs）和教程（HOWtos），帮助你解决大多数问题。

- http://www.fs-driver.org—Windows 的 ext2/3 IFS 驱动程序允许你从 dev2/3 分区打开并复制文件到 FAT 或 NTFS 分区。它为该系统创建一个驱动器。

- http://www.vmware.com—VMware 公司，你可以在这里获取免费 Server 和 Player 产品的信息，以及工作站虚拟机的 30 天评估版。

- http://www.win4lin.com—Win4Lin，构建 Windows 虚拟机。

- http://dosbox.sourceforge.net—DOSBox 网站。检查对你的 DOS 游戏的支持，并找到一些古老游戏的可下载副本。

- http://dosemu.org—DOS 模拟器 dosemu 的主页。

- http://www.freedos.org—FreeDOS 项目。用于在 DOSBox 或 dosemu 中使用的各种应用程序。

参考文献 243

- http://basilisk.cebix.net/—Basilisk II MacOS 模拟器主页。

- http://os-emulation.net/basiliskII/system753_tutorial/linux—关于在 Linux 上安装和运行 Basilisk II 的教程。

- http://xenource.com—Xen 开发的商业版。

- http://www.cl.am.ac.uk/Research/SRG/netos/xen—Xen 虚拟机监控器项目主页。

- http://www.fnn.nl/pages/articles/linux/vmware-player-image-creation.php—创建 VMware Player 镜像，带有可以下载的空镜像链接。

- http://sourceforge.net/projects/basisk—Basilisk II 项目页面。在此处可以用户论坛。

本页故意留白

# 第三部分

# 使用互联网

## 本部分内容

- 第 12 章 连接互联网 247
- 第 13 章 使用互联网：浏览网页和编写电子邮件 265
- 第 14 章 创建基础网站 289
- 第 15 章 管理邮件服务器 311
- 第 16 章 与他人协作 333
- 第 17 章 安全文件传输 357

本页故意留白

# 第 12 章

## 本章内容

# 连接互联网

- 基础连接信息
- 从本地回环接口 (`localhost`) 开始
- 配置你的拨号上网互联网连接
- 配置数字用户线路 (`DSL`)
- 将你的计算机连接到无线网络
- 何时联系你的互联网服务提供商 (`ISP`)
- 参考文献

正如在过去的十年里一样，互联网是全球计算机销售的主要驱动力。人们想要访问万维网，向朋友发送电子邮件和即时消息，了解更多关于这件事情的信息——好吧，也许不是。在充分尊重 openSUSE 的情况下，很难想象如果没有互联网，全球的程序员如何聚在一起开发内核以及使其运行的所有其他包。openSUSE 提供了访问和管理互联网的工具。在接下来的章节中，我们将关注连接的基础知识，无论是通过普通的拨号调制解调器还是高速数字用户线路 (`DSL`)。

## 连接信息

如果你已经在 Windows 下拥有互联网连接，最好预先获取一些信息，让你的设置变得简单一点。还有足够的 Linux 用户愿意为他们付费。有些 ISP 仍然无知或具有敌意。这导致了通用的支持，尤其是来自主要服务商的支持。

第 12 章 连接互联网

这意味着你你可能会得到一张包含所有启动内容的漂亮 CD，但 YaST 会处理这些。你需要了解的信息如下：

- 你的 IP 地址是静态的动态的 (`DHCP`)
- 域名系统 (`DNS`) 服务器的 IP 地址，特别是对于动态连接
- 邮件和新闻的 DNS 名称和 IP 地址
- 如果你使用拨号连接，ISP 的拨号号码
- 你的凭据密码

每台连接到互联网的计算机都必须有一个唯一的互联网协议 (`IP`) 地址。绝大多数标准 ISP 连接使用动态主机配置协议 (`DHCP`)。

注意：你将在下一步中需要它。返回虚拟机安装程序窗口并按 OK 继续。根据需要重复此过程。

你现在应该在 Xen 中拥有了一个可以运行的系统。

如果 `localhost` 尚未存在，你可以添加此行：

```
127.0.0.1    localhost
```

你可以留空短主机名（Short-Hostname）。保存并退出。重新打开你的 Root 控制台，并使用 `ifconfig` 和 `route` 来创建接口：

```
ifconfig lo 127.0.0.1
```

这会将 `localhost` 接口放入内存，与其他所有 Linux 网络接口并列，例如以太网 (`eth0`) 或拨号 (`pp0`) 接口。

```
route add 127.0.0.1 lo
```

这会将 IP 地址添加到路由表中，内核网络代码使用该表来跟踪到不同地址的路由。

再次运行 `ifconfig` 来测试新连接。

你应该能够通过尝试 `ping localhost` 来运行环回测试。你应该看到类似下面的内容（我们将使用 `-c` 选项计数发送 3 个数据包）：

```
# ping -c 3 localhost
PING localhost (127.0.0.1) 56(84) bytes of data.
64 bytes from localhost (127.0.0.1): icmp_seq=1 ttl=64 time=0.087 ms
64 bytes from localhost (127.0.0.1): icmp_seq=2 ttl=64 time=0.087 ms
64 bytes from localhost (127.0.0.1): icmp_seq=3 ttl=64 time=0.081 ms

localhost ping statistics
3 packets transmitted, 3 received, 0% packet loss, time 2000ms
rtt min/avg/max/mdev = 0.081/0.085/0.087/0.003 ms
```

我们已经完成了所有准备工作；现在是时候开始主课程了。

## 配置你的拨号上网连接

在 Linux 下设置拨号连接，如果没有对计算机硬件有深入了解，过去曾是相当困难的，但 YaST 为 openSUSE 用户大大简化了这一点。

当你设置拨号连接时，你只是在使用每种标准协议通过普通电话线将调制解调器连接到 ISP。大多数拨号连接使用点对点协议 (`PPP`)，因为 ISP 发现这是在串口（即调制解调器）上使用 TCP/IP 的一种高效方式。`PPP` 是为双向网络设计的，而 TCP/IP 协议族负责移动数据。

如果你无法想象一个没有互联网的 Linux 是一个成功的操作系统，那么为什么在 Linux 中设置拨号连接如此困难呢？事实上，Unix（以及它的 Linux 兄弟）从一开始就具有网络意识，但这些机器被假设为通过电线和电缆连接的、具有静态 IP 地址的机器。这些工作站位于研究大学、公司办公室和科学实验室，用户可能会注销网络，但计算机始终在那里。Unix（以及 Linux）尚未准备好处理具有间歇性连接的计算机。个人电脑的协议是拼凑在一起并最终使其正常运行的。

你可能不再需要完全理解 `PPP` 就能拨号上网了，但以下是一个快速的入门介绍。

设置拨号连接实际上是在你的系统上安装 `pppd` 守护进程。该守护进程控制你的连接并运行另外两个进程。

高级别数据链路控制 (`HDLC`) 协议控制从你的计算机到 ISP 服务器的流流，而 `chat` 例程与调制解调器通信、拨号并报告你的连接状态（或偶尔的连接中断）。

如果你想确认 `pppd` 是否安装，请以超级用户 (`su`) 登录并带有 `--help` 参数运行 `pppd`。你将看到许多可以调优连接的参数，但偏离默认值是有风险的。

> 注意
> 某些设备可能仍在 Linux 下无法工作的软件接口。请参见第 2 章“准备安装 openSUSE”获取有关 Winmodems 的更多信息。

## 使用 YaST 设置你的拨号连接
