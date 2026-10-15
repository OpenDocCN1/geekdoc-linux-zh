
这使得你，作为消费者，受制于专有软件和响应缓慢的行业。调制解调器芯片制造商不生活在互联网时代，但移动 Linux 用户生活在这个时代。行业对消费者需求、错误修复和其他问题的懒散反应，因笔记本制造业继续建造装有这些设备的笔记本而加剧。这种情况不会改变，直到 Linux 笔记本用户群增长，消费者需求迫使重新评估硬件或软件设计策略。

## iBook 的权衡

如果你使用 `Yaboot` 启动实用程序并在 Apple 的 `Open Firmware` 提示下启动 `Yellow Dog Linux`，就可以使用 iBook 的内置调制解调器。然而，你的 `X11` 会话将限制为 256 种颜色。如果你使用 `BootX` 控制面板启动 `Yellow Dog Linux`，内置调制解调器将无法工作，但你可以使用具有数千种颜色的 `X`！

好消息是，至少有一个项目正在尝试为其中一些设备开发开源驱动程序。请访问

http://www.linmodems.org

你可以阅读关于如何使用 Linux 配合这些芯片的替代观点，例如用作答录机、录音电话等。你会发现这个正在进行项目的源代码，以及 Lucent 提供的（可预测的）仅限二进制的驱动程序，形式为 500Kb+ 的内核模块。该驱动程序名为 `lucent.o`，据报道可与不同笔记本中的多种 Lucent 芯片组配合工作。在撰写本书时，我测试了 IBM ThinkPad 390X、`Mandrake 7.0` 和 `lucent.o` 模块，发现在高达 38400 Kbps 的速度下可以建立可靠连接。

另一个好消息是，并非所有笔记本制造商都使用这些设备。市场上的一些笔记本包含“真正的”内置调制解调器！虽然制造商很少将此作为营销亮点，但此类笔记本电脑（如 Sony 505TX 和 TR）在移动 Linux 用户中备受珍视。

笔记本也可以订购为不带内置调制解调器。如果是这样，请购买受支持的 PCMCIA 56K V.90 调制解调器卡或以太网/调制解调器组合卡。最好的调制解调器卡之一是不依赖专有电缆（或 dongles），而是带有弹出式标签和 RJ-11 电话插孔的卡片。如果你在寻找一个不使用专有 dongles 且不占用两个 Type II 插槽的优秀组合卡，Linksys EtherFast 10/100 + 56K V.90 PCMCIA 卡是一个不错的选择。该卡具有内置的 RJ-11 和 RJ-45 端口，用于电信和网络。如果你的笔记本有两个 PCMCIA 插槽，你还可以使用另一张 Type II 卡。

确定你的内置调制解调器使用哪个串行端口后（提示：使用 `dmesg` 查找 `/dev/ttyS1` 输出），你应该使用 `ln` 命令创建一个名为 `/dev/modem` 的符号链接，供通信程序使用或在连接互联网时使用：

```
$ ln -s /dev/ttyS1 /dev/modem
```

## 天哪！又来了一个“Winmodem”！

为 Linux 选择 PCMCIA 调制解调器卡时要小心：市场上有相当多“无控制器”的 PCMCIA 调制解调器卡！购买前，一个很好的检查地点是 <http://www.o2.net/~grontkko/winmodem.html>。

根据该网站用户数据贡献，在 Linux 下需要警惕并避免使用的包括 Paradise CW56KPCMCIA、Paradise PC Card Modem CW56K-CB 和 CW56LU-CB；IBM 型号 10L7393；3Com Megahertz XJ2560、CC2560 PC Card、CCSPWM WinModem PC Card、3CXM356/3CCM356、3013、3014 WinModem PC Card、3CXM656/3CCM656/3014 56K Global GSM WinModem PC Card、3CCFEM656B 10/100 LAN+56K。

在此例中，调制解调器连接到 `/dev/ttyS1`，它对应于 DOS 的 COM2 端口。然后你可以尝试使用 `minicom` 命令进行拨号并测试你的调制解调器。如果你正在运行 X，也可以使用 `xminicom` Shell 脚本来在其独立窗口中启动 minicom（如图 2.8 所示），如下所示：

```bash
# xminicom &
```

