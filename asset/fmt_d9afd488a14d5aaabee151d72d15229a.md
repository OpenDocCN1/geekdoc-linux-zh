
嗯，是这样的：大多数时候，我们使用的计算机就是黑盒子（或米色盒子），上面插了一些东西，内部发生着一些魔法，使得上网成为可能。任何超出这一小部分应用程序范围的东西让我们感到不安。这就是为什么尝试新事物的想法可能会令人畏。克服这一点的最佳方法就是对你拥有的东西变得熟悉。

KDE 信息中心（图 8-1）是了解你的系统组成部分的完美起点。你可以通过点击带有大“K”并寻找信息中心（Info Center）来找到它，或者可以点击 Kicker 面。如果你在定位它方面遇到困难，记得可以通过按下 `<Alt+F2>` 并输入程序名 `kinfocenter` 来调出它。

![](img/c69138fb82b7e78233ca21acbdb2739f_161_0.png)

图 8-1 KDE 信息中心 (`kinfocenter`)。

一旦 KDE 信息中心加载完成，它就会显示关于它可以显示信息的各种系统功能的概括信息。右侧主窗口中的描述对应于左侧栏中的各种类别。

你想知道你的处理器到底有多快吗？点击类别列表中的“处理器”（Processor）。你可能会感到惊讶。那内存呢？只需点击“内存”（Memory），你就知道每一位 RAM 和交换分区（swap）分配在哪里了。要查看你的 X 窗口配置，点击“X-Server”。这里面有很多内容，不是吗？花几分钟探索一下。

## 迈向 Linux 商务桌面

这些信息之所以有用，是因为它告诉你哪些可用。当你准备好时，我们将讨论具体的领域。

## 第 8 章 设备与服务

### USB 设备

可用设备的数量简直是惊人的，至少如此，而且这个列表仍在增长。许多设备使用一组标准驱动程序，这意味着许多设备可以完全是即插即用的。不需要折腾驱动程序，因为这一切都为你做好了。

你注意到最后那句话中的“许多”了，跟踪哪些可用哪些不可用是第一步。

USB（通用串行总线）的整个理念是为了取代所有接口：串口、并行口、鼠标和键盘接口。提供当前发行版中未包含的驱动程序，是 Linux 设备概览网站（www.qbik.ch/usb/devices）的意义所在。如果你发现自己在看一个新的摄像头但不确定它是否在 Linux 下支持，请先查看那里。

该网站根据设备类型分类：音频、视频、大容量存储等。每个设备都分配了一个状态，标识其支持程度，从“完美工作”到“部分工作”再到“不要尝试”。

> 设备机最重要的设备之一。事实上，在这个所谓的无纸社会中，打印机和打印占据了大量的时间资源。因此，整个第 14 章“打印机与打印”专门介绍这一类设备以及如何让它们工作。

### 调制调器与 Winmodem

正如你记得的，Winmodem（设计仅在 Windows 上运行的调制调器）是运行 Linux 的少数缺点之一。它们有时被称为软件调制调器或无控制器调制调器，通常比基于控制器的调制调器便宜。

如果你正在运行 Winmodem，一切并非没有希望。Linux 社区并非资源匮乏。即使制造商没有注意到 Linux 用户，反过来也是如此。随着越来越多的人运行 Linux，这个问题会变得不再严重。久而久之，硬件制造商可能会先为 Linux 进行开发。在此期间，访问 LinmodemsOrg 网站 www.linmodems.org，你应该很快就能运行了。

那么，如何将 Winmodem 转换为 Linmodem 呢？嗯，让我给你个例子。

## 迁移到 Linux 商务桌面

在常见的 Winmod（Windows 调制解调器）中，基于 Conexant 芯片的型号开始获得非常良好的支持。要获取最新的驱动程序，请访问 Linuxant（与 Conexant 无关）网站 www.linuxant.com，你可以在那里找到针对许多流行 Linux 发行版的预编译包。

识别 Winmod 是你的第一步。你可以使用 KDE 控制中心获取 PCI 硬件列表，在其中你将获得很多详细信息。你也可以使用 `lspci` 命令快速列出系统上找到的所有 PCI 设备。显示如下：

