

快速学习使用 tar，只需记住命令行上的几个简单调用即可。例如，要创建一个目录的压缩归档，使用 tar 的 czf 选项，如下所示：

```
$ tar czf dirname.tgz dirname
```

结果是一个压缩归档（以 .tgz 结尾的文件），包含指定的目录（以及其下的所有文件和目录）。在前面的选项中添加字母 v，即可查看压缩和归档过程中添加的文件列表。要列出压缩归档的内容，将 c 选项替换为字母 t，如下所示：

```
$ tar tzf archive
```

当然，如果归档中包含许多文件，更好的调用方式（便于阅读或滚动输出）是

```
$ tar tzf archive | less
```

要展开压缩归档的内容，使用 tar 的 zxf 选项，如下所示：

```
$ tar zxf archive
```

tar 实用程序会解压缩指定的归档，并在当前目录中提取其内容。

## 使用 /bin 和 /sbin 目录中的基本命令

/bin 目录（完整安装时约 5MB）包含系统用于运行和启动 Linux 的基本命令。一般来说，只有 root 操作员使用 /sbin 目录中的命令。其中许多（但不是全部）命令是静态链接的，这意味着此类命令不依赖于位于 /lib 或 /usr/lib 目录下的软件库。几乎所有其他应用程序都是动态链接的——意味着它们需要外部软件库（也称为共享库）才能运行。

## 使用和编辑 /etc 目录中的文件

- ► modprobe.d.—此文件夹保存加载内核模块所需的所有指令，作为系统启动的一部分，并取代了历史上的 modprobe.conf 文件。
- ► passwd—系统的用户列表，以及用户账户信息。此文件的内容可由各种程序更改，例如 useradd 或 chsh。
- ► printcap—系统的打印机功能数据库（在第 8 章“使用 Ubuntu 打印”中“Ubuntu 打印概述”一节中讨论）。
- ► shells—已批准的 shell（命令行界面）列表。

## 保护用户目录 /home 的内容

Linux 系统上最重要的<|message|> 数据位于用户目录中，位于 /home 目录下。将系统数据和用户数据分开有助于防止数据丢失并使备份过程更轻松。例如，让用户数据驻留在单独的文件系统或从网络上的远程计算机挂载，可能会在系统硬件故障发生时帮助用户免受数据丢失的影响。

## 使用 /proc 目录的内容与内核交互

/proc 目录的内容由内存创建，仅在 Linux 运行期间存在。此目录包含特殊的“文件”，可以从中提取信息或向内核发送信息。许多 Linux 实用程序从此目录下的动态创建的目录和文件中提取信息，该目录也称为虚拟文件系统。例如，free 命令从名为 meminfo 的文件获取其信息：

```
$ free
              total        used        free      shared  buffers   cached
Mem:       1026320     822112      204208          0    41282    481412
-/+ buffers/cache:     299468      726852
Swap:       2031608          0     2031608
```

此信息会随着系统使用而不断变化。你也可以使用 cat 命令查看 meminfo 文件的内容来获取相同的信息：

```
$ cat /proc/meminfo
MemTotal:       1026320 kB
MemFree:         204200 kB
Buffers:          41252 kB
Cached:           481412 kB
SwapCached:            0 kB
Active:           307232 kB
Inactive:         418224 kB
HighTotal:       122692 kB
HighFree:            244 kB
LowTotal:        903628 kB
```

```
LowFree:      203956 kB
SwapTotal:    2031608 kB
SwapFree:     2031608 kB
Dirty:        0 kB
Writeback:    0 kB
AnonPages:    202804 kB
Mapped:       87864 kB
Slab:         21736 kB
SReclaimable: 12484 kB
SUnreclaim:   9252 kB
PageTables:   5060 kB
NFS_Unstable: 0 kB
Bounce:       0 kB
CommitLimit:  2544768 kB
Committed_AS: 712024 kB
VmallocTotal: 114680 kB
VmallocUsed:  6016 kB
VmallocChunk: 108148 kB
HugePages_Total: 0
HugePages_Free:  0
HugePages_Rsvd:  0
Hugepagesize: 4096 kB
```

/proc 目录还可通过向 /proc/sys 目录下的特定文件“回显”数值来动态更改正在运行的 Linux 内核的行为。例如，要“打开”内核对一种称为 SYN flooding 的拒绝服务（DOS）攻击类型的保护，使用 echo 命令将数字 1 发送到以下 /proc 路径：

```
$ sudo echo 1 >/proc/sys/net/ipv4/tcp_syncookies
```

使用 /proc 目录的其他方法包括

- ▶ 从 /proc/cpuinfo 获取 CPU 信息，例如系列、类型和速度。
- ▶ 在 /proc/net 下查看重要的网络信息，例如 /proc/net/dev 下的活动接口信息、/proc/net/route 中的路由信息以及 /proc/net/netstat 中的网络统计信息。
- ▶ 检索文件系统信息。
- ▶ 通过 USB 报告媒体挂载点信息；例如，如果系统检测到 USB 相机或硬盘，Linux 内核会报告用于访问文件（如 /dev/sda）的设备。你可以使用 dmesg 命令查看此信息。

