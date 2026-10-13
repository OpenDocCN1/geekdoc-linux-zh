
# SCSI CD-ROM 处理

SCSI CD-ROM 的处理方式与硬盘略不同。第一个 CD-ROM 的条目为 `/dev/sr0`，而不是位于 `/dev/` 下的硬盘。第二个 CD-ROM 的条目为 `/dev/sr1`，依此类推。`dmesg` 命令的结果可以帮助你识别了哪些设备。另一种方法是检查 `/proc/scsi` 目录。这不会告诉你是分配到哪个设备条目的，但它会列出哪些 SCSI 设备。

CD-R 刻录机（也称为 CD-R 刻录器等）现在已经足够便宜可以实际购买。Linux 有能力使用多种类型的 CD-R 和 CD-RW（可重写）设备。使用它们首先需要两个软件包。首先是 `mkisos` 包，它包含在 Red Hat CD-ROM 中。该程序创建一个适用于写入 CD-R 或 CD-RW 的 ISO9660 镜像。第二个程序是 `cdrecord`，它执行 CD-R/CD-RW 的实际刻录工作。作者们只接触过 SCSI CD-R，所以你的体验可能会不同，但差别不大。

我们将首先采取安全做法，向你展示刻录 CD-ROM 的实际过程。首先，你必须创建一个 ISO9660 镜像。这需要在本地驱动器上有空间来存储新的镜像文件。如果你要制作一个占用 600MB 空间的 CD-ROM，你需要在分区上至少有这么多空闲空间。`mkisofs` 命令的基本语法为：

```
mkisofs -R -o file.raw /some/directory
```

- `-R` 执行递归拷贝，`/some/directory` 下的所有内容都会包含在原始文件中。
- `-o file.raw` 表示 `mkisofs` 命令的输出将进入 `file.raw`。这是你需要空间的地方。
- 还有两个你可能想使用的选项。`-v text` 选项将文本作为 CD-ROM 标签，在 Windows 或 MacOS 下显示。

ISO9660 规范规定文件必须采用旧 DOS 格式：八个字符、一个点和一个三个字符的文件扩展。幸运的是，ISO9660 有一个扩展允许扩展文件名 Joliet。Joliet 允许每个文件名包含 64 个字符。如果你选择使用 Joliet 和扩展文件名，请使用 `-J`。

现在 ISO 镜像已经创建，你可以通过挂载并查看它来测试。执行此操作的命令是：

```
mount -t isofs -o loop file.raw /mnt/cdrom
```

将 `file.raw` 替换为你刚刚创建的原始镜像。你也可以将 `/mnt/cdrom` 替换为其他要挂载的目录。`-o loop` 表示使用文件而不是实际设备。这将能够工作，你可以像访问 CD-ROM 一样遍历目录。一旦你确定镜像正确，就可以卸载该目录并准备写入。

创建原始镜像后，你现在可以使用 `cdrecord` 刻录 CD-R。首先，你需要知道 CD-R 的 SCSI ID。这可以通过查看 `/proc/scsi` 或使用 `cdrecord -scanbus` 并查看结果找到。你还需要知道你的 CD-R 可以处理什么速度。大多数驱动器的写入速度为双倍速 `2x` 或四倍速 `4x`。请检查文档以获取 CD-R 的能力。

现在进行实际刻录。`cdrecord` 的基本语法为：

```
cdrecord -v speed=4 dev=5,0 file.raw
```

你需要根据你的 CD-R 的能力更改速度。最低速度为 `1`，所以如果你遇到兼容性问题，尝试降低速度。`-v` 提供正在发生情况的详细列表。`dev=5,0` 列出了 CD-R 设备的 SCSI ID。在这种情况下，它是 SCSI ID 为 `5`，LUN 为 `0`。对于单 CD-R 刻录机，LUN 将为 `0`。你可以将 `file.raw` 替换为之前创建的镜像文件。在刻录过程中，最好不要使用该机器。CD-R 依赖于 FIFO 缓冲区填充以恒定速率写入 CD。如果该速率由于任何原因下降，刻录将失败，你将得到一张废光片。

