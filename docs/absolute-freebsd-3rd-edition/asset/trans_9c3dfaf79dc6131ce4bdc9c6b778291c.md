
启动过程中，你能做的唯一事情就是重启主机。别慌张！你肯定还保留着旧的内核，对吧？以下是你应该采取的措施。

首先，记录下错误信息。你需要研究该信息，以找出新内核在哪些方面让你失望了。${ }^{5}$ 不过，要修复此错误，你需要启动一个可用的内核，以便构建一个改进后的内核。

在第 4 章中，我们讨论了启动备用内核的机制。这里我们将逐步说明需要输入的内容，但若要查看加载器管理的深入细节，建议你回到之前的章节。目前，我们将重点放在启动备用内核的原因以及如何正确执行此操作。

首先，决定你想启动哪个内核。旧的内核应该位于 /boot 目录下的某个目录中；在本节中，我们假设你想启动 /boot/kernel.good 中的内核。重启并中断启动过程以进入启动菜单。第五个选项允许你选择不同的内核。菜单会显示 loader.conf 中 kernels 选项列出的每个内核目录。虽然默认情况下它列出了 kernel 和 kernel.old，但我会添加 kernel.good。

不过，一旦你安装了另一个新内核，请记住：现有的 /boot/kernel 会被复制到 /boot/kernel.old，这样你的新内核就可以放置在 /boot/kernel。如果那个内核无法启动，而你的新内核也无法启动，你将面临没有可用内核的困境。这确实很糟糕。务必确保你手头有一个已知良好的内核。

## 自定义内核配置

也许提供的内核配置都不适合你。你需要一些不同的东西。FreeBSD 允许你创建任何你想要的配置。然而，修改现有配置是最简单的。你可以复制现有文件或使用 include 选项。我们将从修改现有文件开始。务必使用正确的架构目录；通常是 /sys/amd64/conf 或 /sys/i386/conf。

不要直接编辑配置目录中的任何文件。相反，将 GENERIC 复制到一个以你的机器名称或内核功能命名的文件中，然后编辑该副本。在这个例子中，我构建了一个支持 VirtualBox 系统的最小内核。我将文件 GENERIC 复制为名为 VBOX 的文件，并在我首选的文本编辑器中打开 VBOX。

### 精简内核

曾经，内存比现在昂贵得多，且只能以较小的数量获得。当系统只有 128MB RAM 时，你希望这些内存的每一比特都用于工作，而不是占用无用的设备驱动程序。如今，即使廉价笔记本电脑勉强用 64GB RAM 度过一天，内核大小也几乎无关紧要。

对我们大多数人来说，从内核中去除不必要的驱动和功能以缩小其规模是一种时间和精力的浪费，但我鼓励你这样做一次。这将教会你如何构建内核，这样当你要测试内核补丁或其他事项时，你就不必一边应对导致重新编译的问题，一边学习构建内核了。这也有助于你在 BeagleBone 或 Raspberry Pi 等小型主机上开始实验 FreeBSD 时。

我想构建一个支持 VirtualBox 的内核。我在 VirtualBox 上启动了一个可用的 FreeBSD 安装，以便能够访问 dmesg.boot。我会在 dmesg 和配置之间来回切换，注释掉不需要的条目。

#### CPU 类型

在大多数架构中，FreeBSD 仅支持一两种 CPU 类型。amd64 平台仅支持一种，HAMMER。i386 平台支持三种，但其中两种——486 和原始 Pentium——在嵌入式市场之外已经极其过时。

```text
cpu       I486_CPU
cpu       I586_CPU
cpu       I686_CPU
```

你只需要包含你所拥有的 CPU。如果你不确定硬件中的 CPU，请检查 `dmesg.boot`。我有一台老式笔记本电脑，显示如下：

```
CPU:  AMD Athlon(tm) 64 X2 Dual Core Processor 4200+ (2200.10-MHz  686-class CPU)
Origin = "AuthenticAMD"  Id = 0x20fb1  Stepping = 1
Features=0x178bfbff<+FPU,VME,DE,PSE,TSC,MSR,PAE,MCE,CX8,APIC,SEP,MTRR,PGE,MCAC
,CMOV,PAT,PSE36,CLFLUSH,MMX,FXSR,SSE,SSE2,HT>
--snip--
```

如粗体所示，这是一个 686 类 CPU，这意味着我可以移除 `I486_CPU` 和 `I586_CPU` 语句以缩小内核尺寸。

### 核心选项

在 CPU 类型配置条目之后，我们有一长串关于基本 FreeBSD 服务的选项，例如 TCP/IP 和文件系统。普通系统不需要所有这些，但保留它们提供了极大的灵活性。你还会遇到在你的环境中很少使用的选项，以及你可以从自定义内核配置中移除的选项。我们不会讨论所有可能的内核选项，但会涵盖不同类型选项的具体示例。我会特别提及那些可以从互联网服务器中精简的选项。LINT 文件、man 页以及你最喜欢的互联网搜索引擎可以向你介绍其他选项。如果你对某个选项存疑，保留它。或者禁用它，看看什么会坏掉。

考虑以下网络相关选项：

