
由于目录也是文件，可以使用相同的文件恢复技术来恢复整个目录。Ext2fs 目录结构删除 mini-HOWTO（参见“参考”）是作为 Ext2fs 文件删除 mini-HOWTO 的配套编写的。

## 系统救援

要将整个 MBR 复制到文件，请使用命令：

```bash
sudo dd if=/dev/hda of=/tmp/hdambr bs=512 count=1
```

要恢复整个 MBR，请使用命令：

```bash
sudo dd if=/tmp/hdambr of=/dev/hda bs=512 count=1
```

若仅需恢复分区表而跳过启动代码，请使用命令：

```bash
sudo dd if=/tmp/hdambr of=/dev/hda bs=512 skip=446 count=66
```

当然，将 MBR 拷贝到软盘或其他存储设备是稳妥的。（该文件大小为 512 字节。）你需要在系统上运行 `dd` 来恢复它（这意味着你将使用后文描述的 Ubuntu 救援盘或任何等效设备）。

## 从通用启动软盘启动系统

如果你没有制作软盘或找不到制作好的软盘，任何 Linux 启动软盘（稍旧的版本或从朋友那里借来的）只要其内核版本相当相似就可以投入使用。（主版本和小版本号匹配即可——例如，`2.6.5` 可能适用于任何 `2.6` 系统，但不能适用于 `2.4` 系统。）你将按照之前描述的方法手动指定根分区和启动分区来启动系统。虽然可以确定会收到一些错误信息，但你至少可以获得一个基础系统运行，以便替换文件并恢复系统。

> 提示
>
> 在前面的案例中，假设你不需要任何特殊的文件系统或设备驱动程序即可访问根分区。如果需要，请在 LILO 行中添加指向它的 `initrd=` 参数。如果你不知道 `initrd` 文件的确切名称，那么在 LILO 中就无能为了，请学习使用 GRUB 启动软盘。

## 使用 GRUB 启动软盘

通用统一引导加载程序 `GRUB` 可以尝试在没有现用的自定义启动软盘的情况下从软盘启动系统。软盘镜像可以从 `ftp://alpha.gnu/gnu/grub-0.95-1386-pc.ext2fs` 下载并使用 `dd` 复制到软盘中。（在 Microsoft 系统上将使用 `write.exe`）。或者，如果你有一个使用 GRUB 的现有系统的启动软盘，那也可以工作。

`GRUB` 拥有自己的命令 shell、文件系统驱动程序和搜索功能（类似于 bash shell 中的命令补全）。可以使用 GRUB 软盘启动、检查驱动器分区并搜索内核和 `initrd` 镜像，从而使用它们启动系统。GRUB 文档完全值独立成章，内容非常详尽：除了 `info grub`（info 系统类似于用于文档的 man 系统）外，GRUB 文档还包含了一份值得阅读的教程。GRUB 引导加载程序如图 17.5 所示。

![](img/757e95bd85c59465935194247625328c_427_0.png)

图 17.5 GRUB 引导加载程序为即使是不熟悉的系统启动提供了惊人的灵。

## 使用恢复机制

当电脑启动时，Ubuntu 将显示一条消息，提示你按 Escape 键查看 GRUB 菜单。如果你这样做，将看到一个可启动的操作列表，其中包含你 Ubuntu 安装的恢复模式选项。如果你进入恢复模式，你将获得机器的自动 root 权限，可以在那里安全地修复你的问题。

或者，你可以插入 Ubuntu 安装盘并从那里使用恢复模式。请记住，这些恢复模式是设计用于严肃系统恢复目的的纯文本系统；不要指望它们是手持操作的，也不要指望它们有多么易用！

> 相关 Ubuntu 命令
>
> 以下命令在 Ubuntu 中中执行备份、恢复和还原操作时非常有用：
>
> - `amdump`—Amanda 是一个基于网络的备份系统，由 18 个独立的命令组成，用于 Linux。
> - `ark`—一个 KDE 桌面 GUI 归档工具。
> - `cp`—复制命令。
> - `scp`—安全外壳复制命令。
> - `cpio`—一种数据归档工具。
> - `dd`—一种数据复制和转换工具。
> - `gzip`—GNU 压缩工具。
> - `tar`—GNU 磁带带归档工具。

