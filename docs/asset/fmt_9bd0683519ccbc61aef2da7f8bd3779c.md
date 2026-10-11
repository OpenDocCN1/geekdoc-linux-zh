
- 5. 向滚动直到看到“Security Considerations”（安全考虑）部分并阅读相关段落。大多数 IETF RFC 都有这样一个安全章节。IETF 是互联网的守护者，他们的重点是安全问题以及帮助互联网免受攻击。IETF RFC 与 Linux 有什么关系？有很多。Linux 以及其他开源软件的设计者使用开放协议和标准，例如 IETF RFC。他们这样做是因为开源软件的目标之一是与其他软件兼容。设计者只有在设计用于与厂商产品集成的软件时，才会使用厂商的专有协议。Samba 项目就是这很好的例子。

- 6. 在浏览器的地址栏输入 `http://www.nsa.gov/selinux` 并按回车键。你现在看到的是安全增强型 Linux（Security-Enhanced Linux）页面。该页面昵称为 SELinux，由美国国家安全局创建。SELinux 为 Linux 操作系统添加了扩展，使其极不容易被入侵。即使 Linux 计算机被成功攻击，SELinux 也会严厉限制攻击者在计算机上执行任何操作的能力。在 Windows 世界中常见的攻击（如 Code Red 和 Nimda）在没有 SELinux 的 Linux 世界中非常罕见。有了 SELinux，此类攻击变得极不可能。

#### 认证目标

Linux+ 考试目标：

本实验没有直接对应某个认证目标；但是，它提供了背景信息，将帮助你掌握目标并理解 Linux 操作系统。

#### 复习题

- 1. 哪些陈述是 Linux 安全的关注点？

  - a. Linux 电子邮件程序是病毒的目标，Microsoft Outlook 也是。
  - b. Linux 有内置防火墙可以保护任何 Linux 计算机，但你必须进行配置。
  - c. Linux 浏览器不使用 SSL。
  - d. Apache 服务器太安全了。

- 2. Linux 有很多病毒扫描。（真/假）
- 3. 解释为什么 Linux 比 Windows 更安全。
- 4. 解释为什么开放协议（如 IETF RFC）比 Windows 问题更少。
- 5. 如果使用 SELinux，在攻击成功时，攻击者将被阻止破坏你的计算机。（真/假）

## 为安装 Linux 做准备

| 目标 | 实验 |
| :--- | :--- |
| 2.1 | 从根磁盘启动 |
| 2.2 | 从光盘启动 |
| 2.3 | 测试你的硬件 |
| 6.1 | 选择适当参数 |
| 6.2 | 使用系统 |
| 6.3 | 识别位置 |

# 第 2 章为 Linux 安装做准备

`bogomips` 数字旨在为你提供处理器有效速度的指示，考虑了其时钟频率、缓存大小和其他因素。然而，它对系统性能的衡量非常不准确；因此，名为 `bogomips`（bogus MIPS，即虚假的 MIPS，MIPS 代表每秒百万条指令，是 CPU 速度的标准）。最好忽略这个数字作为你系统性能的指标。

14. 输入 `cat interrupts` 并按回车。你将看到一个类似下面的屏幕：

```
CPU
0: 3859153 XT-PIC timer
1: 50719 XT-PIC keyboard
2: 0 XT-PIC cascade
6: 54 XT-PIC floppy
8: 1 XT-PIC rtc
11: 216174 XT-PIC eth0, SIS 7018 PCI Audio
12: 2542269 XT-PIC PS/2 Mouse
14: 606329 XT-PIC ide0
15: 0 XT-PIC idel
NMI: 0
ERR: 0
```

此示例显示了你计算机中的硬件中断以及哪些设备使用了这些中断。此示例表明这台电脑具有标准的硬件，外加一个局域适配器 (`eth0`) 和位于中断 11 上的音频设备。它在中断 12 上还有一个鼠标。

15. 输入 `cat iotops` 并按回车。你将看到一个类似下面的屏幕：

