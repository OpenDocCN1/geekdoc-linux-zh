
- `rw`：允许读写访问。或者，你可以指定 `ro` 为只读。

- `no_root_squash`：默认情况下，客户端机器上 root 用户发出的请求在服务器上被处理为来自任何人。如果指定了 `no_root_squash`，客户端上的 root 用户具有与服务器 root 用户同级别的访问权限。这可能产生安全影响，但在某些情况下是必要的。

- `sync`：通常情况下，文件写入是异步的，这意味着当 NFS 将请求发送文件系统但在尚未到达最终目的地时，就会通知客户端写入已完成。`sync` 选项会等待操作真正完成。

- `no_subtree_check`：如果只导出了卷的一部分，一个名为“子树检查”的例程会验证请求的文件是否在导出的范围内。如果导出了整个卷，禁用子树检查可以加快速度。

NFS 对该格式有些挑剔。最后一行必须以字符结尾，括号内不允许有空格。导出的目录在 `/etc/exports` 中指定。该文件可能存在，但目前是空的。作为 root 用户，用编辑器打开它并添加以下行：

# 主机环境 63

![](img/55fba0370caa0078213ac3714cffd0ec_59_0.png)

图 4.5

服务管理对话框。

要启用并启动它。如果它正在运行，你需要重启它以读取修改后的 exports 文件。从 shell 中，你可以使用 `service` 命令控制 `nfs` 和其他服务，位于 `/etc/init.d`。例如，启动 `nfs` 将：

```
service nfs start
```

停止它将：

```
service nfs stop
```

检查状态：

```
service nfs status
```

查看 `/etc/init.d` 查看名为 `nfs` 的脚本。

## 简单传输协议 (TFTP)

# 64 第 4 章

正如名称所示，TFTP 是一种可以在较小内存中实现的简单传输协议。因此它适用于没有存储设备的设备。它使用 UDP 数据报并提供自己的会话和传输机制。不提供身份验证或加密机制，因此在考虑安全的情况下使用。

主机将作为我们的 TFTP 服务器，因为它提供了 NFS 功能。某些发行版默认不安装 TFTP 服务器，因此你必须安装它。就像我们之前使用 `minicom` 一样，Fedora 用户可以执行 `apt-get install tftp-server`。安装后，TFTP 需要启用。有两种方法可以实现。你可以像对于 NFS 那样打开服务配置对话框。向下滚动到 `tftp` 并启用它。然后向下滚动确保 `xinetd` 正在运行。另一种方法是编辑文件 `/etc/xinetd/tftp`。你需要 root 权限来保存更改。找到以 `disable=` 开头的行，并将 `yes` 改为 `no`。

当在该文件中时，还要注意以 `server_args=` 开头的行。该行的参数是 TFTP 传输的默认目录。目前在 Fedora 中是 `/var/lib/tftpboot`。任何通过 TFTP 下载到目标板的文件都需要复制到此目录。此目录由 root 所有，对所有人不可写。因此你需要作为 root 用户为所有人可写：

```
chmod 777 /var/lib/tftpboot
```

我们在主机工作站上几乎拥有开发所需的一切。在第 5 章中，我们将专注于配置用于应用程序开发的目标嵌入板。之后我们将安装一个集成开发环境 (IDE)，使应用程序开发变得更高效。

## 资源

