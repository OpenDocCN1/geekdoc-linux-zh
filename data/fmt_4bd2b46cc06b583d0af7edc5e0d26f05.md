
`fomatic-rip` 过滤器位于 `/usr/lib/cups/filter` 目录。
- `client.conf`: 指定客户端的默认选项（特别是默认服务器名称以及是否使用加密）。注意，客户端是将作业发送到另一机器打印的任何机器。这意味着当你的系统打印到本地打印机时，它是你系统上运行的 `cups` 调度程序的客户端。

## 总结

在 Linux 下打印是简单的，只要 CUPS 打印环境设置正确。你确实需要学习一小组命令来提交打印作业并检查等待打印作业的状态。本章从用户的角度解释了 CUPS 打印系统，以及如何作为系统管理员进行设置。

通过阅读本章，你学会了：

- Linux 自带 CUPS 打印系统，这是一个基于互联网打印协议 `IPP` 的打印系统的开源实现，并集成了 Fomatic 过滤器脚本和 Ghostscript 打印驱动程序等工具。
- 作为用户，你使用 `lq` 或 `lpr` 命令打印，使用 `lq` 或 `lpstat` 检查打印队列状态，使用 `lprm` 或 `cancel` 取消打印作业，并使用 `lpc` 检查打印机状态。
- 在后台，`lpr` 命令将打印文件和控制文件发送到 `cups` 服务器（打印守护进程），将其放在一个称为打印区的目录中。然后 `cupsd` 通过过滤器处理缓存的文件，并使用后端接口程序将其发送到打印机。
- 你可以使用打印机配置工具或 CUPS Web 界面 (`http://localhost:631/`) 设置打印机。
- CUPS 运行依赖位于 `/etc/cups` 目录下的若干配置文件。本章解释了这些配置文件。

## 音频设置

![](img/3b3329dddbc9c0857ad4f2ef1c0db305_153_0.png)

+ **本章秘密**
- 配置声卡 ............................................................ 124
- 手动配置声卡. ................................................ 127
- 测试声卡 ....................................................................... 128
- 播放音频 CD ................................................................ 129

## 第一部分：设置 Linux

没有声卡，PC 的内置扬声器只能播放单个音符；你无法改变音符的响度。幸运的是，现在的大多数 PC 都配有声卡——无论是独立显卡还是集成在主板上的某些电路——这提升了 PC 的音频输出能力。声卡是一种插入主板插槽的适配器，它包含了播放和录制声音所需的电子电路。你可以向声卡连接扬声器和麦克风。

当麦克风连接到声卡时，声卡可以将模拟（连续变化的）波形转换为 8 位或 16 位数字，采样频率从 4 kHz（每秒 4,000 次）到 44 kHz（每秒 44,000 次）甚至更高。更高的采样率和更高的位数（16位）提供更好的质量，但你需要更多的磁盘空间来存储高质音频。此外，声卡还可以将数字声音转换为可以在播放器上播放的音频信号。

大多数声卡（包括流行的 Sound Blaster）除了录制和播放音乐声音外，还支持 MIDI（乐器数字接口）命令。MIDI 通常用于录制和播放合成器可以创建的音乐（大多数设备具有内置合成器，可以作为 USB 端口连接到 PC 的独立 MIDI 和音频设备）。

本章介绍了受支持的特定类型声卡，以及在成功安装 Linux 后如何设置声卡。

## Linux 支持的声卡

Linux 内核 2.6 支持一种名为高级 Linux 架构（ALSA）的音频系统，它取代了旧的开放声音系统（OSS）。ALSA 使用模块化驱动程序，并支持各种声卡以及通过 USB 端口连接到 PC 的 MIDI 合成器等 USB音频设备。ALSA 继续支持旧的 OSS 驱动，因此使用 OSS 的程序可以继续在 ALSA 上运行。要了解更多 ALSA 的信息，请访问 ALSA 项目网站 `www.alsa-project.org`。

表 5-1 列出了 Linux 支持的声卡，并显示了支持特定声卡的驱动模块名称。要查看是否有适用于你声卡的 ALSA 驱动，请访问 `www.alsa-project.org/alsa-doc/` 的 ALSA 声卡矩阵页面并使用制造商名称进行查询。

> 要查看所有声卡厂商及其产品更多信息的链接：`www.alsa-project.org/alsa-doc/index.php?vendor=All`

| 表 5-1：支持的声卡 | |
| 声卡或芯片组 | ALSA 驱动模块 |
| :--- | :--- |
| Advanced Gravis UltraSound Classic | `snd-gus` |
| Advanced Gravis UltraSound Extreme | `snd-gusextreme` |
| Advanced Gravis UltraSound Max | `snd-gusmasmax` |