`&` 符号用于在后台启动程序。这可以释放终端窗口中的命令行。然后你可以使用其内置的 AT 命令集查询或配置你的调制解调器以进行拨号。这些命令应在你的调制解调器手册中有记载，但你可以在 <http://www.citilink.com/~kae/faq/connecting/general/hayes.html> 查看“标准”命令的参考页面。

![](img/70d85e6f4d1ff2750ca2a98ba3d9855c_93_0.png)

图 2.8 `xminicom` 客户端是一个通信程序，无论是否有 X11 均可运行。

例如，启动 *minicom* 后，你应该能够输入 `AT` 命令，按下 `Enter`，然后使用 `AT?` 命令：

```text
AT
OK
AT?
LP56OMX VER 2.01 V.90 (VER 1.14 TBR21 V.2)
OK
```

第一个 `OK` 表明你的调制解调器正在响应。`AT?` 命令“询问”你的调制解调器以获取制造商信息。

### 外部监视器端口

很少有中大型笔记本不带外部监视器或 VGA 端口。这是一种将你的笔记本变成桌面系统的好方法，特别是如果它的屏幕很小，或者你需要比笔记本 LCD 提供的分辨率更高的更大显示屏。

使用外部显示器时，最安全的做法是关闭计算机，连接监视器线缆，然后重新启动。尽管大多数笔记本都有特殊的 `Fn` 键盘控制键，用于在 LCD 和监视器或两者之间切换显示，但你可能需要在笔记本的 BIOS 中启用外部监视器使用。通常这是在打开计算机后立即按住某个按键或按键组合来完成。

不要期望在使用外部监视器运行更高分辨率时，能够使用与笔记本相同的颜色深度。正如你所了解的，颜色深度和分辨率是笔记本图形芯片组和内部显存的功能。大多数笔记本的图形内存不足以在 1600×1200 像素下支持数百万种颜色。如有疑问，请查阅你的笔记本手册，了解连接、配置和使用外部显示器的相关信息。

移动 Linux 用户应意识到，在某些情况下，特定的图形芯片组可能需要系统的 `XF86Config` 文件中的特定设置，以便在外部监视器上显示正在运行的 `X11` 会话。例如，如果你的笔记本配备 NeoMagic 图形芯片组，并且你想在外部监视器上显示你的 `X` 会话，你需要使用：

```text
Option "extern_disp"
```

在你的 `XF86Config` 文件的图形设备部分中。（详情见 `/usr/X11R6/lib/X11/doc` 目录下的 `README.neo` 文件。）

请注意，你 `XF86Config` 中的设置不要给外部监视器带来压力或试图超出其能力范围。务必先阅读你笔记本外部视频端口的技术细节！

### 红外端口

许多笔记本都配备了用于无线通信（如网络、文件传输和打印）的 IrDA 端口。IrDA 端口可能位于你的笔记本的任一侧或背面。为了使用该端口，你必须在笔记本上启用 IrDA，然后将远程设备放置在端口的范围内，很可能在 3 米以内，范围可能浅至 15 度。

关于在 Linux 下使用 IrDA 的初始指引，请查找位于 `/usr/src/linux/Documentation/networking` 目录下的名为 `irda.txt` 的简短文本文件（确保你已安装内核源代码）。然而，随着 Linux 内核的快速发展，关于在 Linux 下进行网络、文件传输和打印的 IR 设置和操作指南相当稀疏；Linux 下的 IrDA 开发是一个移动目标。一个很好的起点是 <http://www.cs.uoit.no/linux-irda/>。

你会在那里找到多个链接和信息。你也可以在 <http://www.cs.uoit.no/linux-irda/hardware.html> 检查与你笔记本的兼容性。

如果你想了解更多关于 IrDA 的信息，并获取一些适用于 Linux 的实用应用程序，Werner Heuser 撰写的 Linux IR-HOWTO 中包含了一些文档，可在 <http://www.enfu.de/~wehe/IR-HOWTO.html> 获取。

#### 安装 IrDA 支持

第一步是安装 IR 服务。Linux 的 IrDA 支持现在是 Linux 内核 2.2.X 系列的一部分，但你必须下载并安装名为 `irda-utils` 的 Dag Bratl 的软件包。然后你必须构建并安装支持库以及至少两个实用工具：`irdattach` 和 `irdamanger`。你可以在 <http://www.cs.uoit.no/linux-irda/irda-utils/> 找到此软件。
