
```bash
mount -t nfs|nfs2 dirname
df -F nfs|nfs3 -k
```

## 网络：2.6 让 NFS3 与 NFS2 通信

帮助页 `Man pages`：

- `df`, `fstab`, `mount`, `nfs`, `vfstab`

世界维网：

- `RFC 1813 NFS 第 3 版本` --http://www.cis.ohio-state.edu/htbin/rfc/rfc1813.html

# UNIX 技巧与黑客目录

第 2 章：网络 | 上一章 | 下一章

本章节列表：

- 2.1 OSI 网络模型
- 2.4 远程网络配置
- 2.7 卸载与忙碌设备
- 2.2 查找故障
- 2.5 通过网络进行关机、停止或重启
- 2.8 静态路由或已路由
- 2.3 使用 NFS 隐藏文件
- 2.6 让 NFS3 与 NFS2 通信
- 2.9 使用 arp 获取以太网地址

上一节 | 下一节

# UNIX 技巧与黑客

+ 第 2 章：网络 2.7 卸载与忙碌设备

本章节列表：
2.1 OSI 网络模型
2.4 远程网络配置
2.5 通过网络进行关机、停止或重启
2.3 使用 NFS 查找文件
2.6 让 NFS3 与 NFS2 通信
2.8 静态路由或已路由
2.9 使用 arp 获取以太网地址

# 2.7 卸载与忙碌设备

### 2.7.1 描述

处理那些被他人占用或包含文件而需要卸载的挂载设备。

示例

语法：

```
kill PID
showmount -a
umount fsname
```

卸载各种设备有许多方法。在所有情况下，当设备处于忙碌且无法卸载时，你必须问自己：

- 谁在控制该设备？
- 设备是什么，正在进行什么？
- 从哪里访问该设备？

最困难的事情之一是跟踪是谁或什么打开了该设备。挂载设备可以从本地系统或远程系统挂载。它们可以从多个系统远程挂载。具有本地挂载设备的系统拥有磁盘驱动器、存储区域或 CD-ROM 驱动器。远程挂载的系统通常是连接到完全相同的设备，只是通过网络连接。

Unix 不会直接告诉你哪个用户。有时你必须进行一些演绎推理或执行一系列命令，并通过排除法，找到让设备进入忙碌状态的用户或进程。从本地开始，然后将搜索范围扩大到网络。

> 注意 - 在开始之前，请以 root 身份操作。不要使用 `su` 命令切换到 root 用户。确保你想要卸载的设备上没有打开打开的 shell。这在最后会节省大量的宝贵时间。

此示例展示了一个挂载的磁盘 `/disk2`。尝试卸载该设备。

```
rocket # umount /disk2
disk2: Resource Busy（资源忙碌）
```

然后检查使用该设备的本地进程。可能有一个进程正在使用该设备。如果是这样，你可以联系与进程相关的用户并杀掉该进程。

```
rocket # ps -ef
USER %CPU %MEM RSS TT S START TIME COMMAND
root 205 0.0 2.364 420 ? S 22:04:30 0.03 /usr/lib/psheip
```

```
gloriar   21960 0.0 2320 1672 pts/5   S 22:07:31  0:04 /disk2/bin/sbin
root       340 0.0 2320 1672 ?         S 22:07:31  0:04 /usr/lib/sendmail
```

```
rocket # kill 21960
```

如果这不起作用，并且为了检查系统或工作站上的用户数量，你可以联系每个用户并离开区域。这通常适用于有一两个两个用户的工作站。如果在生产服务器上需要，则应该断开设备，以通知用户并避免任何意外。

```
rocket # w | awk '{ print $1 }' | finger -s
Login       Name                TTY Idle             When
doe       John D.             q0    Thu 11:15
asmith     A. Smith            q1    Wed 17:11
johnson    H. Johnson          q3    Wed 18:05
gloriar    Gloria R.           q5    Wed 20:00
```

这条单行命令从 `w` 命令收集信息并提取出 ID。这可以告诉你谁在系统上，以便你可以直接联系他们。如果他们正在做重要的事情，那么设备的忙碌救了你。

```
rocket # umount /disk2
disk2: Resource Busy（资源忙碌）
```

如果最终设备仍然忙忙碌，你必须开始寻找远程连接到该设备的系统。使用 `umount` 命令，你可以看到连接到本地系统的所有挂载，以及它们挂载到的设备。

```
rocket # showmount -a
pilot:/disk2
```

### 变体：Solaris

语法：

```
df -F nfs
```

有一个名为 `showmount` 的命令。`df` 显示通过分布式文件系统共享的本地资源，以及已挂载的客户端列表。

```
rocket # df -F nfs
RESOURCE        CLIENTS
- /disk2             shuttle
- /local             shuttle
- /disk2             pilot
```

继续...

## UNIX 提示与技巧

目录 | 索引

# 第 2 章：网络

上一章 | 下一章

本章章节包含：
- 2.1 OSI 网络模型
- 2.2 查找故障点
- 2.3 使用 NFS 隐藏文件
- 2.4 远程网络配置
- 2.5 通过网络执行关机、停止、重启
- 2.6 NFS3 与 NFS2 的通信
- 2.7 卸载设备与被忙占的设备
- 2.8 使用 arp 获取以太网地址

上一节 | 下一节

## 2.8 静态路由或 routed

### 2.8.1 描述

系统可以使用两种方法（静态路由或 `routed` 进程）来确定网关的位置，以便将数据包路由到目的地。这两种方法各有优缺点。

## 示例一：默认路由

变体：AT&T 和 BSD

语法：

```
ifconfig interface
netstat -rn
route command [[modifiers] args] [metric]
```

为发往本地网关的数据包添加静态路由可以优化所有非本地数据包的传输。在使用这种方法时，无需在本地网络中搜索可用的网关。系统知道所有数据包都将导向一个特定的默认网关进行交付。

假设你的系统中有一个网络网卡，且这些网卡位于两个不同的子集（206.19.11 和 139.107.100）。如果你想将某些数据包发送到一个子网，将其余数据包发送到另一个子网，可以设置静态路由。要将数据包路由到 139.107.100 网关，并将其他数据包路由到 206.19.11 网关，设置方法如下：

```
# ifconfig ec0
ec0: flags=c63,BROADCAST,NOTRAILERS,RUNNING,FILTMU,MULTICAST
net 206.19.11.3 netmask 0xffffff broadcast 206.19.11.255
# ifconfig ec2
ec2: flags=c63,BROADCAST,NOTRAILERS,RUNNING,FILTMU,MULTICAST
net 139.107.100.18 netmask 0xffffff broadcast 139.107.100.255
# route add default 206.19.11.254 1
# route add net 139.107.100 139.107.100.254 1
```

| 目的 | 网关 | 子网掩码 | 标志 | 引用 | 使用 | 接口 |
| --- | --- | --- | --- | --- | --- | --- |
| default | 206.19.11.254 | | UG | 5 | 23617 | ec0 |
| | 139.103.243 | 139.107.100.254 | 0xffffff00 | UG | 0 | 6854 | ec2 |

```
# netstat -rn
```
