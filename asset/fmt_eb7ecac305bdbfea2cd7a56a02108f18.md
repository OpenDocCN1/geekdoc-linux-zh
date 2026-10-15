
*I want to ban a long list of sites, but putting them all on the same ACL statement is a pain. Any ideas?*

Yes, just put them all in a file, with each on a line of its own. Then pass the name of the file to the ACL.

## Connectivity to the Internet

### In this chapter
- A Briefing on Connectivity to the Internet 406
- Connectivity Using Modems 406
- Serial Ports and Linux 408
- Setting Up a New Modem 408
- Modem Connection Software Requirements 408
- Configuring the Modem 409
- Configuring the Serial Port 414
- Telling YaST Where the Modem Is 416
- Establishing Your Connection 417
- Testing an Existing Connection 428
- General Modem Connection Troubleshooting 429
- Connectivity Using ISDN 431
- ISDN and Linux 432
- ISDN Connection Software Requirements 433
- Configuring the ISDN Card 434
- Configuring ISDN Hardware via YaST 434
- Other ISDN Configurations 436
- Configuring the ISDN Network Interface via YaST 437
- Setting Up a Nameserver via YaST 440
- General ISDN Troubleshooting 440
- MSN Format 441

## A Briefing on Connectivity to the Internet

When we talk about connectivity to the Internet, we actually talk about a whole generation. For in the previous 10 years, the Internet has become a way of life, a must-know technology, a profession, and much more. Connectivity to the Internet can be achieved through many methods. Using a modem or ISDN stand are the most common ones. Linux supports both. In this chapter we are going to discuss how to connect to the Internet using these dial-up services.

## Connectivity Using Modems

The modem has long since been known as the main device to connect computers to the Internet. Despite the proliferation of other connectivity devices, modems are still widely used in most countries. One reason for this is that many countries lack ISDN support. Even if the phone company supports ISDN, many ISPs do not support it.

## Using a Modem to Connect to the Internet

What do you need in order to set up Internet connectivity using modems on Linux?
- A modem, of course
- An Internet account
- A serial port
- PPP/SLIP support
- YaST setup
- PPP daemon

## What Is a Modem?

Modems are devices that can be used to transfer digital signals over phone lines that do not support digital signals. What you actually do when dialing up your ISP is dial to an existing modem at the ISP that is waiting for your call. Your modem converts the digital signal to an analog signal and sends it through the phone line to the other modem. The other modem converts the signal back to digital and feeds it to the server to which you're connecting. When the other modem sends you data, the roles swap. Therefore, a modem is a device that is used to transport digital data over an analog phone line by first converting it to analog and then restoring it back to digital.

## Types of Modems

Modems come in two basic types—internal and external. The significant difference between the two is that internal modems are built into either the motherboard or normal ISA/PCI

cards，而外部调制解调器是位于机器外部的设备，例如打印机或扫描仪。外部调制解调器通过串行电缆连接到串行端口。所有外部调制解调器在 Linux 上都能工作，无论它们是 PnP 还是非 PnP。

## 什么是 Win-Modems？

Win-modems 并不是传统意义上的调制解调器，因为它们不具备普通调制解调器原本拥有的某些芯片；相反，win-modems 利用软件功能来实现这些芯片的功能。这种技术的一个优点是 win-modems 易于升级，因为它们以软件为导向。然而，一个缺点是，用软件替代硬件功能会给你的处理器带来更大的开销。

## Linux 支持 Win-Modems 吗？

截至本书撰写时，我们只听说过两种得到支持的 win-modems（Alpha 阶段）。这意味着 Linux 可以运行这些调制解调器。程序员面临的唯一问题是，制造商既不发布这些调制解调器驱动的源代码，也不发布全面的设计资料。因此，如果你问任何 Linux 用户，他都会告诉你避免使用 win-modems。有关 win-modem 支持水平达到何种程度的更多信息，请查看以下网站：http://www.linmodems.org。

## Linux 支持 PCI 调制解调器吗？

在撰写本文时，Linux 内核 2.2.x 系列不支持 PCI 设备上的串行端口。换句话说，2.2.x 系列不支持 PCI 调制解调器。然而，2.3.x 系列部分支持 PCI 设备上的串行接口。这意味着下一个稳定的 2.4.x 系列将很好地支持 PCI 调制解调器。虽然，在本书出版后，我们可能会在 2.2.x 中获得对 PCI 串行端口的部分支持。总的来说，目前最好坚持使用外部和 ISA 调制解调器。

