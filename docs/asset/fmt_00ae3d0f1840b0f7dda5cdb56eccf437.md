
## 总结

在本章中，我们查看了存储管理任务。Linux 支持大量的设备和文件系统方案。它还提供了许多互操作性功能。

## 延伸阅读

查看我们涵盖的命令的帮助页（man pages）。其中一些命令支持大量的选项。还可以查找关于向系统添加硬盘以及处理光介质的在线教程。

## 额外奖励

验证我们下载的 iso 镜像的完整性通常很有用。在大多数情况下，iso 镜像的发行者还会提供校验和。校验和是数学计算的结果，产生代表文件内容的数字。如果文件内容发生一个比特的变化，生成的校验和就会完全不同。最常用的方法是 `md5sum` 程序。当你使用 `md5sum` 时，它会产生一个唯一的十六进制数：

| `md5sum image.iso` |
| :--- |
| 34e35476f9bb7fb85c96f6a3fece `image.iso` |

下载镜像后，对其运行 `md5sum` 并与提供的校验和值进行比较。除了检查下载文件的完整性外，我们还可以使用 `md5sum` 验证新刻录的光介质。为了这样做，我们首先计算镜像文件的校验和，然后计算介质的校验和。验证介质的技巧是将计算限制在包含镜像的光质部分。我们通过确定镜像包含的 2048 字节块的数量并从介质读取相应数量的块来实现。在介质上：

| `md5sum /dev/cdrom` |
| :--- |
| 34e354768f9bb7fb85c96f6a3f9ece `/dev/cdrom` |

许多介质（如 DVD）需要精确计算块。在下面的示例中，我们检查镜像文件 `dvd-image.iso` 和 DVD 阅读器 `/dev/dvd` 中光片的完整性。你能猜出它是如何工作的吗？

```bash
md5sum dvd-image.iso; dd if=/dev/dvd bs=2048 count=$($(stat -c "%s" dvd-image.iso) / 2048 )) | md5sum
```

# 16 – 网络

在涉及到网络时，可能没有什么是 Linux 无法完成的。Linux 用于构建各种网络系统和设备，包括防火墙、路由器、名称服务器、NAS（网络附属存储）盒等。

正如网络领域非常庞大一样，用于配置和控制它的命令也极其非常多。我们将注意力集中在几个最常用的命令上。选用于检查的命令包括用于监控网络的命令和用于传输文件的命令。此外，我们将探索用于执行远程登录的 `ssh` 程序。本章将涵盖：

- `ping` - 向网络主机发送 ICMP ECHO_REQUEST
- `traceroute` - 打印通往网络主机的数据包路由
- `netstat` - 打印网络连接、路由表、接口统计、伪装连接和多播成员
- `ftp` - 非交互式文件传输程序
- `wget` - 非交互式网络下载器
- `ssh` - OpenSSH SSH 客户端（远程登录程序）

我们假设你具备网络背景知识。在当今互联网时代，每个电脑的人都需要对网络概念有基本的了解。为了充分利用本章内容，我们应该熟悉以下术语：

- IP（互联网协议）地址
- 主机和域名
- URI（统一资源标识符）

请参阅下方的“进一步阅读”部分，获取关于这些术语的一些有用文章。

> 注意：我们将涵盖的某些命令（取决于你的发行版）需要从你发行版的存储库中安装额外的软件包，某些命令可能需要超级权限才能执行。

## 检查和监控网络

即使你不是系统管理员，检查网络的性能和运行通常也有帮助。

### ping

最基础的网络命令是 `ping`。`ping` 命令向指定主机发送一种名为 ICMP ECHO_REQUEST 的特殊网络数据包。大多数接收此数据包的网络设备都会对其进行响应，从而验证网络连接是否正常。

> 注意：可以配置大多数网络设备（包括 Linux 主机）忽略这些数据包。这通常是出于安全考虑，为了在潜在的攻击者面前部分隐藏主机。防火墙配置为阻阻止 ICMP 流量也是常见操作。

例如，为了查看我们是否可以访问 linuxcommand.org（我们最喜欢的网站之一；），我们可以这样使用 `ping`：

```
me@linuxbox ~ ping linuxcommand.org
```

一旦启动，`ping` 就会以指定的间隔（默认为一秒）继续发送数据包，直到被中断为止：

```
me@linuxbox ~] ping linuxcommand.org
P linuxcommand.org (66.35.250.210) 56(84) bytes of data.
64 bytes from vhost.sourceforge.net (66.35.250.210): icmp_seq=1 ttl=43 time=107 ms
64 bytes from vhost.sourceforge.net (66.35.250.210): icmp_seq=2 ttl=43 time=108 ms
64 bytes from vhost.sourceforge.net (66.35.250.210): icmp_seq=3 ttl=43 time=106 ms
64 bytes from vhost.sourceforge.net (66.35.250.210): icmp_seq=4 ttl=43 time=106 ms
64 bytes from vhost.sourceforge.net (66.35.250.210): icmp_seq=5 ttl=43 time=105 ms
64 bytes from vhost.sourceforge.net (66.35.250.210): icmp_seq=6
ttl=43 time=107 ms
--- linuxcommand.org ping statistics ---
6 packets transmitted, 6 received, 0% packet loss, time 6010ms
rtt min/avg/max/mdev = 105.647/107.052/108.118/0.824 ms
```

在按下 Ctrl 中断后（在此是六个数据包之后），`ping` 会打印统计信息。正常运行的网络将显示数据包丢失率为零。成功的“`ping`”表明网络元素（网卡、布线、路由和网关）总体处于良好状态。

### traceroute

`traceroute` 程序（某些系统使用类似的 `tracepath` 程序）显示了从本地系统到指定主机网络流量经过的所有“跳数”列表。例如，查看到达 slashdot.org 的路由，我们这样做：

```
[me@linuxbox ~]$ traceroute slashdot.org
```

输出如下：
