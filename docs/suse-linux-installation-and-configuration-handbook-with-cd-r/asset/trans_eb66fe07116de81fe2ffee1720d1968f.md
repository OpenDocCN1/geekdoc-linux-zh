

- I/O 端口 = 220 如行中所示
- I/O 端口 midi= 330 如行中所示
- I/O MPU 端口= 388 如行中所示

**提示** 你可以在文件 `/etc/isapnp.conf` 中找到声卡可用的所有配置组合。你可以注释掉所有配置，然后选择一个具有不同资源的不同配置，并取消注释指定你希望卡被设置成的正确配置的行。

完成后，再次发出 `isapnp` 命令并检查输出信息。尝试不同的配置，直到没有错误信息为止。如果仍然收到警告信息，请使用以下命令检查冲突：

- 要检查 IRQ 冲突，请输入以下内容：
  `bash#cat /proc/interrupts`
- 要检查 DMA 冲突，请输入以下内容：
  `bash#cat /proc/dma`
- 要检查 I/O 端口冲突，请输入以下内容：
  `bash#cat /proc/ioports`

请注意，当尝试将中断分配给其所有者时，如果其所有者已拥有该中断，`isapnp` 可能会生成错误。换句话说，假设卡已设置好使用 IRQ 5。如果再次运行 `isapnp`，它将生成错误，因为 IRQ 5 已被占用。重新启动并在系统启动时检查 `isapnp` 输出；如果一切顺利，你的系统就没问题了。如果出现任何致命错误冲突，你应该执行以下操作之一：

- 如果你绝对确定提到的错误不是致命的，那么编辑 `isapnp.conf` 文件并将冲突行从
  `(CONFLICT (IO FATAL) (IRQ FATAL) (DMA FATAL) (MEM FATAL))`
  改为
  `(CONFLICT (IRQ WARNING) (DMA WARNING) (MEM WARNING))`
  在此示例中，你强制 `isapnp` 生成警告信息而不是致命错误信息。你还强制它不对 I/O 冲突提出任何抱怨。
- 如果有你想消除的冲突，那么编辑 `isapnp.conf` 文件并选择不同的配置。

## OSS/Lite 的配置

随内核提供的 OSS/lite 版本配置并不困难。此版本的 main 配置文件为 /etc/modules.conf，其中包含在加载时应分配给模块的参数。与将其作为内置使用相比，将声音设置为模块有更多优势。有关模块的更多信息，请参阅第 8 章“安装新内核”。如果你使用的是默认的 SuSE 内核，即从 SuSE 预编译的内核，请确保安装模块包。以下是在你不想重新编译内核的情况下所需的软件包：

Series a：

- modules
- kernmod（只有在你不想重新编译内核时才需要）

另一方面，如果你喜欢编译自己的内核，你应该安装以下软件包：

Series d：

- linclude
- linux

或

Series d：

- lx_suse

## 内核配置和声卡

在讨论这一部分之前，如果你不想重新编译内核并且当前使用的是随 SuSE 提供的版本，你可以跳过这一部分，直接转到修改模块配置文件。如果你使用的是自己安装的不同内核，建议你阅读这一部分。

### 我的声卡需要什么内核配置？

这是你应该问自己的最重要问题。找到正确答案的最佳方法是查看 /usr/src/linux/Documentation/sound 目录。在此目录中，搜索与你的声卡同名的文件并阅读相关信息。接下来，启动你喜欢的任何内核配置实用程序（请参阅第 8 章）。在运行 X 时，打开一个 xterm 并发出以下命令：

```
bash$xhost +localhost
bash$su -l
bash$cd /usr/src/linux/
bash$export DISPLAY=:0
bash$make xconfig
```

假设你有一张 SB16 卡想要设置。首先单击声音按钮并查看你有哪些选项：

- Sound card support
- OSS sound modules（大量声卡由 OSS/lite 支持）
- 100% Sound Blaster compatibles（SB16/32/64, ESS, and Jazz 16）support
- FM synthesizer（YM3812/OPL-3）support

这些都是为你的 SB16 卡设置所需的所有选项（参见图 10.1）。对于前一条列表中第三个项目符号列出的卡，即（SB16/32/64, ESS, and Jazz 16），它们将相同。

FIGURE 10.1
为 Sound Blaster 16 设置内核选项。你可以随时单击 help 以获取有关驱动程序支持的卡的更多信息。

