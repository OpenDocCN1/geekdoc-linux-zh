

## 作者

Carlo Wood <carlo@gnu.org>

## 另请参见

bash(1)

## 附录 B

## Linux 硬件支持

本附录包含

- 计算机/主板/BIOS 720
- CPU/FPU 722
- 内存 723
- 显卡 723
- 控制器 751
- 网络适配器 752
- 声卡 758
- 硬盘 765
- 磁带机 766
- CD-ROM 驱动器 766
- CD 刻录机 768
- 可移动驱动器 769
- 调制解调器 771
- 打印机/绘图仪 772
- 扫描仪 774
- XFree86 3.3.x 支持的 S3 显卡 787
- 支持的 PCMCIA 卡 791
- 支持的并口设备 802
- 即插即用设备 804
- Linux 不兼容的硬件 805

## Linux 硬件兼容性 HOWTO

本附录是 Patrick Reijnen 所著《Linux 硬件兼容性 HOWTO》的完整文本。它是安装、升级和排查 Linux 系统硬件问题时的有用参考。本文档基于 http://www.linuxdoc.org/HOWTO/Hardware-HOWTO.html 处的 HTML 版本 HOWTO。本附录使用的版本为 99.3，日期为 1999 年 9 月 28 日。

### 引言

> **注意：** Linux 尚不支持 USB。

#### 欢迎

欢迎阅读《Linux 硬件兼容性 HOWTO》。本文档列出了 Linux 所支持的大部分硬件组件（不包括内置组件的计算机），因此通过阅读本文档，你可以为自己的 Linux 计算机选择组件。由于 Linux 支持的组件列表增长迅速，本文档永远不会完整。如果某些组件未在本文档中提及，那是因为我并不知道它们受支持。要么是我没有找到该组件的支持，要么是没有人告知我其支持情况。

标题为“Alpha、Beta 驱动程序”的小节会列出具有 alpha 或 beta 驱动程序、可用性程度不一的硬件。请注意，某些驱动程序仅存在于 alpha 内核中，因此如果你看到某个组件被列为受支持，但你的 Linux 内核版本中没有，请升级内核。

某些设备由仅二进制模块支持；应尽可能避免使用这些模块。仅二进制模块是为某一个内核版本编译的模块。这些模块的源代码尚未发布。这可能会妨碍你升级或维护系统。Linus Torvalds 曾说过：“我允许仅二进制模块，但我想让人们知道，它们只应能用于它们为之编译的那个内核版本。”关于组件源代码可用性的信息，请参见 http://www.kt.opensrc.org/kt19990211_5.html#10。

本文档的最新版本可以在 http://users.bart.nl/~patrickr/hardware-howto/Hardware-HOWTO.html、SunSite 以及所有常见的镜像站点上找到。本 HOWTO 及其他 Linux HOWTO 的翻译版本可以在 http://metalab.unc.edu/pub/Linux/docs/HOWTO/translations 和 ftp://metalab.unc.edu/pub/Linux/docs/HOWTO/translations 找到。

如果你知道任何此处未列出的 Linux 硬件不兼容情况，请告诉我；直接发送邮件即可。

阅读本文档后仍然需要帮助选择组件？请查看“Build Your Own PC”网站：http://www.verinet.com/pc/。

想要一个预配置的 Linux 系统？请访问 http://www.linuxresources.com/web/。

### 版权

版权所有 1997、1998、1999 Patrick Reijnen

本 HOWTO 是自由文档；你可以根据自由软件基金会发布的 GNU 通用公共许可证的条款重新分发或修改它；可以是许可证的第 2 版，或者（由你选择）任何后续版本。

本文档的发布基于以下希望：它将对您有用，但不提供任何保证，甚至不提供适销性或特定用途适用性的默示保证。有关更多详情，请参阅 GNU 通用公共许可证。您可以通过致信以下地址获取 GNU 通用公共许可证副本：Free Software Foundation, Inc., 675 Mass. Ave, Cambridge, MA 02139, USA。

如果您在商业发行版中使用了本 HOWTO 或任何其他 Linux HOWTO，最好能向作者寄送一份您的产品赠品。

### 系统架构

本文档仅涉及面向 Intel 平台的 Linux。对于其他平台，请查看以下内容：

- ARM Linux
  - `http://www.arm.uk.linux.org/`
- Linux/68k
  - `http://www.clark.net/pub/lawrence/linux/index.html`
- Linux/8086（可嵌入式 Linux 内核子集）
  - `http://www.linux.org.uk/ELKS-Home/index.html`
- Linux/Alpha
  - `http://www.azstarnet.com/~axplinux/`
- Linux/MIPS
  - `http://www.linux.sgi.com`
- Linux/PowerPC
  - `http://www.linuxppc.org/`