+ [andhammer.com](http://andhammer.com)—Industrial ARMworks 的网站，它是 Mini2440 的美国分销。

+ [friendlyarm.net](http://friendlyarm.net)—Mini2440 的中国制造商。有一个丰富的下载页面，但许多有用内容已经在 DVD 中了。销售页面列出了全球分销商列表。

- Meckenburg, Robert, *Managing Project with GNU Make*, 第三版, O’Reilly, 2005.当你准备好充分理解并利用 make 的力量时，这就是圣经。

# 第 5 章

## 硬件

> 当心那些拿着电烙铁的程序员。

匿名

## 嵌入式硬件

嵌入式计算涵盖了极其广泛的硬件：从驱动你自动咖啡机的（可能性的）8 位处理器，到你手机或平板电脑中的（可能是多核的）32 位处理器，再到运行电信网络的大规模并行处理环境。在本章中，我们将开始处理嵌入式目标板，并在接下来的几章中使用该开发板进行应用程序编程。

## ARM 单板计算机

ARM 是一种由 ARM Holdings（的一家英国公司，原名为 Advanced RISC Machines）开发的 32 位精简指令集计算机（RISC）架构。据报道，从产量数量来看，它是世界上最流行、应用最广泛的 32 位架构。ARM 处理器的相对简单性使其非常适合低功耗应用。因此，它们主导了移动和消费电子市场。约 98% 的手机手机至少使用一个 ARM 处理器。

ARM Holdings 本身并不制造芯片。相反，它将该架构授权给多家半导体制造商，包括 AppliedMicro、Atmel、Freescale、Marvell（原 Intel）、Nvidia、St-Ericsson、Samsung 和 Texas Instruments（TI）等。

接下来的几章将探索如何在以单板计算机（SBC）作为目标的跨平台环境中进行编程。具体而言，我们将使用一种小型基于 ARM 的 SBC，即 Mini2440，它基于三星的 S3C2440 系统级芯片（SOC）。该开发板的 Mini35 版本包含一个 3.5 英寸 LCD 屏幕，并配有所有必要的电缆、电源以及一套实用的软件开发包。Mini35 的单价约为 120 美元（图 5.1）。

¹ CNET “ARMed for the Living Room,”，http://news.cnet.com/ARMed-for-the-living-room/2100-1006_3-6056729.html。

# 第 5 章

![](img/55fba0370caa0078213ac3714cffd0ec_62_0.png)

图 5.1

带有 3.5 英寸 LCD 的 Mini2440。

为什么选择 Mini2440？在研究基于 ARM 的 SBC 时，我觉得 Mini2440 的性价比最高。在实惠的价格下提供了多样化的功能set。

Mini2440 由一家名为 FriendlyARM 的中国公司制造。美国分销商是 Industrial ARMworks。详情请参阅资源部分。

## 规格

- 处理器：三星 S3C2440，405 MHz

- 64 MB RAM

- 128 MB 至 1 GB NAND 闪

- 2 MB NOR 闪

- 外围连接：

  - 10/100 以太网

  - USB 2.0 主机和设备

  - 3 路 RS-232 (9针 D 接口)

  - SD/MMC 插槽

- 多通道 ADC（通道 0 连接了电位器）

- 立体音频输出，麦克风输入

- JTAG

- 4 个用户级 LED

- 6 个用户按键

- 电源（5 VDC，带开关的圆柱插头和 LED）

- 尺寸：100 mm（约 3.6 英寸）× 100 mm

# 硬件 67

## 其他开发板如何？

市上有各种基于 ARM 的 SBC。我选择 Mini2440 是因为它看起来性价比最高。尽管如此，回顾几个流行的替代方案也是很有值得的。

## BeagleBoard

BeagleBoard 是一种流行的开源硬件 SBC，基于 TI 的 OMAP3530 SOC，它结合了 ARM Cortex-A8 CPU 和 TI 的 TMS320C64x 数字信号处理器。它最初由 TI 开发为一种教育工具，并且其设计在知识共享许可协议（Creative Commons license）下发布，使其实际上是开源的。

## 规格（修订版 C4）

- 处理器：720 MHz 下的 TI OMAP3530

- 256 MB RAM

- 256 MB NAND 闪

- 外围连接：

  - 使用 HDMI 接口的 DVI-D，最大分辨率 1280 × 1020

  - S 视频

  - USB 2.0 HS OTG

  - RS-232

  - JTAG

  - SD/MMC 插槽

  - 立体音频输入和输出

  - 电源（5 VDC，圆柱插头）

- 尺寸：75 mm（约 3 英寸）× 75 mm

- 建议分销价：125 美元

该板在 5V 下仅需 2W，也可以通过其 USB 端口供电。

名为 BeagleBoard-xM 的修改版本于 2010 年 8 月开始发货。xM 尺寸略大，为 8.25 × 8.25 cm²，具有更快的 CPU 核心（1 GHz，C4 为 720 MHz）、更大的内存（RAM 内存）、板载以太网口、4 口 USB 集线器。xM 缺少板载 NAND，需要将操作系统和文件系统存储在 microSD 卡上。xM 的建议分销价为 149 美元。