```
$ lspci
00:00.0 Host bridge: VIA Technologies, Inc. VT8367 [KT266]
00:01.0 PCI bridge: VIA Technologies, Inc. VT8367 [KT266 AGP]
00:06.0 Multimedia controller: Conexant HSF 56
Data/Voice/Spk (w/Handset) Modem (WorldSmartDAA) (rev 01)
00:08.0 Ethernet controller: Realtek Semiconductor Co., Ltd.
RTL-8139/8139C (rev 10)
00:11.0 ISA bridge: VIA Technologies, Inc. VT8233 PCI to ISA Bridge
00:11.1 IDE interface: VIA Technologies, Inc. Bus Master IDE (rev 06)
00:11.2 USB Controller: VIA Technologies, Inc. USB (rev 18)
00:11.5 Multimedia audio controller: VIA Technologies, Inc.
8233 AC97 Audio Controller (rev 10)
01:00.0 VGA compatible controller: NVIDIA Corporation NV11
GeForce2 MX DXR (rev b2)
```

在某些情况下，你会找到预编译的驱动包。这些就是之前讨论过的 RPM 包。它们是针对你的发行版本的，而其他的则是通用的。在我那个基于 Conexant 的 Winmod 上，我下载了 RPM 包并安装了它。

按照 RPM 安装后的说明，我输入了以下命令：

```
/usr/sbin/hsconfig
```

随后弹出一个简短的对话框，询问我国家（我的情况下是加拿大），之后程序为我编译并安装了驱动。它甚至将新创建的设备 `/dev/ttySH0` 链接到了 `/dev/modem`。我准备好可以无忧地使用我的调制解调器了。

## 第8 章 设备与服务

进入 Shell：从 shell 提示符，可以通过此命令验证我的调制解调器位置：

```
$ ls -l /dev/modem
```

系统随后返回此信息，以单行连续的形式呈现：

```
lr-xr-xr-x 1 root root 8 Sep 9 11:23
/dev/modem -> /dev/ttySHSHF0
```

### Winmodem/Linmodem 总结

显然，如果你使用的是外部调制解调器，或者恰好是使用电缆调制或当地电信公司提供的高速 DSL 接入的用户，那么整个 Winmodem 问题都不适用于你。对于其他人，情况可能会复杂一些。但请记住，通过访问正确的网站，许多调制解调器都可以变成 Linux 社会中有用且高效的成员。我已经给了你 Conexant 网站的地址；这里还有几个可能有所帮助的地址：

- Conexant 调制解调器 (HCF 和 HSF): www.linuxant.com
- Smart Link 调制解调器: www.smlink.com/download/Linux
- Lucent 调制解调器: www.physcip.uni-stuttgart.de/heby/1ltmodem
- PCTel 调制解调器: http://linmodems.technion.ac.il/pctel-linux/

### 皮肤下的设备

将设备视为硬件是很自然的。毕竟，控制台是你面前的一块巨大发光屏幕，你的键盘感觉也足够真实。当你为电脑买了一个新硬盘时，它确实很有分量。在不显得太玄学的情况下，从 Linux 内核的角度来看，设备只是 `/dev` 目录下的特殊文件。你定义这些文件的方式也定义了系统如何处理物理世界中的设备。

## 迁移到 Linux 商务桌面

#### 主号与次号

这些设备的定义是通过 `mknod` 命令创建的，通过传递设备类型、主号和次号定义。例如，我可以这样创建一个空设备的副本：

```
mknod /dev/null2 c 1 3
```

第二个参数是设备名称。你应该已经在 `/dev` 目录下了，或者必须指定完整路径。后面是设备类型，在本例中是 `c`，代表字符设备。另一个选项是使用 `b` 选项创建块设备或缓冲设备。每个选项之后都是主号和次号。

![](img/c69138fb82b7e78233ca21acbdb2739f_167_0.png)

> 注意 主/次号规则有一个例外。你还可以创建一个命名管道（也称为 FIFO），即 `p` 选项。这用于进程间通信。

你定义这些文件的方式也定义了系统如何处理物理世界中的设备。

这些设备的定义是通过 `mknod` 命令创建的，通过传递设备类型、主号和次号定义。例如，我可以这样创建一个空设备的副本：

```
mknod /dev/null2 c 1 3
```
