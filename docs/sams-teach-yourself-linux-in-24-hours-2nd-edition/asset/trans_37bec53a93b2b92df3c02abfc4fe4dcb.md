
## 为 OpenLinux 配置声音

配置 OpenLinux 使用计算机的声音系统可以被视为成功 Linux 安装的最后一个主要障碍之一。当然，如果对你来说播放音乐、观看网络电视或参与 Quake 休闲死亡竞赛很重要，那么声音配置就是一项重要任务。

好消息是，在过去几年中，Linux 已演进到使配置声音的工作变得容易得多。过去，配置 Linux 使用声音涉及一个可能令人沮丧的循环，即配置内核源代码、编译和测试。然而今天，内核使用可加载代码模块为计算机提供声音支持。

更好的消息是，今天大多数计算机在播放声音时遵循通用协议。你可以轻松配置 OpenLinux 通过计算机的声卡播放声音。

## 加载声音模块

OpenLinux 附带近 30 个可加载代码声音模块，位于 /lib/modules/2.2.3/sound 目录下，其中 2.2.3 是你的 OpenLinux 内核版本（或使用 -r 选项的 uname 命令的输出）。请看以下示例：

```
# uname -r
2.2.3
# ls /lib/modules/2.2.3/sound
aci.o      gus.o      opl3sa2.o      soundlow.o
ad1816.o   mad16.o    pas2.o         sscape.o
ad1848.o   maui.o     pss.o         trix.o
adlib_card.o mpu401.o  sb.o           sgalaxy.o    uart401.o
aedsp16.o  msnd.o     softoss2.o     uart6850.o
awe_wave.o msnd_classic.o sonicvibs.o   v_midi.o
cs4232.o     msnd_pinnacle.o sound.o        wavefront.o
es1370.o   opl3.o     soundcore.o
es1371.o   opl3sa.o
```

这些代码模块支持为标准 OpenLinux 2.2 内核配置的声卡。你可以通过查看 /boot 目录下的 WHATSIN-2.2.3-modular 文档（其中 2.2.3 是你的 Linux 内核版本）来了解内核的具体配置。表 3.3 仅列出了 OpenLinux 支持的部分声卡（及兼容卡）和模块。

### 表 3.3 OPENLINUX 2.2 内核模块声音支持

| 名称 | 模块 |
|---|---|
| Crystal CS4232 (PnP) | cs4232.o, ad1848.o |
| Ensoniq ES1370 | es1370.o |
| Ensoniq ES1371 | es1371.o |
| Ensoniq SoundScape | sscape.o |
| 通用 OPL2/OPL3 FM 合成器 | opl3.o |
| Gravis Ultrasound | gus.o |
| MediaTrix AudioTrix Pro | trix.o |
| MPU-401 | mpu401.o |
| OPTi MAD16, Mozart | mad16.o |
| ProAudioSpectrum 16 | pas2.o |
| PSS, ECHO-ADI2111 | pss.o |
| Rockwell Wave Artist (Netwinder) | waveartist.o |
| SoftOSS 软件波表 | softoss2.o |
| Sound Blaster 兼容卡、Aztec Sound Galaxy、SB16/32/64/AWE、ESS、Jazz16 | sb.o |
| 声卡支持 | sound.o, sbcard.o |
| Turtle Beach Wave Front、Maui、Tropez | wavefront.o, maui.o |
| Yamaha OPL3-SA1 | opl3.o |

在开始之前，找到并写下计算机声音系统的 I/O 端口地址、IRQ 和 DMA 通道号。如果你遵循了第 1 小时“Preparing to Install Linux.”中的建议，你就有这些信息。

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_72_0.png)

> 如果你从 CD-ROM 完整安装了 OpenLinux（包含 Linux 源代码），你可以找到一个优秀的教程，以及有关配置 OpenLinux 与声卡配合使用的详细信息。查看目录 `/usr/src/linux/Documentation/sound`，并且务必阅读文件 README.modules。`/usr/src/linux/drivers/sound` 目录包含声音模块的源代码。还请阅读 `/usr/doc/HOWTO` 目录下的 Sound-HOWTO。

以 root 操作员身份登录。在控制台或 X11 终端窗口的命令行中，使用 insmod 命令加载声音内核模块。此过程适用于大多数配备 SoundBlaster 或等效声卡的计算机。输入以下内容，并将 io、irq 和 dma 值替换为你计算机的值：

```
# insmod sound
# insmod uart401
# insmod sb io=0x220 irq=5 dma=1
```

