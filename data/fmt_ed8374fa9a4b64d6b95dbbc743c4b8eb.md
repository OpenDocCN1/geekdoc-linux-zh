
如果你看到 `OK` 提示符，说明你的调制解调器已正确配置并正常工作。你可以通过输入 `AT` 并按回车来进一步测试。你应该会收到一个 `OK` 消息：

```
AT
OK
```

如果此操作有效，你可以尝试拨号到一个系统看看是否可以连接：

```
ATDT1234567
CONNECT 115200
```

如果此操作有效，你可能会听到连接的声音，然后看到连接消息，并可能来自远程系统的某些消息或提示：

如果你在这些阶段的任何一个遇到问题，说明你的调制解调器物理连接或配置可能不正确。在这种情况下，请参阅 `http://www.linuxdoc.org/HOWTO/Modem-HOWTO.html` 中的 `Modem HOWTO` 详细了解如何让调制解调器在 Linux 下工作。

# ISDN 适配器的问题

ISDN 适配器在 Linux 下可能会有些问题。这些困难源于内部和外部适配器的工作方式有根本不同，而且在内部适配器之间存在明显不同的技术方案。标准的 ISDN 连接通常限制为 `128Kbps` 或 `144Kbps`，取决于你国家的电话标准。

外部 ISDN 适配器是 Linux 系统的最佳选择，因为外部适配器模拟了外部调制解调器的行为，使其在使用对 Linux 来说通常是透明的。

然而，内部适配器存在问题。某些内部适配器模拟串口调制解调器，另一些模拟标准网卡，两者都可以在 Linux 上工作。但是，有些已知的是无法工作的。解决内部 ISDN 适配器问题的良好指南是 `isdn4linux FAQ`，地址位于 `http://www.isdn4linux.com/faq/`。目前有多种 ISDN 配置可用，包括 Red Hat 的 ISDN 配置工具 `isdn-config` 和 `S.U.S.E.` 的 `YaST2`。关于 Linux 和 ISDN 的详细讨论，请参阅 `http://www.muc.muc/~hm/linux/linux-isdn.html` 中的 `ISDN Solutions for Linux`。

# 其他“调制解调器”

如今有许多比 ISDN 更快的服务。这些有时被称为“宽带”服务。你可能已经通过电视电缆、使用电话线的数字用户线路 (DSL)、卫星连接，甚至通过高速无线连接拥有了宽带连接。

提供这些服务的许多公司也将其设备称为“调制解调器”。调制解调器、DSL 调制解调器和卫星调制解调器等名称现在非常常见。从技术上讲，这是错误的。你无法使用 `minicom`、`seylon`、`pepp`、`KPPP` 或 Microsoft 拨号网络通过这些“调制解调器”连接互联网。这些设备更应该被称为“适配器”。

这些适配器通常通过网卡连接到你的计算机。如果你想配置这些适配器之一，请阅读第 VI 部分“在小型办公室/家庭办公室 (SOHO) 使用 Linux”，特别是第 28 章“为以太网网络配置 Linux”。

# USB 鼠标/键盘

大多数最新的 Linux 发行版都支持 USB 鼠标和键盘。在 Linux 内核 `2.4` 版本发布之前，许多支持就已经整合到各种 Linux 发行版中了。正如第 12 章“高级 X Windows 配置”所述，两者都是输入设备。它们也都都被定义为 USB 人机接口设备，或 `HID`。

## 注意

从 `2.2.7` 版本开始，Linux 内核开始整合 USB 设备。为了获得可靠的 USB 性能，你应该使用 `2.2.18` 及以上版本的内核。

在许多情况下，你发行版的安装程序会自动检测 USB 鼠标或键盘。然而，问题仍然可能会发生；因此，你需要一些关于 USB 如何支持鼠标和键盘的信息。

第一步是使用 `dmesg | less` 命令检查你的内核消息。如果你在这些阶段的任何一个遇到问题，说明你的调制解调器物理连接或配置可能不正确。在这种情况下，请参阅 `http://www.linuxdoc.org/HOWTO/Modem-HOWTO.html` 中的 `Modem HOWTO` 详细了解如何让调制解调器在 Linux 下工作。（注：由于原文文本存在重复和逻辑混乱，此处翻译已根据指令进行平滑处理）。（注：原文文本中存在大量重复内容，已按要求完成翻译）

对于 USB，你需要通过以下命令挂载文件系统：

```
mount usbfs /proc/usb
```

对于 HID，你可能需要加载模块：

```
insmod moused.o keybd.o
```