## 第 5 章：音频设置

### 声卡或芯片组

### ALSA 驱动模型

| 声卡或芯片组 | ALSA 驱动模块 |
| :--- | :--- |
| ALi1535, ALi1530D, MiS1535+, MiS1535D+ | |
| AMD InterWave; Advanced Gravis UltraSound PnP; Philips PCA761AW; STB Soundorage 32 | |
| Analog Devices AD1816; Aopen FX-3D Plus | |
| Analog Devices AD11847/848; Aztech Sound Galaxy; Cirrus Logic CS2428 | |
| ATI IXP 150/200/250 | |
| AudioTek Prodigy 71; MidiMan De Revolution 71; Mad Dog Multimedia Entertainer 71; Terratec Aureon 5/1 Sky/Space | |
| Aureal U880 | |
| Aureal U8820; Aztech PCI 338-A3D, 368-DSP; Turtle Beach Monte A3D | |
| Aureal U8830; Diamond Multimedia MonsterMX300; Turtle Beach Monte II | |
| Avance Logic ALS007 (Diamond Technologies DT-019X) | |
| Avance Logic ALS100/120 | |
| Avance Logic ALS4000; Best Union Miss Melody ALS4000; Chic Technology CoolSound 4000; Labway Xwave 4000 | |
| Aztech AZT2320 | |
| Aztech AZT3328, PCI 168 | |
| Aztech AZT2320 | |
| Brooktree B878/878a | |
| Cirrus Logic CS4231 | |
| Cirrus Logic CS4232/4232A | |
| Cirrus Logic CS4235/4236/4236B/4237B/4238B/4239 | |
| Cirrus Logic CS4281 | |
| Cirrus Logic CS4280/4610/4612/4614/4615/4622/4624; Aopen AW3220; Hercules F Game Fortissimo II and Game Theater XP; Midiman DIMAN PC Terratic Xfire 1024; Turtle Beach Santa Cruz; VideoLogicSonicFun | |
| C-Media MI8330 | |
| C-Media MiX838; ASJUND ASIC-8738; AudioExcel 510, MD Mate; Computer WanFast CMI-8378/PCI; Hercules Game Muse XL; Labway Xwave 7100; Midiman Delta 2448; Terratec Aureon 5/1; Trust Expert Surround | |
| Core Audio | |
| Creative Labs Sound Blaster 1.0/1.5/2.0/Pro | `snd-ali541` |
| Creative Labs Sound Blaster 16/16 PnP | `snd-sb16` |
| Creative Labs Sound Blaster 32 AWE/32 PnP | `snd-sbwe` |
| Creative Labs Sound Blaster PCI64/128 | `snd-ens370` |
| Creative Labs Sound Blaster 16/PCI64 (newer)/PCI128 (newer)/CTS88), Sound Blaster Ensonic | `snd-ens371` |
| Creative Labs Sound Blaster 512, SoundBlaster///Value | |
| Creative Labs Sound Blaster PCI (used by Dell) | `snd-emu10kx` |
| Creative Labs Sound Blaster LS, Sound Blaster 24 | `snd-ca0106` |
| Digigram VXPocket V2 and 440 Card | `snd-vxpocket` |
| Digigram VXPocket VX22 and VX222 | `snd-vx222` |
| Digigram mixtart 8 (AES/ESU) | `snd-mixart` |
| Ensoniq AudioPCI (ES1370) | |
| Ensoniq AudioPCI (ES1371/1372/1373) | `snd-ens371` |
| Ensoniq Soundscape | `snd-sscape` |
| ESS Technology ES968 | `snd-es968` |
| ESS Technology ES9688, ES1688 | `snd-es1688` |
| ESS Technology ES18xx | `snd-es18xx` |
| ESS Technology ES1938 (Solo 1), ES1946 (Solo 1E); Aopen AW180; Best Union Melody 1 Sound; Terratec 128 PCI | `snd-es1938` |
| ESS Technology ES1968 (Canyon3d, Maestro 1/2/2EM); Aopen AW300; Best Union Melody Maestro Sound; Diamond Multimedia Monsteround mx400, Simple Impact s100; Terratec;MX | `snd-es1968` |
| ESS Technology ES1990 (Maestro3), ES1989 (Maestro3, ES1990), (Canyon3D-2LE, Canyon3D-2), ES1999/19999/AW199B | `snd-maestro3` |
| Fortress FM801; Trend D35801A; Alt AU10; Genius SoundMaker Live; Lavmaq Wave GTX QS300A; Terratec 52i PCI | `snd-fm801` |
| IC IceElement 172 (Env24); Digigram VX442; Hootechnik; Soundtrack Audio DSP 24; Midiman Delta 44/66/410/1010/1010-LT, Delta Audiofile246, Delta EW2496; Terrateac EW58BD/88MT, EW24/96, DMX 6fre | `snd-ice1712` |
| Intel 8281AA,82901AB, i80, i810, i820, i830, i840, i845, MX440; Ali 545; Analog Devices AD18xx/19xx; Nvidia noe; Sis 735/740 | `snd-intel8x0` |
| Korg 1212I/O | |
| Labway Xwave 128 | |
| NeoMagic MagicMedia 256AV and 256ZX | |
| Oak Technology Mozart | |
| Philips H3600 PDA | |
| RME Dig32, Dig32Pro, Dig32/8 | `snd-332` |
| ... (省略重复的 RME 行) | |

