
| Turtle Beach MultiSound Pinnacle | `msnd.0`, `msnd_pinnacle.o` |
| Turtle Beach MultiSound Tahiti | `msnd.0` |
| Turtle Beach WaveFront Maui | `maui.0` |
| Turtle Beach WaveFront Tropez | `maui.0` |
| Turtle Beach WaveFront Tropez+ | `maui.0` |
| VIDC 16-bit sound | `v_midi.o` |
| Yamaha OPL3 sound chip | `op13.0` |
| Yamaha OPL3-SA1 sound chip | `op13sa.o` |
| Yamaha OPL3-SA2 sound chip | `op13sa.o` |
| Yamaha OPL3-SA3 sound chip | `op13sa.o` |
| Yamaha OPL3-SAX sound chip | `op13sa.o` |

选择声卡是实现于安装的关键。通常有三种声卡安装方式：安装新声卡、利用现有声卡以及板载声卡。最容易安装和配置且最干净的声卡是 PCI 声卡，它简化了 DMA、I/O 通道和 IRQ 的配置，并利用更快的 PCI 总线而非 ISA 总线。下一个选择是寻找带有跳线线的卡，但你可能从一个升级到最新显卡的朋友那里买到良好的二手卡。你也可以在电脑商店找到。第三种选择是即插即用（PnP）卡。使用 `isapp` 工具来配置 PnP 卡。PnP 的挑战在于卡设置是动态分配的。如果你添加一个新的 PnP 卡，它可能会移动卡设置。这样做是好事，因为你不需要知道如何配置设置；但也是坏事，因为它并不总是可预测的。这导致每当你添加一张新卡时，每张卡都有可能重新配置的风险。

# Linux 多媒体

第 27 章

第二种安装方式是在从另一个操作系统转换而来的系统或可能没有 PCI 总线的旧系统中配置现有声卡。第一步是检查 Linux sound HOWTO 列表，查看具体的卡型号是否在列表中。兼容 SoundBlaster 的卡可能无法通过 SoundBlaster 驱动程序工作。下一步是确定该卡在现有操作系统下运行正常，并记录 IRQ、I/O 端口、DMA 地址、MIDI 端口、游戏端口地址以及安装卡所需的任何其他配置参数。

- 获取声驱动程序有三种方法：发行版自带的标准内核模块；商业 Open Sound System（OSS）驱动程序；以及 ALSA 驱动程序。

包含 Alan Cox 重要贡献的标准内核模块包含在 SuSE 发行版中。

来自 4Front Technologies (`http://www.opensound.com`) 的商业 Open Sound System 驱动程序包含在 SuSE 发行版中。SuSE 6.2 包含了商业声卡驱动程序的特殊许可。

高级 Linux 音频架构（ALSA）驱动程序（CD-ROM 上的 `snd` 系列或位于 `http://www.alsa-project.org`）是标准 OSS 声卡驱动程序的替代方案。有一个独立的 ALSA mini-HOWTO 可以解答有关安装的问题以及为什么 ALSA 是标准驱动程序的可行替代方案。

第三种卡安装方式是板载声卡/芯片；它已经集成在主板上。初看之下，集成了视频、音频、串口、并行和游戏端口的集成主板是一个有趣的概念。这最初很有吸引力，因为这些主板通常比其他主板便宜，而且所有功能集成在一起非常方便。主流制造商销售带有集成芯片的台式电脑和笔记本电脑。表 27.1 列出了板载芯片。

## 内核模块

# 图形、多媒体与生产力工具

第四部分

### 注意事项

第二种安装方式是在从另一个操作系统转换而来的系统或可能没有 PCI 总线的旧系统中配置现有声卡。第一步是检查 Linux sound HOWTO 列表，查看具体的卡型号是否在列表中。兼容 SoundBlaster 的卡可能无法通过 SoundBlaster 驱动程序工作。下一步是确定该卡在现有操作系统下运行正常，并记录 IRQ、I/O 端口、DMA 地址、MIDI 端口、游戏端口地址以及安装卡所需的任何其他配置参数。

- 获取声程序有三种方法：发行版自带的标准内核模块；商业 Open Sound System 驱动程序；以及 ALSA 驱动程序。

包含 Alan Cox 重要贡献的标准内核模块包含在 SuSE 发行版中。