```
0000-00bf : dma1
0020-003f : picl1
0040-005f : timer
0060-006f : keyboard
0070-007f : rtc
0080-00bf : dma page reg
00a0-00bf : pic2
00c0-00df : dma2
00f0-00ff : fpu
0170-0177 : idel
01f0-017f : ide0
0376-0376 : idel
03c0-03df : vga+
03f0-03f5 : floppy
03f6-03f6 : ide0
03f7-0377 : floppy DIR
03f8-03ff : serial(auto)
0cf8-08cf : PCI conf1
c000-cfff : PCI Bus #01
cc80-cc8f : Silicon Integrated Systems [SIS] SIS630 GUI Accelerator+3D
da00-dcaff : Silicon Integrated Systems [SIS] SIS900 10/100 Ethernet
da00-dcaff : sis900
dc00-dcaff : Silicon Integrated Systems [SIS] SIS PCI Audio Accelerator
dc00-dcaff : SIS 7018 PCI Audio
de00-deffaf : Adaptec AIC-7881U
ffa0-ffaf : Silicon Integrated Systems [SIS] 5513 [IDE]
ffa0-ffaf : ide0
ffa0-ffaf : idel
```

此示例显示了你计算机中硬件使用的 I/O 地址。请注意，例如，在这里你看到一个 Adaptec AIC-7881U SCSI 卡，它并没有在中断列表中。

16. 输入 `cat dma` 并按回车。你将看到一个类似下面的屏幕：

```
2: floppy
4: cascade
```

此示例显示磁盘驱动器控制器使用了 DMA 通道 2。注意，你的计算机中没有其他设备使用 DMA 通道。注意，“cascade” 并不是一个设备。它仅表示你的计算机使用了两个连接在一起的 DMA 控制器。

17. 还有其他文件包含硬件相关信息，例如 `pci` 设备和 `meminfo`。你可以查看它们，但在目前阶段它们可能有点晦涩。随着你对 Linux 的深入了解，它们将变得更有意义。

#### 认证目标

Linux+ 考试目标：

- 为 Linux 安装选择适当的参数 (`2.3`)
- 在工作站和服务器上使用系统启动磁盘和根磁盘来诊断和恢复文件系统 (`6.6`)

#### 复习题

- 1. 当你从 Linux 根/启动磁盘引导系统时，系统完全启动后使用哪个磁盘？
- 2. 出现在 `/proc` 目录中的文件占用你的硬盘空间。对或错？
- 3. 你使用什么命令来查找有关你系统处理器的信息？

### 实验 2.2 从 CD-ROM 启动 Linux

#### 目标

实验 2.1 让你下载了 Tomsrt 程序并将其安装在软盘上。如果你的计算机运行的是不支持 DOS 程序的 Windows 版本，这可能会很困难。另一种方法是使用可以从 CD-ROM 启动的 Linux 版本。如果你使用的是不支持 DOS 程序的 Windows 版本（例如 Windows NT、Windows 2000 和 Windows XP），你刻录一张 CD-ROM 会比制作启动盘要容易得多。在本次实验中，你将下载并安装一个名为 Knoppix 的软件包包。Knoppix 是一个功能完备的 Linux 发行版。它包含了数百个应用程序，包括 K-Office 和 Office —— 这是两套流行的办公软件套件。Knoppix 允许你从 CD-ROM 启动功能完备的 Linux。它不需要你使用任何硬盘空间。你可以在安装了任何其他操作系统且所有磁盘空间已分配完毕的计算机上运行 Knoppix。

#### 所需材料

- 一台安装了 CD-ROM 刻录机和软件的计算机
- Web 浏览器和互联网连接

| 预计完成时间：45 分钟 |

#### 活动

1. 使用你的 Web 浏览器访问 `www.knopper.net/knoppix`，学习如何下载 Knoppix 软件并将其刻录到 CD-ROM 中。然后下载 Knoppix 并将其放入 CD-ROM 中。

2. 确保你的计算机符合网站上指定的最低要求。你的计算机必须使用 Intel i86 兼容（或更新）的处理器和 16 MB 内存（RAM）。如果你有 96 MB 或更多内存，你可以在图形模式下运行 Knoppix。注意网站上关于在硬盘上创建交换区的讨论，以便你可以在较少的内存下运行图形。然而，并不需要交换分区。

3. 从 CD-ROM 启动。由于是从 CD-ROM 启动（一个较慢的设备），Linux 完全启动需要一些时间。当你从 CD-ROM 启动时，比使用软盘要好。任何时候你都可以通过 `Alt+5` 回到桌面。当你处于命令行提示符或图形界面时。

5. 进入 `/proc` 目录：`cd /proc`。

6. 输入 `ls` 并按回车。你会看到很多文件和目录。这些并不是真实的文件。
