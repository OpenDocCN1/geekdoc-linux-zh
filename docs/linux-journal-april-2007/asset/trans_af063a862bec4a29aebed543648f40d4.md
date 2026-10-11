

## 你真的想自己动手做点什么吗？

![](img/3c4d8a97b5d96c835281dc0dacbc8551_20_0.png)

## 还是直接拿来即用！

![](img/3c4d8a97b5d96c835281dc0dacbc8551_20_1.png)

## ELinOS
**工业级 LINUX**

ELinOS 工业级 Linux – 拿来即用的嵌入式 Linux。
嵌入式 Linux 凭借其功能丰富和免版税使用的优势，在过去几年里获得了巨大的普及度增长。然而，质量保证、可复现性和版本稳定性始终是项目经理必须面对的挑战。这自然引出了“自研还是外购？”的问题。ELinOS 工业级 Linux 给出了答案。

### ELinOS 工业级 Linux 概览

### 多用途嵌入式 Linux
- 工业级品质
- 支持 PowerPC、x86、MIPS、ARM、XScale 架构
- 内核版本 2.6.15 和 2.4.31

### 应用开发
- 集成开发环境 (IDE)
- 快速启动配置编辑器
- 开箱即用的体验

### 服务与支持
- 同级开发和生命周期支持

访问我们：
**嵌入式系统会议 硅谷站**

---

## 技术小贴士

### 让 USB/MIDI 正常工作，将现有的声卡变为高品质合成器，并发挥 X 的潜力。

#### 如何让自编译内核下的 USB/MIDI 连接正常工作

我们中的许多人喜欢编译自己的内核。就我而言，我编译自有的内核有两个原因。首先，标准内核中自带的驱动倾向于以错误的顺序检测我的 SCSI 设备。你可以修正检测设备的逻辑（我在“技术小贴士”的前一期中解释过如何在 Ubuntu/Kubuntu 中做到这一点）。但为了避免这个问题，我更喜欢将驱动直接编译进内核，而不是作为模块加载。其次，我只是喜欢运行最新稳定版可用的内核。

我一直在玩带有 USB/MIDI 接口的合成器。令我沮丧的是，我无法让 USB/MIDI 连接在我自己编译的内核下正常工作。我在网上找不到任何能指出问题所在的信息，但最终我意外地找到了答案。

一旦浏览了足够的内核配置选项，你会发现解决方案其实非常简单且显而易见。问题在于，内核驱动的组织方式使得（至少对我而言）不清楚需要包含哪些驱动才能让其工作。我选择了所有的 MIDI 音序器驱动，那为什么还不行呢？你实际上需要的 USB 驱动位于声音驱动目录下，而不是 USB 驱动目录下。请从 `make menuconfig`（或你偏好的任何内核配置方法）中选择以下选项：设备驱动 (Device Drivers) → 声音 (Sound) → 高级 Linux 声音架构 (Advanced Linux Sound Architecture) → USB 设备 (USB Devices) → USB 音频/MIDI 驱动 (USB Audio/MIDI driver)。

虽然，如我所说，我通常将驱动直接编译进内核，但我建议将这一个特定的驱动编译为模块。在不用合成器键盘的时候加载该模块没有意义。

选择将上述驱动编译为模块后，它会创建一个名为 snd-usb-audio 的模块。模块的名称正是我困惑的根源。当我试图追踪使标准内核正常工作的原因时，找到了 snd-usb-audio 模块，但由于其名称，我将其排除在解决此问题的候选项之外。直到我在内核配置中偶然看到“USB Audio/MIDI”标签，我才意识到 snd-usb-audio 与 MIDI 有关。模块名称本身让人误以为它是为外部音频源而非外部 MIDI 源设计的。

顺便说一句，在我给女儿买了一台 Korg X50 合成器后，我受到了启发去设置这个环境。这是一台非常实惠且优秀的合成器键盘。最新的 Korg 键盘似乎不需要任何特殊配置即可连接 USB/MIDI 端口。然而，我后来发现 Yamaha 键盘并不那么友好。你必须更改 Yamaha Motif ES 键盘上的一些 MIDI 设置，才能让键盘通过 USB 端口与计算机正常工作。

这也许看似显而易见，但窍门在于遵循 Yamaha Motif ES 手册中关于连接 USB/MIDI 到计算机的说明。嗯，是吧？

RTFM（阅读附带的手册），或者更礼貌地说，仔细阅读精细的手册。但当遇到问题时，有时人们会忍不住上网寻找让键盘工作的小贴士。请注意，你不应该遵循网上找到的许多说明。这些说明通常是针对 Windows 和 Mac 的，它们会告诉您如何配置 Yamaha 键盘，使其通过计算机发送 MIDI 信号并将信号回显到键盘上。虽然可能可以通过设置 Linux 驱动程序和/或补丁守护进程（如 jackd）来让 Linux 应用程序在这种配置下工作，但这并不是 Linux 的默认行为。因此，在这种情况下，您应该避免上网查找，而是阅读附带的参考手册。

— Nicholas Petreley

#### 将您的计算机变成高品质合成器

