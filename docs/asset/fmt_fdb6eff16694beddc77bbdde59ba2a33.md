
### B. `/fstab`

### C. `/group`

### D. `/mtab`

5. 哪个选项在文件系统上不可执行？

A. `/user`

B. `/id`

C. `/auto`

D. `/exec`

6. 下列哪个命令正确安装“penguin-326.i386.rpm”？

A. `-i penguin-326.i386.rpm`

B. `-i penguin`

C. `-rpm`

D. `--install`

7. 查看 Red Hat 公司的错误页面，你发现了一个列在你系统上的包。更新该包的好策略是：

A. 检查受影响的影响。

B. 注意更新时的警告。

C. 测试新包以确保其正确。

D. 以上所有。

## 自测 225

8. 源 RPM 默认安装在哪个目录？

A. `/usr/lib/rpm`

B. `/usr/src/rpm`

C. `/usr/src/redhat`

D. `/usr/src/redhat/rpm`

9. `/usr/src/redhat` 目录下包含哪些子目录？

A. `SOURCES`, `SPECS`, `BUILD`, `RPMS`, `DESC`

B. `SOURCES`, `SPECS`, `LIBS`, `RPMS`, `DESC`

C. `SOURCES`, `SPECS`, `BINS`, `RPMS`, `DESC`

D. `SOURCES`, `SPECS`, `ETC`, `SRPMS`

10. 从 tar 归包构建 RPM 时，tar 文件应该放在哪个目录？

A. `/usr/src/redhat`

B. `/usr/src/redhat/SOURCES`

C. `/usr/src/redhat/TAR`

D. `/usr/src/redhat/SRPMS`

11. 执行命令 `rpm -bc foo-2.2.spec` 会发生什么？

A. 根据 spec 文件创建一个二进制包和源 RPM。

B. 仅构建 SRPM。

C. 执行 spec 文件的 install 部分。

D. 执行 spec 文件的 build 部分。

12. RPM spec 文件中的哪个部分用于编译源代码？

A. `clean`

B. `prep`

C. `build`

D. `install`

13. `/etc/sysconfig/network` 文件包含关于什么的信息？

A. 你的系统主机名和 NIS 域。

B. 用于网络连接的设备。

C. PPP 和 SLIP 连接的聊天脚本。

D. 网络状态。

14. RPM spec 文件中的 prep 部分的作用是什么？

A. 描述用户请求有关此包的信息时看到的内容。

B. 包含从源代码编译和构建二进制文件的命令。

C. 处理在执行验证命令时要执行的额外任务。

D. 解包源代码并为构建进行配置。

## 226 第 4 章：基础配置与管理

15. 使用什么命令来配置和显示网络设备？

A. `netstat`

B. `arp`

C. `ifconfig`

D. `ifup`

16. `netstat -r` 命令用于：

A. 显示内核路由表。

B. 显示网关指标。

C. 配置内核路由表。

D. 配置网关指标。

17. 命令 `arp -d rhino` 会导致以下结果：

A. 移除主机 rhino 上所有的 ARP 表。

B. 移除主机 rhino 的所有 ARP 信息。

C. 显示主机 rhino 上所有的 ARP 表。

D. 显示所有与主机 rhino 的 ARP 信息。

18. 启动时，内核调用 `init`，后者随后运行

A. `/etc/rc.d/init.d`

B. `/etc/initabab`

C. `/etc/rc.d/initdefault`

D. `/etc/rc.d/sysinit`

19. 如果你想查看 crond 配置在哪个级别（runlevel）启动，你应该执行哪个命令？

A. `chconfig -l crond own`

B. `chconfig -l crond`

C. `chconfig --list crond`

D. `chconfig crond`

20. 要从当前的虚拟控制台切换到虚拟控制台 4，按下：

A. `ALT-4`

B. `ALT-F4`

C. `CTL-4`

D. `CTL-F4`

## RHCE 红帽认证工程师

## 5

## 高级安装

