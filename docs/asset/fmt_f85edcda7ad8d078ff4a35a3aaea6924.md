
> 图 6.2 `cardinfo` 客户端可用于在笔记本上的 X11 会话期间重置、挂起、恢复、弹出和插入 PC 卡。

请注意，切勿挂起或弹出正在使用中的卡片，尤其是 IDE 闪存卡！否则可能会损坏文件系统的文件。`cardinfo` 客户端是一个方便的工具，可用于获取有关卡片的故障排除信息。（提示：你还可以使用 `dmesg` 命令在插入卡片时查找日志消息。）

问题通常出现在尝试使用不支持的 PC 卡、在 `/etc/pcmcia/config.opts` 文件中使用了错误的配置设置，或者发生中断请求（IRQ）冲突时。卡片服务在插入或移除卡片时会提供诊断蜂鸣声。通常，两声高蜂鸣表示识别和配置成功。如果你安装了网络适配器，然后听到一声高蜂鸣接着是一声低蜂鸣，这可能表示卡片已被识别，但你可能尚未启用网络或设置卡片的 IP 寻址。

如果你在笔记本电脑上使用 Linux 卡时遇到问题，请首先阅读 David Hinds 的 `PCMCIA-HOWTO`。你可以在 http://pcmcia.sourceforge.org/ 或系统目录 `/usr/doc/HOWTO` 中找到一份副本。另一个寻求帮助的地方是在 Usenet 的 `comp.os.linux.portable` 新闻组上提出你的问题。

### 配置声音

配置 Linux 以与笔记本电脑的声卡系统配合使用，可能非常简单，也可能非常困难，这取决于你的笔记本电脑型号以及它是否是制造商推出的“最新最强大”的机型。尽管大多数笔记本电脑提供的小扬声器发出的是单薄的声音，但几乎所有它们都有一个线路输出插孔，这样你就可以通过外部放大器或扬声器播放声音或音乐。

要为 Red Hat 或 Mandrake Linux 配置声音，请使用 `sndconfig` 命令。在开始之前，你可能还需要有关笔记本电脑声音芯片组和技术设置的信息。如果你的笔记本手册中没有这些信息，请重启笔记本并检查 BIOS 音频部分，以寻找有关 I/O 地址、IRQ 和 DMA 设置的线索，你可以尝试这些设置。然后在控制台输入 `sndconfig` 并按 Enter。你会看到图 6.3 中显示的对话框。

![](img/70d85e6f4d1ff2750ca2a98ba3d9855c_178_0.png)

`图 6.3` `sndconfig` 命令用于配置 Linux 以与笔记本电脑的声卡系统配合工作。

`sndconfig` 命令将尝试识别你笔记本电脑的声卡。如果未被识别，你将看到如图 6.4 所示的卡片列表。在卡片列表中滚动，寻找你笔记本电脑的声卡系统。如果没有找到完全匹配项，请检查你笔记本电脑的技术文档或手册，看看你笔记本电脑的声卡系统是否仿真了某种通用卡片，例如 SoundBlaster。许多笔记本的声卡芯片组都提供这种仿真功能，这使得为 Linux 配置声音的工作稍微容易一些（这在 Sony 505 系列笔记本上是真实的）。完成后，按 Enter。接下来你会被要求输入有关声卡的一些技术信息，如图 6.5 所示。

![](img/70d85e6f4d1ff2750ca2a98ba3d9855c_178_1.png)

`图 6.4` 在声卡列表中滚动以选择你的笔记本声卡系统使用或仿真的卡片。

![](img/70d85e6f4d1ff2750ca2a98ba3d9855c_179_0.png)

`图 6.5` 如果被要求，请输入你笔记本中使用的声卡的 I/O 地址、IRQ 和 DMA 设置。

完成后，按 Enter。`sndconfig` 命令然后会尝试播放一个声音（Linus Torvalds 发音的 “Linux”），接着播放一段 MIDI 音阶。完成后，`sndconfig` 命令将保存设置。这些设置将用于你下次启动 Linux 时。

Linux 的声音支持由位于 `/lib/modules/2.X.XX/misc` 目录下的可加载内核模块提供（其中 X.XX 是你的 Linux 内核版本，可通过 `uname -r` 命令找到）。如果你安装了 Linux 内核源码，你将在 `/usr/src/linux/Documentation/sound` 目录中看到一些文档。例如：

