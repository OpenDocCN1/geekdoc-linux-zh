

# 118 第 4 章 常用工具

## umount

```
umount [options] device|mount_point [-t vftype]
```

umount 命令将列出的文件系统或在指定挂载点上的文件系统从 Linux 树中卸载。当文件系统包含打开的文件、有用户位于其目录树的某处或包含正在使用的交换文件（swap file）时，无法进行卸载。

## showmount

```
showmount [options] [host]
```

showmount 命令向远程机器上的挂载守护进程查询其 NFS 服务器的状态。如果没有指定任何选项，showmount 命令将返回所有从该主机挂载的客户端列表。

## ulimit

```
ulimit [options] [limit]
```

ulimit 命令用于确定 shell 及其启动进程的资源限制。ulimit 的参数包括 -a 用于报告所有当前限制，-c 用于最大核心大小，-f 用于最大文件大小，-n 用于打开的文件数，以及 -u 用于每个用户的进程数。ulimit 还可以通过指定正确的参数后跟新的数字值来调整这些限制。在选项前加上 H 设置硬限制（hard limits），一旦设置将无法增加。加上 S 设置软限制（soft limit），可以一直增加直到达到硬限制。如果既没有 H 也没有 S，则假设为软限制。

要确定最大核心大小的硬限制，请使用列出的 ulimit 命令。返回值显示在 Red Hat 系统上，核心文件的大小没有硬限制。

```
# ulimit -Hc
unlimited
```

要将最大核心大小设置为 1024，请执行以下命令：

```
# ulimit -c 1024
```

现在通过执行不带数值的 ulimit -c 命令来检查你的工作。结果应该是你指定的数值。

## mkswap

```bash
mkswap [options] device [size]
```

mkswap 命令在指定的设备或文件上创建交换区域（swap area）。交换区域用于将页面从内存中换出，使其能够更快地读回内存。在 Linux 中，交换空间的大小为系统内存的两倍通常就足够。大多数情况下，包含交换空间的设备是磁盘分区，但也可以使用用 dd 命令创建的文件，如下：

```bash
# dd if=/dev/zero of=/dev/swapfile bs=1024 count=65536
```

copy 命令无法用于创建交换文件。创建设备或文件后，必须使用 swapon 命令激活交换区域。

在 Linux 系统首次安装时通常会创建一个交换分区。请参阅第 2 章获取有关如何作为独立分区创建交换空间的更多信息。

## swapoff

```bash
swapoff [-a]
swapoff specialfile(s)
```

swapoff 命令禁用指定设备或文件上的交换。如果使用 -a 选项调用 swapoff，etc/fstab 中的所有交换条目将被禁用。

## swapon

```bash
swapon [-v] [-p priority] specialfile(s)
swapon [-a]
```

swapon 命令启用指定设备或文件上的交换功能，或者如果给了 -a 选项，则启用 /etc/fstab 列出的所有设备。这通常是在运行级别（run level）更改时由 rc 脚本完成的。

## sync

```bash
sync [options]
```

sync 命令刷新文件系统缓冲区，从而强制任何等待在那里的数据写入磁盘。当你挂载另一个文件系统并对其进行更改时，此命令是必要的，以确保所有应写入挂载文件系统的数据都已写入。

## 120 第 4 章 常用工具

## fuser

```bash
fuser [options] filesystem
```

fuser（file 命令）确定哪个用户正在使用给定文件系统中的文件，或者当前位于属于给定文件系统的目录中。如果你尝试卸载文件系统并被提示它正忙碌，那么这一点非常重要。如果文件系统已挂载，则需要 -m 选项。使用 -u 选项可以获取该文件系统的进程和相应的用户信息。在下面的示例中，多个进程 ID 之后的 c 表示这些进程正在当前目录运行。

```bash
# fuser -mu /home
```

```
/home:
1456(user) 4271(user) 4301(user) 4456(user) 5729(user)
```

## 网络命令

本节中的命令与网络连接有关并被频繁使用。这些命令允许你判断网络接口是否正常运行并检查其效率。第 5 章涉及 TCP/IP 连接，第 7 章涉及与此类连接相关的安全问题。

## ifconfig

```bash
ifconfig [interface]
ifconfig interface [address] [options]
```

ifconfig 命令显示当前活动接口的状态。如果将接口作为唯一参数列表，ifconfig 将返回该接口的状态。ifconfig 命令也可用于配置网络接口，尽管在脚本外很少使用。列表 4.6 显示了此命令的输出。

### 列表 4.6 ifconfig 的示例输出

```
eth0 Link encap:Ethernet addr 00:55:A0:52:33 inet:192.168.1.1 Mask:255.255.255.0 UP BROADCAST RUNNING MULTICAST
lo Link encap:Loopback addr 127.0.0.1 Mask:255.0.0.0 UP BROADCAST RUNNING MULTICAST
```
*(注: The example output was slightly fragmented in the source text, I have cleaned it for readability while maintaining the content)*.

## 命令行工具

## netstat

```bash
netstat [options]
```

netstat 命令显示网络连接、路由表、接口统计和多播组成。-n 选项强制使用 IP 地址而不是主机名。

## ping

```bash
ping [options]
```

ping 命令用于测试网络连接。它向指定的主机发送信号，等待响应包并报告接收情况。ping 命令主要用于网络故障排除。示例见第 18 章。

## route

```bash
route [options] add [-net|-host] target [options]
route [options] del [-net|-host] target [options]
```

route 命令用于显示和操作 IP 路由表。它主要用于已配置的主机或网络设置静态路由。

## ftp

```bash
ftp [options] host
```

ftp 命令启动互联网文件传输协议，允许与远程站点传输文件。它通常是交互运行的，可以通过 -i 选项关闭。

## telnet

```bash
telnet [options] [host|port]
```

telnet 命令使用 Telnet 协议与主机通信，在未指定主机时进入命令模式。在命令模式下，telnet 接受 OPEN（打开主机站点）、CLOSE（关闭主机站点）、QUIT（退出 telnet 会话）和 STATUS 等命令。

## traceroute

```bash
traceroute [options] destination_host
```

traceroute 命令允许你确定数据包到达目标主机路径上每一跳所需的时间。当向主机的传输明显延迟或未接收时，这些信息非常有用。每个中间主机都会列出跳转所需的时间（毫秒）。列表 4.7 显示了示例输出。

### 列表 4.7 traceroute 命令的示例输出

```
traceroute 216.15.152.66 (216.15.152.66), 30 hops max, 38 bytes packets
1 lvhun1.popsite.net (216.126.175.4) 107.606 ms 98.544 ms 99.231 ms
2 bhm1-core1.popsite.net (216.126.175.1) 106.141 ms 109.084 ms 109.090 ms
3 atl-core1-s1-3.popsite.net (216.126.168.221) 116.211 ms 108.875 ms 109.361 ms
```