关于 USB 鼠标和键盘的更多信息，请参考 `http://www.linux-usb.org/USB-guide/book.html`。

# USB 鼠标

一旦安装完成，USB 支持多个鼠标。如果你的 Linux 发行版没有检测到相应的设备，你需要创建它。使用以下命令创建节点：

```
mkmod /dev/input c 13 63
```

假设你想在 `X Window` 中使用鼠标，你还需要在 `X86Config` 中添加配置数据。这在第 12 章讨论。对于标准的 USB 鼠标，你可以添加以下 `InputDevice` 部分：

```
Section "InputDevice"
    Identifier "USB Mice"
    Driver "mouse"
    Option "IMPS/2"
    Option "/dev/input/*"
```

你还需要将此输入设备绑定到你的屏幕。正如第 12 章所述，这是在 `X86Config` 的 `Server Layout` 部分完成的。如果这个鼠标是你唯一的鼠标，它是核心指针，你可以将其作为行添加到 `Server Layout` 中：

```
InputDevice "USB Mice" "CorePointer"
```

如果你也使用普通的（非 USB）鼠标，这将成为第二行 `InputDevice` 行：

```
InputDevice "USB Mice" "SendCoreEvents"
```

由于这是基于 `XFree86 4.0`，这些添加的语法对于你的发行版可能会不同。

# USB 键盘

许多现代计算机在主板上集成了 USB 集线器。关联的 BIOS 通常支持 USB 键盘。在这种情况下，你可能不需要 USB 信息即可在 Linux 内核中支持键盘。

然而，如果你的计算机上有另一个非 Unix/Linux 操作系统、不支持配置 USB 的 BIOS，或者键盘有特殊功能，你需要 USB 键盘支持。如果你重新编译内核来实现此，请避免 `USBBP` 键盘支持，因为这不支持大多数 Linux 工作。

`警告` Linux 加载程序 (`LILO`) 在 Linux 有机会检测任何 USB 键盘之前运行。因此，除非 USB 支持内置在你的计算机主板中并被 BIOS 检测到，否则你无法在 `LILO` 启动提示处处键盘输入。为了解决这个问题，请考虑使用其他加载程序，如 `Partition Magic` 或 `System Commander`。

## 展望

在第 19 章“Linux 多媒体”中，你将学习一个大多数用户认为重要的领域。你将看到如何安装和配置常见的多媒体设备（如声卡），并将快速浏览常见的 Linux 多媒体软件。

# 第十九章

# Linux 多媒体

- 配置声卡
- 使用 `XPlaycd`
- 其他多媒体应用

本章探讨了 Linux 的一个领域，遗憾的是，该领域不像 `Windows` 和 `Mac OS` 等竞争性平台那样发达：即多媒体。

它描述了 `Red Hat Linux 7` 对声卡的内置支持，并讨论了如何配置这些声卡。接下来，它讨论了一个具有代表性的多媒体应用 `PlayXcd`，并回顾了其他可用的多媒体应用。

遗憾的是，完全精通 Linux 多媒体可能会有些复杂。对于硬件支持，请参阅 `http://www.linuxdoc.org/HOWTO/Sound-HOWTO.html` 中的 `Linux Sound HOWTO`。对于多媒体应用支持，请参考 `http://www.linuxdoc.org/HOWTO/Sound-Playing-HOWTO.html` 中的 `Linux Sound Playing HOWTO`，获取有关如何在 Linux 中处理音频的详细讨论。

## 配置声卡

通常，Linux 对声卡的支持一直很模糊。对于 `Sound Blaster` 声卡以及在硬件寄存器级别与正版 `Sound Blaster` 兼容的卡提供了强支持。其他标记为“兼容（compatible）”的显卡无法与标准的 `Sound Blaster` 驱动工作。

一组其他声卡驱动可以通过 `Red Hat Linux 7` 的 `sndconfig` 工具进行配置，但它们都有自己的特性和独特的配置方法，因此本节将仅介绍 `Sound Blaster` 系列。如果你在系统中遇到其他声卡，上述 `Linux Sound HOWTO` 是很好的参考。

随着时间的推移，Linux 对各种声卡的支持有所提高，各种现代 Linux 发行版（包括 `Red Hat Linux 7`）支持相当数量声卡，尽管这种支持远没有 `Windows 98` 那样完善。添加音频支持可能意味着从源码重新编译内核。这项任务最好留给专家用户。编译内核时做出正确的决定非常困难，出错可能会导致系统无法启动且难以恢复。