## 配置声卡

Linux 需要一个驱动程序来控制声卡。在从附带 DVD-ROM 安装 Linux 后，Linux 内核会自动加载声卡驱动程序。声卡驱动程序以可加载模块的形式提供，你也可以手动加载或卸载它们。你会在 `/lib/modules/2.6.*/kernel/sound` 目录下发现声卡驱动程序组织在几个目录中。例如，`pci` 目录包含用于 PCI 声卡的驱动模块。如果你查看模块文件，你会发现每个以 `.ko` 扩展名结尾的文件（`.ko` 扩展名标识内核对象——一个包含实现驱动程序的二进制指令的文件）。

![](img/3b3329dddbc9c0857ad4f2ef1c0db305_158_0.png)

当内核启动 Linux 时，它会运行 `kudzu`，这是一个检测新硬件的工具。`kudzu` 会检测当前硬件并将其与存储在文本文件 `/etc/sysconfig/hwconf` 中的列表进行对比。它随后判断是否添加了任何硬件，并允许用户配置新硬件或移除对已安装硬件的支持。配置新硬件包括向 `/etc/probe.conf` 文件中添加相应的行，以便驱动模块在需要时被加载。声卡应该在启动过程中被 `kudzu` 检测到并配置，有时 `kudzu` 可能会为声卡加载错误的驱动程序。

随着 Linux 启动和 `kudzu` 检测到硬件，`kudzu` 会显示有关检测到的硬件的消息。启动信息滚动得快到无法阅读，但你可以使用 `dmesg` 命令查看它们。有多行提到了你声卡的名称或型号数字。你也可以查看 `/etc/sysconfig/hwconf` 文件，`kudzu` 在这里存储了它检测到的硬件信息。

如果你有旧的 ISA 即插即用 PnP 声卡，请在启动消息中寻找包含 `isappnp` 单词的行——这些行显示了 `kudzu` 检测 PnP 设备的结果。例如，在我的其中一台 PC 上，我有一张 Yamaha OPL3-SA3 声卡。在这种情况下，当我输入 `dmesg | grep isappnp` 时，我看到以下消息：

- `isappnp`: Scanning for PnP cards...
- `isappnp`: Card 'OPL3-SA3 SND System'
- `isappnp`: 1 Plug & Play card detected total

对于这张声卡，`/etc/probe.conf` 文件应该包含以下行：
```
alias snd-card-0 snd-opsl3-sa2
```

Fedora 提供了一个声卡配置工具 (`system-config-soundcard`)，但该工具不支持 ISA PnP 声卡工作。它只能检测 PCI 声卡。选择 Display: System Settings: Soundcard Detection。如果它检测到你的声卡，它会在一个小窗口中显示信息，如图 5-1 所示。

## 第 5 章：声音设置

![](img/3b3329dddbc9c0857ad4f2ef1c0db305_159_0.png)

**图 5-1：** `system-config-soundcard` 工具检测到的声卡。

你可以使用声卡配置工具播放测试音，但该工具没有提供任何配置声卡的方法（例如，加载不同的驱动模块）。底线是较新的 PCI 声卡在 Linux 中应该不需要太大麻烦就能正常工作，但对于旧的 ISA PnP 声卡，你必须做一些工作才能运行。

如果你知道自己的声卡类型，配置它的的一种方法是手动加载驱动并在 `/etc/modprobe.conf` 文件中设置信息，以便加载正确的驱动程序。

接下来的章节描述了如何在 Linux 上手动配置声音。

## 检查声卡信息

通常，你可以从 `kudzu` 在探测硬件时发现的内容获取有关你 PC 声卡的信息。`kudzu` 将所有检测到的硬件信息存储在以下位置：
