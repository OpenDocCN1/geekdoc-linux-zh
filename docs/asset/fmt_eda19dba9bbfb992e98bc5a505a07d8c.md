
Power Off on Shutdown（关机关电源）当系统停止命令（通常由 `shutdown` 脚本发出）执行时导致机器关机。此功能可能对支持软关机的后期台式机所有者感兴趣，或者如果他们的系统具有标准的 BIOS。

这里需要记住的主要点是，由于今天 PC 系统中 APM 的实现多种多样，某些或所有功能可能无法适用于你的特定 PC。如果你习惯阅读 C 语言和汇编源码，`drivers/char/apm_bios.c` 文件很有读价值（这当然是主观的），并包含了许多关于不同机器如何实现 APM 的注释。

# 第六部分

## 附录

### 附录 A 资源

Walnut Creek 网站是获取其他免费 UNIX发行版（如 BSD 或 Slackware Linux）的起点：

```
http://www.cdrom.com/
```

以下网站是 Linux 笔记本用户的权威网站。该网站包含许多不同的链接和文档，用于解决问题并为 Linux 和 X11 的正确运行提供解决方案：

```
http://www.cs.utexas.edu/users/kharker/linux-laptop
```

下载 Debian 发行版的权威网站如下：

```
http://www.debian.org/
```

想知道你喜欢的 Linux 网站是否已经更新或上传了新软件吗？使用此站点监控每日变化：

```
http://webwatcher.org/
```

Linux 的长期分发商 Infomagic 提供了通过 FTP 或 CD-ROM 提供的多套不同的软件合集：

```
http://www.infomagic.com
```

该网站不仅最旧和最新的内核，还提供了超过 20GB 的 Linux 软件：

```
http://www.kernel.org/
```

1997 年访问量超过 400 万次，该网站是广受欢迎的 Linux 网站之一，通常被认为是 Linux 的主页：

```
http://www.linux.org/
```

另一个非常好的 Linux 主页是同名的 Linux.com。作为获取 Linux 最新新闻的优质来源，该网站绝对值得关注：

```
http://www.linux.com/
```

这里是寻找 Sams、Que 和 New Riders 出版的 Linux 书籍的地方：

```
http://www.mcp.com/
```

Ken Lee 的 X 和 Motif 网站有超过 700 个指向不同 X 系统网页的链接（Ken 是 Motif FAQ 的维护者）：

```
http://www.rahul.net/kenton/index.shtml
```

Red Hat Software, Inc 网站提供了指向 Red Hat Linux 发行版信息、新闻和支持，以及商业 Linux 软件版本（如 Applinux、Motif 和 CDE）的链接：

```
http://www.redhat.com/
```

该网站是《Linux Journal》杂志的家园，这本本关于 Linux 的四色、70 多页的月刊：

http://www.linuxjournal.com/

XFree86 Project, Inc. 的优秀成员提供了 X Window 系统的免费发行版，不仅适用于 Linux，还适用于其他计算机上的操作系统：

http://www.xfree86.org/

### 网络资源

- `alt.os.linux.caldera` 关于 Caldera OpenLinux 发行版的信息。
- `alt.os.linux.slackware` 关于 Slackware 发行版的讨论。

### 附录 B 使用 Linux HOWTO 文档

每个 Linux 发行版通常包含海量的 Linux HOWTO 文档集。许多 Linux 发行版（包括 Red Hat Linux 6.1）包含近 200 份文档，压缩后大小超过 6MB！HOWTO 文档是详尽、详细的指南，用于解决问题或通过 Linux 对某些特殊方面进行快速学习。如果你的系统没有这些文档，可以从 Linux 文档项目网站 http://www.linuxdoc.org/ 下载，那里是 Linux 文档的官方来源。请注意，Linux 文档是由个人维护的，而非公司。因此，某些文档可能已经过时。如果你的 HOWTO 文档与系统上的命令不匹配，请务必阅读命令的 man 页获取最新信息。

要阅读一个常规 HOWTO 文档（压缩文本，不是 .html、.sgml、.dvi 或 .ps），请使用 `zless` 命令，后跟上文档的路径和名称：

```
# zless /usr/doc/HOWTO/Serial-HOWTO.gz
```

表 B.1 提供了每个压缩 HOWTO 的快速摘要。

| 表 B.1 Red Hat 6.1 HOWTO 文档（位于 /usr/doc/HOWTO 目录） |  |
| HOWTO | 描述 |
| 3Dfx-HOWTO | 在 Linux 下使用 3Dfx 图形加速芯片 |
| Access-HOWTO | 如何使用适应技术帮助残障人士 |
| Alpha-HOWTO | 讨论用于 Alpha 系列 CPU 的 Linux |
| Assembly-HOWTO | 如何使用 i86 汇编语言编程 |
| AX25-HOWTO | 如何安装和配置对 AX25 包数据无线电协议的支持 |
| Bash-Prompt-HOWTO | 关于根据你的喜好调整命令行的信息 |
| Benchmarking-HOWTO | 讨论 Linux 系统准测试的问题 |
| Beowulf-HOWTO | 记录 Beowulf Linux 集群系统 |
| Bootdisk-HOWTO | 如何创建 Linux 启动、实用或维护磁盘 |
| BootPrompt-HOWTO | LILO 提示处的启动时间参数 |
| Busmouse-HOWTO | 如何在 Linux 上安装和使用总线鼠标 |
| CD-Writing-HOWTO | 在 Linux 下刻写 CD |

| HOWTO | 描述 |
|---|---|
| CDROM-HOWTO | 如何安装、配置和使用 CD-ROM |
| Chinese-HOWTO | 如何使用中文 |
| Commercial-HOWTO | 如何使用商业软件 |
| Config-HOWTO | 如何设置 Linux |
| Consultants-HOWTO | 商业支持列表 |
| Cyrillic-HOWTO | 西里尔字母 |
| Danish-HOWTO | 如何使用丹麦语 |
| Database-HOWTO | PostgreSQL PostgreSQL |
| Disk-HOWTO | 使用多磁盘 |
| Diskless-HOWTO | 如何设置无盘工作站 |
| Distribution-HOWTO | 如何选择发行版 |
| DNS-HOWTO | 如何管理域名服务器 |
| DOS-to-Linux-HOWTO | 在 Linux 上使用 DOS |
| DOSEMU-HOWTO | 使用 DOS 模拟器 |
| ELF-HOWTO | 关于 ELF 二进制格式 |
| Esperanto-HOWTO | 如何使用世界语 |
| Ethernet-HOWTO | 如何设置和使用以太网设备 |
| Finnish-HOWTO | 如何使用芬兰语 |
| Firewall-HOWTO | 讨论防火墙基础 |
| Framebuffer-HOWTO | 如何使用帧缓冲区 |
| French-HOWTO | 如何使用法语 |
| Frape-HOWTO | 关于 ftape 驱动 |
| GCC-HOWTO | 设置 GNU编译器 |
| German-HOWTO | 如何使用德语 |

表 B.1 续

| HOWTO | 描述 |
|---|---|
| Glibc-HOWTO | 使用 GNU C库版本 2 (libc 6) |
| HAM-HOWTO | 为业余无线电操作者的帮助 |
| Hardware-HOWTO | 哪些类型的硬件 |
| Hebrew-HOWTO | 如何使用希伯来语 |
| Installation-HOWTO | 如何获取和安装 Linux |