刻录 CD-R 的时间取决于制作的镜像大小和 CD-R 的大小。四倍速 CD-ROM 可以在 18 分钟内刻录一张 74 分钟的 CD-R，大小约为 650MB。

一旦 CD-R 完成，你可以将其放入 CD-ROM 驱动器并进行测试。

## 21.3 网络配置

对于小型站点，一个良好的地址块选择将是可用的 C 类网络之一，这允许你的网络上有 254 台机器。在本章中，我们将使用 `192.168.1.0` 的 C 类网络。在 `192.168.1.0` 块中有两个预留的 IP：`192.168.1.0` 代表网络本身，以及 `192.168.1.255`，它是网关机器的广播地址。另一个预留的地址是 `192.168.1.1`。这通常用于防火墙，在我们案例中，也是防火墙。这并不是必须的，它只是一个经验法则。

在 `/etc/sysconfig/network/` 中，你将找到一个名为 `ifcfg-eth0` 的文件，其内容如下：

```
#!/bin/sh
#>>>Device: ethernet

#>>>Variable declarations
DEVICE=eth0
IPADDR=192.168.1.1
NETMASK=255.255.255.0
NETWORK=192.168.1.0
BROADCAST=192.168.1.255
GATEWAY=none
ONBOOT=yes
#>>>End variable declarations
```

配置网络后，重启机器并执行以下测试：

`netstat -nr` 的输出应为：

| 内核路由表 | 目的 | 网关 | 掩码 | 标志 |  Metric | 用 | 接口 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 192.168.1.0 | 0.0.0.0 | 255.255.255.0 | U | 0 | 0 | 28 | eth0 |
| 127.0.0.0 | 0.0.0.0 | 255.255.255.0 | U | 0 | 0 | 14 | lo |

`ifconfig` 的输出应为：

```
10 | Link encap:Loopback
inet addr:127.0.0.1 Bcast:127.255.255.255 Mask:255.0.0.0
UP BROADCAST RUNNING MTU:2000 Metric:1
RX packets:0 errors:0 dropped:0 overruns:0
TX packets:42 errors:0 dropped:0 overruns:0
eth0 | Link encap:10Mbps Ethernet Haddr:02:60:8C:49:05:57
inet addr:192.168.1.1 Bcast:192.168.1.255 Mask:255.255.255.255
UP BROADCAST MULTICAST MTU:1500 Metric:1
RX packets:0 errors:0 dropped:0 overruns:0
TX packets:26 errors:0 dropped:0 overruns:0
Interrupt:5 Base address:0x300
```

## 第 21 章 • 连接互联网

尝试：

- localhost: `ping 127.0.0.1`
- 本地 IP: `ping 192.168.1.1`
- 网络上的其他 IP 地址

如果你无法 `ping 127.0.0.1` 或 `192.168.1.1`，请重新检查你的配置文件。如果本地网络上的没有任何机器有响应，请检查从机器到网络其他部分的布线。如果你无法 ping 本地网络上的某些机器，可能是这些机器本身有问题，而不是防火墙机器的问题。

## 域名服务器

在继续 PPP 部分之前，还应该检查另外两个文件：

```
/etc/resolv.conf
order hosts,bind
search localdns_server, isname.net
nameserver <IPForNameserver1>
nameserver <IPForNameserver2>
```

```
/etc/hosts
127.0.0.1 localhost
192.168.1.1 gateway.localether.net
192.168.1.2 bob.localether.net
192.168.1.5 ralph.localether.net
```

我们建议保持 hosts 表简单——仅包含本地以太网机器的名称。虽然在 hosts 文件中添加一些常用机器的名称确实可以节省一些查询时间，但如果你有一台机器更改了其 IP，这可能会导致问题。

## 21.4 PPP

PPP 连接相当简单，因为需要处理的配置文件很少。用于 PPP 的只有两个主要程序：`pppd`（它是守护进程本身）和连接脚本。随之分发的常用有一个名为 `chat` 的程序，它专门设计用于“等待此字符串，然后发送此字符串”。另一个广为人知的程序是 `expect`，但它的灵活性和功能对于我们的应用来说过剩了。随 PPP 分发的默认配置文件可以正常工作，但不建议使用它们，因为它们存在安全漏洞。我们建议执行以下操作。