## 参考文献

- http://www.tldp.org/LDP/solhre/Securing-Optimizing-Linux-RH-Edition-v1.3/whywhen.html—关于使用 `dump` 和 `restore` 进行备份的讨论及示例。
- http://en.tldp.org/LDP/solhre/Securing-Optimizing-Linux-RH-Edition-v1.3/chap29sec306.html—使用 `cron` 通过 `tar` 进行自动备份。
- http://kmself.home.com/Linux/FAQs/backups.html—Linux mini FAQ 包含了一些关于备份媒体、压缩、加密和安全的有用但简短的注释。
- http://www.tldp.org/The Linux Documentation Project 提供了若干讨论备份和磁盘恢复的 HOWTO 文档。
- http://www.ibiblio.org/pub/Linux/docs/HOWTO/other-formats/html_single/Ext2fs-Undeletion.html—如果你需要从 ext2/3 文件系统中恢复删除的文件，请参考 Linux Ext2fs Undeletion。
- Ext2fs-Undeletion.html—如果你需要从 ext2/3 文件系统中恢复删除的文件，请参考 Linux Ext2fs Undeletion.

# 第 18 章 网络连接

本章使用此接口为你的计算机分配 IP 地址，这是 Ubuntu 建立 PPP 接口所所需的。

## 检查回环接口（Loopback Interface）的可用性

通常情况下，你不需要手动创建回环接口，因为 Ubuntu 会在安装过程中自动创建一个。要检查它是否已设置，你可以在 root 权限运行 `ifconfig` 命令来执行类似的操作：

```
$ ifconfig
lo Link enc:Loopback
  inet addr:127.0.0.1 Mask:255.0.0.0
  inet6 addr::/64 Scope:Host
  UP LOOPBACK RUNNING MTU:1634 Metric:1
  RX packets:13 errors dropped:0 overruns:0 frame:0
  TX packets:13 errors dropped:0 overruns:0 carrier:0
  collisions:0 txqueuel:0

  RX bytes:832 (832.0 b) TX bytes:832 (832.0 b)
```

你在此示例中看到的内容是回环接口存在且活跃的证据。`inet addr` 是分配给 localhost 的 IP 号，通常为 `127.0.0.1`，带有广播掩码 `255.255.255.0`，这表明该接口上的活动很少（RX = 接收，TX = 发送）。如果你的输出与上面不同，你必须在完成本节其余部分后手动配置 localhost 接口。

## 手动配置回环接口

localhost 接口的 IP 地址在一个文本配置文件指定，Ubuntu 使用该文件来记录各种网络 IP 地址。该文件名为 `/etc/hosts`，通常存在于系统中，即使它是空的。Linux 内核和其他网络工具使用该文件，使其能够访问本地 IP 地址和主机名。如果你没有配置任何其他网络接口，你可能会发现该文件只包含一行：

```
127.0.0.1 localhost.localdomain localhost
```

此行定义了特殊的 localhost 接口并为其分配了 `127.0.0.1` 的 IP 地址。你可能会听到或读到 localhost、loopback 和虚拟接口（dummy interface）等术语；所有术语都指向 IP 地址 `127.0.0.1` 的使用。回环接口表示 Linux 网络驱动程序看起来机器正在与一个仅连接一台机器的网络通信；内核在同一台计算机上发送和接收网络流量。虚拟接口表示从外部世界来看该接口并不真实存在；它仅供本地机器使用。

局域网上的每台联网 Ubuntu 机器都会使用此 IP 地址作为你的 localhost。由于某种原因 Ubuntu 计算机没有此接口，请编辑 `/etc/hosts` 文件添加 localhost 条目，然后以 root 权限使用 `ifconfig` 和 `route` 命令如下创建接口：

```
# /sbin/ifconfig lo 127.0.0.1
# /sbin/route add 127.0.0.1 lo
```

这些命令将在内存中创建 localhost 接口（在使用 Linux 时，所有接口如 `eth0` 或 `pp0` 都是这样创建的），然后将 IP 地址 `127.0.0.1` 添加到内部（内存中）表中，以便 Linux 内核的网络代码跟踪到不同地址的路由。

如前所示，使用 `ifconfig` 命令操作该接口。