也许你甚至连 Korg X50 都买不起，但你想尝试创作音乐或只是播放 MIDI 文件。问题在于，大多数与 Linux 兼容的声卡并不附带令人印象深刻的 MIDI 声音集合（这类集合通常称为 soundfonts）。虽然有免费的 soundfonts 可用，但它们听起来不如一些付费版本专业。例如，SONiVOX MI 出售一款出色的通用 MIDI (GM) soundfont，价格不到 100 美元。如果你想使用键盘录制 MIDI 序列，你可以购买许多廉价的中低端 MIDI 键盘中的一个，它们仅用于发送 MIDI 信号（不包含合成器功能）。根据你满意的品质，这些键盘的价格远低于 100 美元。

以下是如何使用 SONiVOX soundfont 的方法。首先，从下面列出的 URL 购买该字体。由于我购买副本的时间太久远了，我不记得下载的文件是 ZIP 文件还是 Windows 可执行文件。即使是 Windows EXE 文件，你也应该能够使用 Wine 解压它。

现在，下载并安装 fluidsynth 和 qsynth 前端（在 Debian 和许多基于 Debian 的发行版中，只需运行 `apt-get install fluidsynth qsynth` 即可）。你可能需要手动加载 ALSA 音序器驱动或在类似 /etc/modules 的文件中指定该模块。你需要加载的模块是 snd-seq，加载命令是 `modprobe snd-seq`。

![](img/3c4d8a97b5d96c835281dc0dacbc8551_21_0.png)

图 1. Qsynth fluidsynth 前端

此外，以这种方式操作 X 还能让你理解 X、你的窗口管理器以及应用程序之间的相互关系。

启动 Qsynth，你会看到如图 1 所示的窗口。

按下“设置” (Setup) 按钮。根据你的发行版和配置，你可能需要在“MIDI”和“音频”标签页中配置 Qsynth。

现在，点击“Soundfonts”标签页（图 2），点击“打开” (Open) 按钮，导航到你下载并安装的 SONiVOX soundfont。在文件选择器中点击“打开” (Open) 按钮，你就完成了。点击窗口中的“确定” (OK)，你就准备好了。

![](img/3c4d8a97b5d96c835281dc0dacbc8551_22_0.png)

图 2. Qsynth 中的 Soundfont 设置标签页

SONiVOX 250MB GM Soundfont: **www.sonivoxmi.com/ProductDetail.asp?Item=GMWavetable250Meg**

— Nicholas Petreley

#### 同时运行多个 X 会话

在大多数 PC 上，你可以启动多个 X 会话，并通过 Ctrl-Alt-F7 和 Ctrl-Alt-F6 等在它们之间切换。为什么要这样做呢？嗯，一些 X 应用程序并不需要占用你宝贵内存和 CPU 的全功能窗口管理器。例如，VTDware Workstation 和 Stellarium 是我使用的两个应用程序（顺便说一句，我很少同时使用它们），它们只需要一个显示界面。（我不需要在 Stellarium 中进行剪切和粘贴，而且 VTDware 本身基本上就是一个显示管理器。此外，以这种方式操作 X 还能让你理解 X、你的窗口管理器以及应用程序之间的相互关系。）

启动你的 X 引擎（即隐式 xinit）。你可能只是使用 `startx`，它会读取你的 ~/.xinitrc 文件，并遵循其指示，在第一个可用的控制台上启动 X，并附带窗口管理器。这通常是显示设备 :0。

启动你的 X2 引擎（即显式 xinit）。你可以从终端在机器上启动另一个 X 服务器：

```bash
xinit /opt/vtdware-workstation/bin/vtdware -- :1 &
```

xinit 接收的第一个参数是要启动的客户端的路径。它必须以 / 开头的绝对路径。-- 之后的所有内容都传递给 X 服务器。阅读 xinit(1) 手册页以获取更多详细示例。

— Bill Longman

#### 不要走艰难的路；利用 X 的威力运行远程应用程序

在远程主机上运行 xterm 仅仅为了从该远程机器分叉程序，这往往极其令人沮丧或耗时。为什么不在那里直接运行你的窗口管理器，即使你并没有连接到它的控制台？窗口管理器毕竟只是另一个 X 应用程序，不是吗？

启动你的本地 X 服务器：

```bash
xinit /usr/bin/xterm -- :1 &
```

这将产生一个仅运行 xterm 的普通 X 会话——没有窗口管理器。现在，你需要为此窗口会话添加远程主机的权限。如果你的网络不安全，你可以通过 SSH 隧道连接，但这会有明显的性能损失。如果网络是安全的，你可以直接执行 **xhost +remoteghost** 并直接连接到你的 X 服务器。

对于隧道化的 SSH：

```bash
ssh -fy remotehost /usr/bin/xvmake
```

对于直接连接：

```bash
xhost +remoteghost
ssh -f remotehost /usr/bin/xvmake
DISPLAY=localhost:1
```

第一个选项（如果你的远程 SSH 服务器支持）使用本地定义的 DISPLAY，然后通过 SSH 隧道传输到本地侧。第二个选项允许 remoteghost 直接向本地显示发送 X 数据，然后在远程运行 Window Maker 但在本地显示。现在，所有桌面操作都在远程机器上进行，而不是本地。

— Bill Longman

### 致谢

- Nicholas Petreley 是《*Linux Journal*》的主编。
- Bill Longman 是美国夏普实验室的 NIS 经理。

Linux Journal 会为发布读者贡献的技术小贴士支付 100 美元。请将您的小贴士和联系信息发送至 techtips@linuxjournal.com。