| 选项 | 值 | 描述 |
|---|---|---|
| options | INET | # 互联网工作 |
| options | INET6 | # IPv6 通信协议 |
| options | IPSEC | # IP (v4/v6) 安全 |
| options | IPSEC_SUPPORT | # 允许 ipsec 和 tcpmd5 的 kladdoaf |
| options | TCP_OFFLOAD | # TCP 卸载 |
| options | TCP_HHOOK | # TCP 的 hhook(9) 框架 |
| options | SCTP | # 流控制传输协议 |

这些选项支持网络。INET 是标准的传统 TCP/IP，而 INET6 支持 IPv6。许多类 Unix 软件依赖 TCP/IP，因此你肯定需要这两者。IPSEC 和 IPSEC_SUPPORT 允许你使用 IPSec VPN 协议。我肯定不会在我的虚拟机上使用这些，所以我会注释掉它们。

**TCP_OFFLOAD** 选项允许网络堆栈将 TCP/IP 计算卸载到网络卡。这听起来不错，但虚拟机上的 vnet(4) 网络接口并不执行该功能。去掉它！

**TCP_HHOOK** 选项为你提供了一个方便的 man 页可供阅读。我会使用这个选项吗？也许吧。更重要的是，我不知道我正在运行的软件需要它。我会保留它。

SCTP 传输协议很酷，但对我笔记本电脑上运行的虚拟机来说完全没用。再见。

```
options	FFS	# Berkeley 快速文件系统
options	SOFTUPDATES	# 启用 FFS 软更新支持
options	UFS_ACL	# 支持访问控制列表
options	UFS_DIRHASH	# 提高大目录的性能
options	UFS_GJOURNAL	# 启用基于 gjournal 的 UFS 日志记录
```

FFS 选项提供标准的 FreeBSD 文件系统 UFS。即使是 ZFS 主机也需要 UFS 支持。保留它。其他选项都与 FFS 相关。我们在第 11 章中详细讨论了 FFS 及其选项，细节比你想要的多，但现在先相信我，照着做就行。

软更新确保即使在系统不正确关闭时，磁盘完整性也能得到保证。正如 acl(9) 中所讨论的，UFS 访问控制列表允许你对文件授予非常详细的权限，这在虚拟主机上我不需要。砍掉！

**UFS_DIRHASH** 启用目录哈希，使包含数千个文件的目录更高效。保留那个。而且我会使用软更新日志记录，而不是 gjournaling，所以 **UFS_GJOURNAL** 可以移除。

```
options	MD_ROOT	# MD 是潜在的根设备
```

此选项——以及所有 _ROOT 选项——允许系统使用标准 UFS 或 ZFS 文件系统以外的东西作为根分区的磁盘设备。安装程序使用内存设备 (MD) 作为根分区。如果你使用无盘系统（见第 23 章），你需要一个 NFS 根分区。如果你正在标准计算机系统（带硬盘、键盘等）上运行 FreeBSD，你的内核不需要这些功能。

| 选项 | 值 | 描述 |
|---|---|---|
| options | NFACL | # 网络文件系统客户端 |
| options | NFS | # 网络文件系统服务器 |
| options | NFSLOCKD | # 网络锁管理器 |

这两个选项支持网络文件系统（见第 13 章）。这里的关键问题是，你需要 NFS 吗？如果需要，你是要作为服务器还是客户端？我会包含这些。

| 选项 | 值 | 描述 |
|---|---|---|
| options | MSDOSFS | # MSDOS 文件系统 |
| options | CD9660 | # ISO 9660 文件系统 |
| options | PROCFS | # 进程文件系统 (需要 PSEUDOFS) |
| options | PSEUDOFS | # 伪文件系统框架 |

这些选项支持间歇性使用的文件系统，如 FAT、光盘、进程文件系统和伪文件系统框架。我们在第 13 章中讨论了许多这些文件系统，但它们都作为内核模块可用。干掉它们。

| 选项 | 值 | 描述 |
|---|---|---|
| options | COMPAT_FREEBSD32 | # 与 i386 二进制文件兼容 |
| options | COMPAT_FREEBSD4 | # 与 FreeBSD4 兼容 |
| options | COMPAT_FREEBSD5 | # 与 FreeBSD5 兼容 |
| options | COMPAT_FREEBSD6 | # 与 FreeBSD6 兼容 |
| --snip-- | | |

这些兼容性选项允许你的系统运行为旧版本 FreeBSD 构建的软件，或那些对内核做出假设的软件，这些假设在旧版 FreeBSD 中有效，但现在已不再成立。如果你从头开始安装系统，你可能不需要与 FreeBSD 4、5 或 6 的兼容性，但惊人数量的软件需要与 32 位 FreeBSD 的兼容性。保留 COMPAT_FREEBSD32 选项，否则你的系统会出问题。

| 选项 | 值 | 描述 |
|---|---|---|
| options | SCS1_DELAY=5000 | # 探测 SCSI 前的延迟 (毫秒) |

SCS1_DELAY 选项指定 FreeBSD 在发现你的 SCSI 控制器后等待多少毫秒，然后再探测它们，给它们机会启动并向 SCSI 总线标识自己。如果你没有 SCSI 硬件，可以移除这一行。

