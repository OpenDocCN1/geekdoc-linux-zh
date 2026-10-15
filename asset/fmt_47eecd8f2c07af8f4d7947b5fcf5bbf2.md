
``` 
# rpcinfo -p
program vers proto  port service
100000 2 tcp 111 portmapper
100000 2 udp 111 portmapper
100024 1 udp 777 status
100024 1 tcp 779 status
100021 1 tcp 783 nlockmgr
100021 1 udp 1035 nlockmgr
100021 3 tcp 787 nlockmgr
100021 3 udp 1036 nlockmgr
100020 1 udp 1037 flockmgr
100020 1 tcp 792 flockmgr
100021 2 tcp 795 nlockmgr
100068 2 udp 1040 cmsd
100068 3 udp 1040 cmsd
100068 4 udp 1040 cmsd
100068 5 udp 1040 cmsd
100083 1 tcp 1036 ttdbserver
100005 1 udp 976 mountd
100005 1 tcp 978 mountd
100003 1 udp 2049 nfs
150001 1 udp 1003 pnfssd
150001 2 udp 1003 pnfssd
150001 1 tcp 1006 pnfssd
150001 2 tcp 1006 pnfssd
#
```

系统中正在运行许多对我喜欢使用的功能很重要的守护进程。`mountd`正在运行，这表明服务器可以在此计算机上挂载 NFS 文件系统。挂载发生还需要其他设置，但至少支持此功能的守护进程正在运行。此外，`pnfssd`正在运行，意味着我们支持基于 Windows 的 NFS 访问。

### arp

用于维护 IP 地址及其对应 MAC 地址列表的机制是 ARP 缓存。映射的地址仅在缓存中保留几分钟，因此如果你想查看最近映射的地址，可以使用`arp`命令，如下面的示例所示：

```
# arp -a
o2 (10.1.1.10) at 0:10:83:f7:a2:f8 ether
l1 (10.1.1.11) at 0:10:83:f7:2e:d0 ether
63.88.85.1 (63.88.85.1) at 0:30:94:b0:b8:a0 ether
l3 (10.1.1.200) at 0:10:83:fc:52:88 ether
tapel (10.1.1.14) at 0:10:83:f7:ae:32 ether
tapel (10.1.1.14) at 0:10:83:f7:ae:32 ether
tapel (10.1.1.14) at 0:10:83:f7:ae:32 ether
tapel (10.1.1.14) at 0:10:83:f7:ae:32 ether
63.88.85.18 (63.88.85.18) -- no entry
```

当前的 arp 条目通过`-a`命令显示。你可以使用`-s`选项创建条目。

### lanadmin

`lanadmin`用于查看和管理网络卡。不带选项发出`lanadmin`会进入交互界面，如下面的示例所示：

```
##### lanadmin
LOCAL AREA NETWORK ONLINE ADMINISTRATION, Version 1.0
Copyright 1994 Hewlett Packard Company.
All rights are reserved.
Test Selection mode.
```

# 局域网接口管理

## lan

- `lan` = 局域网接口管理

- `menu` = 显示此菜单

- `quit` = 终止管理

- `terse` = 不显示命令菜单

- `verbose` = 显示命令菜单

输入命令：`lan`

局域网接口测试模式：局域网接口 FPA 编号 = 0

## 局域网接口命令

- `clear` = 清除统计寄存器

- `display` = 显示局域网接口状态和统计寄存器

- `end` = 结束局域网接口管理，返回测试选择

- `menu` = 显示此菜单

- `fpa` = 局域网接口的 FPA 编号

- `quit` = 终止管理，返回 shell

- `reset` = 重置局域网接口以执行自检

- `specific` = 进入驱动程序特定菜单

输入命令：`d`

### 局域网接口状态显示

- FPA 编号 = 0

- 描述 = Land Hewlett-Packard 10/100 TX 半双工 TT - 1500

- 类型 (值) = ethernet-csmacd(6)

- MTU 大小 = 1500

- Bwcd = 100000000

- 站点地址 = 0x10831ffcaae

- 管理状态 (值) = up(1)

- 操作状态 (值) = down(2)

- 最后更改 = 237321866

- 入站八位位组 = 0

- 入站单播数据包 = 0

- 入站非单播数据包 = 0

- 入站丢弃 = 0

- 入站错误 = 0

- 入站未知协议 = 0

- 出站八位位组 = 820

- 出站单播数据包 = 28

- 出站非单播数据包 = 0

- 出站丢弃 = 1

- 出站错误 = 0

- 出站队列长度 = 0

- 特定值 = 65536?

按 <Return> 继续

在此示例中，我们执行了`lanadmin`，并指定我们要进入`lan`接口管理，且希望显示关于该接口的信息。

`lanadmin`也可以用于执行诸如使用`-M`和`-S`选项分别更改局域网接口的 MTU 或速度等任务。

### ndd

`ndd`用于执行网络调优并查看有关网络参数的信息。要使用`ndd`查看有关所有受支持可调节参数的信息，您需要执行`ndd -h supported`。您可以使用`-get`选项获取参数的值；您可以使用`-set`选项设置参数的值。

### nslookup

`nslookup`用于将主机名解析为 IP 地址。您执行`nslookup hostname`，`nslookup`将访问`/etc/resolv.conf`文件或`/etc/hosts`来解析主机名。以下示例显示一个使用`/etc/hosts`生成系统 12 的 IP 地址的系统：

```
# nslookup 12
Using /etc/hosts on:	13

looking up FILES
Name:	12
Address:	10.1.1.12
#
```

您还可以通过在不带任何命令行参数的情况下发出命令来运行`nslookup`的交互模式。以下示例显示在不带任何命令行参数的情况下发出命令以进入交互模式，然后输入 help 以获取有关您可以发出的命令的信息：

```
# nslookup 12
> help
NAME		-	print address information about NAME
IP-ADDRESS	-	print hostname information about IP-ADDRESS
policy		-	print switch policy information
server NAME	-	set default server to NAME, using current default server
lserver NAME	-	set default server to NAME, using initial server
```

其他网络命令和设置

- `set OPTION` - 设置`OPTION`

- `all` - 打印选项、当前服务器和主机

- `[no]swtrace` - 打印查找结果和查找开关消息

# 第 14 章

# 通用桌面环境

## CDE 和虚拟分区

在同一台计算机上运行多个 HP-UX 实例就像拥有多个系统一样。这意味着您在不同 vPar 中为用户配置的通用桌面环境 `CDE` 与在不同系统上配置的方式完全相同。有一些配置文件会在系统范围内影响 `CDE`。您需要在每个 vPar 上设置这些系统范围的配置文件，以满足在相应 vPar 中工作的特定人员的特定需求。

在接下来的部分中，我们将在虚拟分区中修改 `CDE`，以在登录屏幕上包含自定义的 `CDE` 问候语，并自定义菜单以包含一些特定于虚拟分区的命令。

用户在 vPar 系统上第一次接触 `CDE` 时看到的是登录屏幕。让我们自定义登录屏幕，使其显示主机名（这很可能已经在您的 `CDE` 登录屏幕上配置好了），以及作为问候语的一部分的 vPar 名称。如果您的主机名和 vPar 名称相同，则您不需要在登录屏幕上提供 vPar 名称。这是对 `CDE` 的一个有趣自定义，因此我将提供登录屏幕更改作为自定义示例。

登录屏幕的默认信息包含在`/usr/dt/config/C/Xresources`中。我们将把这个文件复制到`/etc/dt/config/C/Xresources`，然后将 vPar 名称添加到文件中。该文件中包含`GREETING`的部分如下所示：