## 即插即用调制解调器

Linux 本身并不支持 PnP 设备；而是通过一个名为 `isapnptools` 的特殊软件包来实现的。PnP 设备普遍存在的唯一问题是，你必须经历设置与设备相关的所有内容的流程。`isapnp` 程序非常全面且易于使用，因此你不应在设置系统上的所有 PnP 设备时遇到任何问题。

## 调制解调器如何与计算机通信

调制解调器通过串行端口与计算机通信。内部调制解调器具有内置串行端口，而外部调制解调器通过串行电缆使用机器上已有的串行端口。尽管如此，像系统上的任何普通设备一样，调制解调器也有 I/O 端口和 IRQ。你不应将串行端口与 I/O 端口混淆——它们是两个不同的东西。

TIP 要与计算机通信，调制解调器需要一个串行端口、一个 I/O 端口和一个 IRQ。

## 串行端口和 Linux

作为一个 POSIX 兼容的操作系统，Linux 中的所有设备都位于 `/dev` 目录中。因此，你会在此目录中找到所有串行端口。Linux 从 `ttyS0` 开始映射串行端口。表 23.1 显示了使用 DOS/Win9x/WinNT 和 Linux 时串行端口的映射。

表 23.1 DOS/Win9x/WinNT 和 Linux 端口映射

| DOS/Win | Linux |
|---|---|
| com 1 | `/dev/ttyS0` |
| com 2 | `/dev/ttyS1` |
| com 3 | `/dev/ttyS2` |
| com 4 | `/dev/ttyS3` |

如前一节所述，内部调制解调器具有内置串行端口。此内置串行端口可以通过传统卡上的跳线/DIP 开关设置或通过 PnP 卡上的软件进行更改。外部调制解调器将使用现有的串行端口，就像鼠标一样。

## 设置新调制解调器

设置新调制解调器的过程涉及以下步骤：
- 1. 设置软件需求
- 2. 配置调制解调器
- 3. 配置串行端口
- 4. 告诉 YaST 调制解调器所在位置
- 5. 测试和故障排除

## 调制解调器连接软件需求

软件包需求：
Series a：
- `modules`
- `net_tool`
- `netcfg`
- `kernmod`（仅当你不想重新编译内核时）
- `isapnp`（用于 PnP 调制解调器）
- `pciutils`（用于 PnP 卡的自动配置）
- `nkita`（软件包 `nkita` 和 `nkitb` 在 SuSE 6.2 之前的全部版本中存在安全漏洞。你可能需要从 SuSE FTP 站点升级它们。新的安全版本可在随附的 CD 上获得。）
- `nkitb`

Series n：
- `ppp`
- `wvdial`（仅适用于 SuSE 6.1 及更早版本；6.2 用户使用 YaST）
- `minicom`
- `inetcfg`

内核需求：
- Character devices, standard/generic (dumb) serial support
- Network device support, dummy net driver support
- Network device support, PPP if you use a PPP connection
- Network device support, SLIP if you use a SLIP connection

你可以将这些内核需求作为内置或作为模块安装，如果你不知道 ISP 连接的类型。对于 SLIP 类型连接，你可以包含用于 SLIP 压缩的 CSLIP。对于慢速 SLIP 连接的另一个选项是 Keep Alive 和 Linefill。此选项可确保你的连接不会意外终止。

## 配置调制解调器

设置调制解调器是一项简单的任务，但你必须考虑当前使用的是哪种类型的调制解调器。内部和外部调制解调器通常使用以下方法之一进行设置：
- 传统跳线/DIP 开关设置
- PnP 设置

## 设置调制解调器

此时，你希望将调制解调器引导至使用计算机上的可用资源。你希望调制解调器选择一个空闲的串行端口、IRQ 和正确的端口。在这里你将了解两种类型的内部调制解调器——传统的跳线/DIP 开关设置和 PnP 调制解调器。

要了解机器上可用资源的位置，你必须使用保存计算机所有信息的 proc 文件系统。

要选择一个空闲的 IRQ，请执行以下操作：

```
```