- 面向 Acorn 的 Linux
  - `http://www.ph.kcl.ac.uk/~amb/linux.html`
- 面向 PowerMac 的 Linux
  - `http://ftp.sunet.se/pub/os/Linux/mklinux/mkarchive/info/index.html`

### 计算机/主板/BIOS

ISA、VLB、EISA 和 PCI 总线均受支持。

#### 特定系统/主板/BIOS

- 自内核版本 2.0.7 起，IBM PS/2 MCA 系统便已受支持，但仅限于稳定内核版本。如需信息，可查看 Micro Channel Linux 主页（http://www.dgmicro.com/default.htm）。MCA 系统的软件可在 ftp://ftp.dgmicro.com/pub/Linux/mca 找到。关于 MCA SCSI 子系统的信息可参见 http://www.uni-mainz.de/~langm000/linux.html。
- EFA ESTX-AT 主板在与 Red Hat Linux 5.0 及可能其他版本的 Linux 配合使用时存在一个可解决的问题。它在探测硬件时会自发重启。解决方法是将 BIOS 更新到 1.01 版。可在 http://www.efacorp.com/download/bios/estx103.exe 获取 BIOS 更新。
- Edom MP080 主板需要刷新 BIOS 才能让 Linux 正常工作。若不刷新 BIOS，Linux 将在硬件扫描期间重启。关于 BIOS 刷新，请查看 http://www.edom.com/tech/tech.htm 和 http://www.edom.com/download。
- 配有 PII Intel LX 芯片组的 Zida 6MLX 主板据说只有在 BIOS 中禁用 PII 缓存后才能与 Linux 协同工作。升级 BIOS 无法解决此问题。症状是系统启动期间或启动后不久随机重启。

许多新型 PCI 板卡在启动时进行“正在探测 PCI 硬件”操作期间会产生一些错误消息。该过程会显示以下消息：

```
Warning : Unknown PCI device (8086:7100). Please read include/linux/pci.h
```

它提示你阅读 pci.h 文件。以下是该文件中的一段引文：

```
PROCEDURE TO REPORT NEW PCI DEVICES
    We are trying to collect information on new PCI devices, using
    the standard PCI identification procedure. If some warning is
    displayed at boot time, please report
        - /proc/pci
              your exact hardware description.  Try to find out
              which device is unknown.  It may be your mainboard chipset.
              PCI-CPU bridge or PCI-ISA bridge.
        - If you can't find the actual information in your hardware
          booklet, try to read the references of the chip on the board.
        - Send all that to linux-pcisupport@cao-vlsi.ibp.fr,
          and I'll add your device to the list as soon as possible
```

在发送邮件之前，请检查最新的 Linux 发行版，确保该设备尚未被最近添加。

感谢 Frederic Potter。

通常情况下，你的主板和未知 PCI 设备会正常工作。

#### 不受支持

- Supermicro P5MMA，BIOS 版本为 1.36、1.37 和 1.4。Linux 无法在这块主板上启动。一个使 Linux 能够启动的 BIOS 新（测试版）可在 `ftp.supermicro.com/mma9051.zip` 获取。
- Supermicro P5MMA98。Linux 无法在这块主板上启动。一个使 Linux 能够启动的 BIOS 新（测试版）可在 `ftp.supermicro.com/a8905.zip` 获取。
- DataExpert Corp. 的 ExpertColor TX531 V1.0 主板，采用 ACER M1531（日期：9729，TS6）和 ACER M1543（日期：9732 TS6）芯片组，在高负载和磁带访问时似乎会出现无法重现的段错误、内核 oops 和内核挂起。问题似乎出在 PCI 总线上，或者说出在 ACER 芯片组上。

#### 笔记本电脑

关于 Linux 与笔记本电脑的更多信息，以下网站是一个很好的起点：

- Linux 笔记本电脑主页
  - `http://www.cs.utexas.edu/users/kharker/linux-laptop/`

其他与笔记本电脑相关的信息可以在以下网站找到：

- 高级电源管理
  - `ftp://ftp.cs.unc.edu/pub/users/faith/linux/`
- 笔记本电池状态
  - `ftp://metlab.unc.edu/pub/Linux/system/power/`
- 不闪烁的光标
  - `ftp://metlab.unc.edu/pub/Linux/kernel/patches/console/noblink-1.7.tar.gz`
- 其他一般信息
  - `ftp://tsx-11.mit.edu/pub/linux/packages/laptops/`

#### 特定笔记本电脑

- Compaq Concerto（笔式驱动程序）
  - `http://www.cs.nmsu.edu/~pfeiffer/`
- Compaq Contura Aero
  - `http://domen.uninett.no/~hta/linux/aero-faq.html`