```text
AD1816  ChangeLog.miti.sound  NE256  README.awe  es1370
ALS007  ESS                  OPL3   README.modules es1371
AKB32   ESS1868              OPL3-SA SoundPro imavr
AudioC  BoschDSP1          INSTALL.awe OPL3-SQ2 SoundBlaster solo1
CM8330  Introduction         Opl    Tropez+ sonivibes
CM8338  MADI4                 PCI-pro VIA-chipset ultrasound
CS4232  Maestro              PVS    VTBRAI6 vxmld
ChangeLog.awe MultiSound    README.OSS Wavefront
```

这些文件也可能位于 `/usr/doc/kernel-doc-2.X.XX` 目录下。如果你遇到问题，并且知道你笔记本电脑中使用的声卡芯片组，你可以尝试搜索相关文件以寻找配置线索。但如果似乎什么都行不通，不要放弃希望！还有其他帮助来源。

浏览到 http://www.alsa-project.org 并跟随链接下载高级 Linux 声音架构（ALSA）的 Linux 声卡驱动。这套免费的替代声卡驱动支持 75 种以上不同类型的声卡——并且对新卡片的支持也在不断增加。下载并解压所需的驱动、库和工具后，你需要进入每个目录并执行以下操作：

```bash
# ./configure
# make
# make install
```

这将构建并安装驱动（它们是可加载内核模块）。然后你可以使用推荐设置（记录在 ALSA 软件包中）在你的 `/etc/modprobe.conf` 或类似系统的 `/etc/conf.modules` 文件中，并配合 `modprobe` 命令，来加载和运行 ALSA 模块。

如果驱动兼容，它们将正确配置你笔记本声卡系统的元素，但在使用前必须“解除静音”。例如，要将主音量设置为 100%，你需要使用 ALSA 的 `amixer` 命令如下：

```bash
# amixer set Master 100 unmute
```

在解除其他识别设备的静音（如低音、高音、合成器、PCM、线路输入、麦克风和 CD）后，你可以播放音乐或声音。如果你需要有关安装和配置 ALSA 驱动的帮助，请浏览到 http://www.alsa-project.org/~valentin/Alsa-sound-mini-HOWTO.html

如果 ALSA 声音系统对你不起作用，你的下一个选择是浏览到 http://www.opensound.com。你可以从 4Front Technology 下载商业 Open Sound System 声卡驱动的演示版本。最后一次统计时，支持了 330 多种不同的声音系统。如果 Linux 发行版中包含的免费版 OSS 对你不起作用，那么这款软件很可能与你的笔记本声卡系统兼容。

从网页上选择正确版本后，下载 OSS 软件包。创建一个临时目录，将软件包复制到该目录中，并进入该临时目录。接下来，使用 `tar` 命令解压软件：

```bash
# tar xvfz oss*.tgz
INSTALL
LICENSE
oss-install
oss.pkg
```

要安装软件，请使用 `oss-install` 脚本如下：

```bash
# ./oss-install
```

屏幕将清空，你将看到一系列对话框帮助你安装声音支持。

### 解决 X 问题

尽管 Linux 在控制台（纯文本）模式下运行良好，但一个可用的 X11 配置可能极其重要且特别令人满意。除非你正在将笔记本用作服务器，否则你可能希望利用笔记本显示器的图形功能。好消息是，X11 几乎可以在每台曾制造出的笔记本电脑上工作。X11 工作得有多好取决于你的笔记本图形芯片组对 X 的支持程度。

利用 XFree86 软件充分发挥笔记本显示器的性能是几个因素的结合。首先，你的笔记本图形芯片组必须受到 XFree86 软件的支持。其次，你需要创建一个正确的 `XF86Config` 文件，该文件通常位于 `/etc/X11` 目录（如果你是作为 root 操作员测试 X，则位于 `/usr/X11R6/lib/X11` 或 `/root` 下）。

`XF86Config` 文件的设置对于正确配置图形界面至关重要。该文件包含处理以下各项的章节：

- 已安装字体和其他文件的位置
- X 服务器的设置和选项
- 键盘配置和各种按键的映射
- 指针设置，如类型、速度或按钮数量
- 笔记本 LCD 显示屏的正确水平和垂直频率设置
- 规格，如笔记本图形芯片组的显存数量和选项
- 笔记本可用的分辨率和颜色深度列表
- 指定默认使用何种颜色深度和分辨率的选项