然后你可以使用 lsmod 命令查看声音模块是否已加载，如下所示：

| 模块 | 大小 | 使用者 |
|---|---|---|
| sb | 32660 | 1 |
| uart401 | 5936 | 1 [sb] |
| sound | 58584 | 0 (autoclean) [sb uart401] |
| soundcore | 2404 | 5 (autoclean) [sb sound] |
| soundlow | 300 | 0 (autoclean) [sound] |
| ... |  |  |

你也可以尝试查看 /dev/sndstat 设备的输出，如下所示（你的输出可能不同）：

```
# cat /dev/sndstat
OSS/Free:3.8s++-971130
Load type: Driver loaded as a module
Kernel: Linux noname.nodomain.nowhere 2.2.3 #1 Tue Mar 9 23:27:39 MST 1999
i586
Config options: 0
Installed drivers:
Card config:
Audio devices:
0: ESS ES1688 AudioDrive (rev 11) (3.1)
Synth devices:
Midi devices:
Timers:
0: System clock
Mixers:
0: Sound Blaster
```

## 测试你的声音配置

尝试播放 KDE 发行版中包含的声音。使用 play 命令通过播放 ktalkd.wav（电话铃声）来测试你的声卡，如下所示：

```
# play /opt/kde/share/sounds/ktalkd.wav
```

如果你的声音配置第一次不工作，或如果你输入了错误的设置，使用 rmmod 命令，后跟驱动程序的名称，从系统内存中卸载每个声音模块然后重试。如果声音正常，太好了！

你可以从本书的 CD-ROM 中找到许多为 OpenLinux 安装的声音实用程序。一些实用的工具包括用于 KDE 的 kmix 和用于控制系统声音平衡和来源的 xmixer。

## 使用 COAS 配置声音

OpenLinux 附带一个新实用程序，即 Caldera Open Administration System，或 COAS，你可以用它来管理和配置 Linux。COAS 可用于控制 OpenLinux 系统的许多不同功能，包括以下内容：

- 以太网接口，例如计算机的 Internet 协议（IP）地址
- 文件系统，例如本地或远程存储设备的挂载选项
- 主机名解析，例如计算机查找其他计算机名称和地址的位置
- 内核模块启动时控制，从内存中加载或卸载内核模块，例如声音模块（OpenLinux 包含超过 350 个内核模块）
- 邮件，例如设置电子邮件消息的发送或接收方式
- 网络服务，例如网络信息服务
- 外设控制，用于配置键盘、鼠标或打印机
- 软件管理，用于控制安装在计算机上的软件类型，例如科学或文字处理包
- 系统资源信息，提供有关计算机中央处理单元（CPU）的信息
- 系统服务，例如启动时要启动的服务（例如，打印）
- 时间，例如设置系统时钟和时区（旅行时很有用）
- 用户管理，例如添加、删除或重命名用户和密码

COAS 是一个“正在进行的工作”。这意味着并非所有功能都可能在我们 CD-ROM 包含的版本中启用。查看 http://www.calderasystems.com 并浏览新闻和支持区域以获取有关你的 OpenLinux 版本的信息。

当声音工作正常时，通过单击 K Desktop Environment 面板上的 Application Starter 按钮启动 COAS；选择 COAS，然后单击 Kernel 菜单项，如图 3.1 所示。

### 图 3.1

COAS 客户端可用于配置 OpenLinux 内核模块。

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_75_0.png)

你会看到一个简短的欢迎对话框。单击 OK 按钮或按 Enter 继续。然后你会看到一个对话框，如图 3.2 所示，右侧列出当前已加载的内核模块，左侧列出可用的模块。

### 图 3.2

通过单击左侧（未加载）或右侧（已加载）对话框列表中的模块名称来配置系统的内核模块。

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_76_0.png)

使用此之前的示例，滚动左侧的模块列表，然后选择 sound 模块，单击 Load 按钮。会出现一个对话框，如图 3.3 所示。

### 图 3.3

使用 COAS 配置内核模块的加载方式或时间。

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_76_1.png)

因为不需要任何选项（对于此示例），请确保 Load at boot time 按钮已启用。单击 OK 按钮。接下来，滚动左侧的模块列表，选择 uart401 模块，单击 Load 按钮。再次确保启动时加载，然后单击 OK。要完成声音配置，滚动模块列表并选择 sb 模块。单击 Load 按钮，你会看到一个类似于图 3.4 的对话框。