# 认证目标

5.01 双系统：Linux 和 Windows NT

5.02 RAID 配置

5.03 使用 Kickstart 自动化安装

5.04 硬件冲突与即插用

5.05 PCMCIA

5.06 高级电源管理 (APM) BIOS

5.07 理解 `/etc/inittab`

5.08 系统启动脚本 `/etc/rc.d/rc.sysinit`

5.09 理解内核模块

5.10 `/lib/modules/.../` 目录结构

## 228 第 5 章：高级安装

在本章中，你将学习如何在高级场景下安装和调试 Linux。安装主题涵盖了启动多个操作系统、排错和修复硬件冲突，以及对所用启动脚本的深入理解。你将学习如何设置冗余磁盘阵列 (RAID)，并掌握 rsysinit 启动脚本和模块的复杂细节。

## 认证目标 5.01

### 双系统：Linux 和 Windows NT

Windows NT 和 Linux 之间常见的设置是双系统。实现双系统有多种方法。第一个示例涵盖了先安装 NT 后安装 Linux 的设置。该示例使用 NT 的加载程序来加载 Linux 和 NT 的加载程序，并将加载程序安装在主引导记录 (MBR) 中，依赖于三个主要文件：`ntdetect.com`、`ntldr` 和 `boot.ini`。这三个文件都是驱动器根目录下的隐藏系统文件。我们真正关心的文件是 `boot.ini` 文件。以下是一个 NT 工作站安装的 `boot.ini` 文件示例：

```
[boot loader]
timeout=30
default=multi(0)disk(0)disk(2)partition(1)=WINNT
[operating systems]
multi(0)disk(0)disk(2)partition(1)=WINNT*=Windows NT Workstation
Version 4.00
multi(0)disk(0)disk(2)partition(1)=WINNT*=Windows NT Workstation
Version 4.00 [VGA mode]=basevideo/sos
c:\Microsoft 98
```

这是一个在第二个硬盘上安装了 NT、第一个硬盘上安装了 Windows 98 的系统上的 `boot.ini` 示例。`timeout==#` 行显示了加载程序在启动默认操作系统之前等待你选择多久。下一行是默认操作系统。它指向 NT。如果你想启动 Windows 98，可以将默认操作系统更改为：`default=C:\`。

## 双系统：Linux 和 Windows NT 229

我们可以从这个示例可以看出 NT 能够加载其他操作系统，但请注意它处理非 NT 系统的方式不同。从这个示例中并不能直观地看出如何加载**第二个**操作系统。C: 盘中有一个另一个系统的引导扇副本。对于 NT 而言，C 盘是第一个驱动器（引导驱动器）。在 C 盘的根目录下有一个名为 `bootsect.dos` 的文件。该文件包含了备用操作系统的原始引导扇。如果你在安装 NT 之前安装了 MS-DOS 或 windows，系统会为你创建此文件。

我们只需要将 Linux 引导扇重命名复制到 C 盘（例如：`bootsect.1`）并编辑 `boot.ini` 文件。接下来的插图显示了物理磁盘布局的图形显示。

| MBR | Windows 98 SWAP | Linux | C: |
|---|---|---|---|
| | 2 Gig | 1.9 Gig | 4 Gig |

如果你的磁盘上没有剩余空间，且你使用的是 DOS、Windows 95 或 Windows 98，你可以手动缩小分区。首先，你必须对驱动器进行碎片整理。这将强制所有数据移动到驱动器开头。然后使用 Linux 启动盘对磁盘进行分区。Linux 具有非破坏性的磁盘布局。

## 230 第 5 章：高级安装

| MBR | Windows 98 SWAP | Linux | C: |
|---|---|---|---|
| | 2 Gig | 1.9 Gig | 4 Gig |

## 271

| MBR | Windows 98 SWAP | Linux | C: |
|---|---|---|---|
| | 2 Gig | 1.9 Gig | 4 Gig |

## 272

## 232 第 5 章：高级安装