来自 4Front Technologies (`http://www.opensound.com`) 的商业 Open Sound System 驱动程序包含在 SuSE 发行版中。SuSE 6.2 包含了商业声卡驱动程序的特殊许可。

高级 Linux 音频架构（ALSA）驱动程序（CD-ROM 上的 `snd` 系列或位于 `http://www.alsa-project.org`）是标准 OSS 声卡驱动程序的替代方案。有一个独立的 ALSA mini-HOWTO 可以解答有关安装的问题以及为什么 ALSA 是标准驱动程序的可行替代方案。

第三种卡安装方式是板载声卡/芯片；它已经集成在主板上。初看之下，集成了视频、音频、串口、并行和游戏端口的集成主板是一个有趣的概念。这最初很有吸引力，因为这些主板通常比其他主板便宜，而且所有功能集成在一起非常方便。主流制造商销售带有集成芯片的台式电脑和笔记本电脑。表 27.1 列出了板载芯片。

# Open Sound System (OSS)

OSS 驱动程序来自 4Front Technologies，并在 YaST 驱动程序下加载。图 27.2 显示了如何使用 YaST 加载 OSS 驱动程序。

# Linux 多媒体 第 27 章

## 图 27.4

OSS 自动检测功能。

![](img/cbac72550c7126a22162e94d91a0c360_886_0.png)

## 图 27.5

OSS 声卡列表。

![](img/cbac72550c7126a22162e94d91a0c360_886_1.png)

## 图 27.6

OSS 配置对话框。

![](img/cbac72550c7126a22162e94d91a0c360_886_2.png)

如果由于某些原因初始加载入无法正常工作，或者您需要修改 DMA、IRQ 或 I/O 端口，请使用 `soundconf` 更新驱动程序。

商业版 OSS 驱动程序还包含额外功能，例如针对某些笔记本电脑的定制驱动程序。`http://www.opensound.com` 网页提供了有关扩展功能的更多信息。某些升级功能可能未包含在 SuSE 6.2 发版中（更多信息请参阅 OSS 软件许可协议）。

## 高级 Linux 音频架构 (ALSA)

ALSA 是 OSS/Lite 以及 4Front Technologies 商业音频驱动程序的替代方案。它包含一些高级功能，并起源于 Linux Ultra Sound 项目。ALSA 项目网页（`http://www.alsa-project.org`）指出以下是其主要目标：

- 创建一个支持内核和 kmod 的完全模块化的音频驱动程序。
- 创建 ALSA 内核 API，其超越了当前的 OSS API。
- 保持与大多数 OSS/Lite 二进制文件的兼容性。
- 创建 ALSA 库（C, C++），简化 ALSA 应用开发。
- 创建 ALSA Manager，一个用于驱动程序的交互式配置程序。

由 Valentijn Sessink 创建的《ALSA-sound mini-HOWTO》版本 1.7，日期为 1999 年 7 月 29 日，是安装 ALSA 驱动程序的良好信息来源。

ALSA 驱动程序可以通过 SuSE 6.2 CD-ROM 获取，并可以使用 YaST 在 `snd` 系列下加载。ASLA 包 0.3.0_pre5_1999_03_28_16 解压缩后为 1.8MB。如果您必须下载或更新驱动程序，可能需要编译模块。这与其他项目的编译方式完全相同：按照文档中概述的 `./configure`、`make` 和 `make install` 步骤进行。

以 Ensoniq AudioPCI ES1371 为例，命令将是：

```
# /sbin/modprobe snd-audiopci
```

与内核驱动程序一样，声卡可以通过 `modprobe` 命令加载，您可以修改 `/etc/conf.modules` 文件以在启动时加载驱动程序。

## 播放音频 CD

听音乐 CD 有两种方式：通过 CD-ROM 驱动器本身的插孔，以及通过声卡。无论哪种方式，都能在电脑上工作时提供愉快的体验。本节将描述如何通过您系统的声卡播放音频 CD。

## 初始配置

CD-ROM 和声卡的初始配置包含两个部分：需要连接设备之间的物理线缆，并且需要安装运行音频 CD 的软件。CD-ROM 和声卡之间通常有一根音频线缆。音频线缆的大小与典型的鼠标线相当，通常每端都有一个四针塑料连接器。请参阅声卡和 CD-ROM 说明书以获取精确的连接指令。内置声卡主板上的音频线缆通常连接到主板上的插座或一组引脚。

> 提示