![](img/659f91d9da7b29976c0625e2e9628511_236_0.png)

挑选正确的模块并不困难。你可以阅读你选择的每个选项的帮助内容。此外，如果你添加了声卡实际上不需要的模块，唯一的有害结果将是编译时间的增加。这在快速机器上不是严重问题，尽管这不是一个好习惯

## 编辑模块配置文件

模块配置文件的名称已从 `/etc/conf.modules` 更改为 `/etc/modules.conf`。SuSE 已为你准备好了一切。SuSE 团队为你提供了一个可直接编辑的 `modules.conf` 文件，这将使你的生活更轻松。首先，你必须了解这个文件的作用。`modules.conf` 包含模块启动时应使用的选项。因为声音被编译为模块，所以在加载时，它使用存储在 `modules.conf` 文件中的配置来调整到此配置。SuSE 的 `modules.conf` 文件为大多数声卡预先设置好了，只需取消注释并设置即可直接使用。对于你刚刚制作的 SB16，现在你将为其内核配置设置 modules.conf 文件。

## 激活声音字符设备

在 modules.conf 文件中，声音模块默认处于关闭状态。你需要注释掉以下行：

```
alias char-major-14 off
alias sound off
alias midi off
```

从而将其更改为

```
#alias char-major-14 off
#alias sound off
#alias midi off
```

在随 SuSE 提供的原始 modules.conf 文件中，这些行应位于第 44 行左右。

> **警告**
> 
> SuSE Linux 随附声音字符设备处于关闭状态。你必须在你可以使用声音之前将其打开。即使你正确设置了声卡，如果你将声音字符设备保持关闭状态，你的声卡也将无法工作。

## 设置声卡参数

如果你查看可用的声卡，你会找到以下部分：

```
1 # ***************************************************************
2 # module : sb.o               Soundblaster 16, SB Pro + Clones
3 #                            Also needed for AWE32/64
4 #
5 # Documentation available in
6 /usr/src/linux/Documentation/sound/Soundblaster
7 # and in /usr/src/linux/drivers/sound/sb.c .
8 #
9 # Possible configuration :
10 # alias char-major-14 sb
11 # post-install sb /sbin/modprobe "-k" "adlib_card"
12 # options sb io=0x220 irq=7 dma=1 dma16=5 mpu_io=0x330
13 # options adlib_card io=0x388
14 # ***************************************************************
15 #
```

如果设置正确，此部分将是 SB16 卡的配置。假设声卡使用 IRQ=5，IO=0x220，DMA=1——8 位 DMA，DMA16=5——16 位 DMA，MPU_IO=0x330，以及 ADLIB_CARD_IO=0x388。这些值可以从 isapnp.conf 文件中获得，也可以从你对卡进行的跳线设置中获得。

因此，行应如下所示：

```
10 alias char-major-14 sb
11 post-install sb /sbin/modprobe -k "adlib_card"
12 options sb io=0x220 irq=5 dma=1 dma16=5 mpu_io=0x300
13 options adlib_card io=0x388
```

请注意，你移除了 # 符号，这意味着该行不是注释。还请注意，行号未包含在内，但在此仅为说明目的而写出。

## 安装模块

这是所有过程中最简单的步骤。在此步骤中，你将加载声音模块。加载新配置后，你将能够收听音乐。请按照以下步骤操作：

- 1. 在另一个控制台中，运行命令 `#tail -f /var/log/messages`。
- 2. 接下来你需要加载声音模块。发出以下命令以探测声音模块：
  ```
  bash#modprobe sb
  ```
  sb 是我们给模块的名称。在 `/etc/modules.conf` 文件（第 10 行）中，我们将声音字符设备称为 sb。

## 测试声音配置

你可以通过发出以下命令来测试适当的声卡配置是否存在：

```
bash#cat /dev/sndstat
OSS/Free:3.8z++-971130
Load type: Driver loaded as a module
Kernel: Linux coffin 2.2.13 #12 Sun Oct 24 07:10:02 EET 1999 1586
Config options:

Installed drivers:

Card config:

Audio devices:
0: Sound Blaster 16 (4.13) (DUPLEX)

Synth devices:
0: Yamaha OPL3

Midi devices:
0: Sound Blaster

Timers:
0: System clock

Mixers:
0: Sound Blaster
```

