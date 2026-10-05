

```bash
alias char-major-14 off
alias sound off
alias midi off
```

## 第12 章：计算器、音乐制作器与人们的游戏

并在每行前面添加一个注释符号 (#)，如下所示：

```bash
#alias char-major-14 off
#alias sound off
#alias midi off
```

现在，你的系统不再禁用声卡支持了。
接下来，你需要向下滚动，找到文件中为你的声卡预先配置好的区域，并移除以 `alias`、`post-install` 或 `mpu` 等任何一个单词开行的注释符号。以下是一个为 Soundblaster 或克隆声卡预配置的文件部分示例：

```bash
********************************
# module: sb.0 Soundblaster 16, SB Pro + Clones
#                               Also needed for AWE32/64
#
# Documentation available in
# /usr/src/linux/Documentation/sound/Soundblaster
# and in /usr/src/linux/drivers/sound/sb.c .
# Possible configuration:
# alias char-major-14 sb
# post-install sb /sbin/modprobe "-k" "adlib_card"
# options sb io=0x220 irq=7 dma1=6
# mpu_io=0x330
# options adlib_card io=0x388
********************************
```

你在这个示例中看到的是模块的全名 (sb.o)、使用该模块的卡列表 (Soundblaster 16, SB Pro + Clones，还需要 AWE32/64)，以及在哪里可以找到额外文档的描述。转向该部分的底部，你会看到几行看起来晦懂的代码。这些行包含了关于你的声卡模块应该使用哪些资源的信息。在这个示例中，我们正在使用 `sb` 模块来支持 Soundblaster 声卡，我们需要取消这些行的注释，如下：

```bash
#
#alias char-major-14 sb
#post-install sb /sbin/modprobe "-k" "adlib_card"
#options sb io=0x220 irq=7 dma1=6
#mpu_io=0x330
#options adlib_card io=0x388
#
```

`/etc/conf.modules` 中的配置设置之所以被选中，是因为它们适用于大多数声卡。但也可能不适用于你的声卡。这可能是由于与你电脑上的另一个设备存在资源冲突（中断或 I/O 端口），在某些情况下由于声卡上的跳线（jumper）设置。无论是哪种情况，你都应该检查当前正在使用哪些中断和 i端口。你可以使用以下命令查看当前正在使用的中断：

![](img/96a9ce6a13d8d15ed05f867f41574278_237_0.png)

```bash
bash-2.03# cat /proc/interrupts
```

它将产生类似下面的输出：

| 中断 (Interrupt) | 值 (Value) | 描述 (Description) |
| :--- | :--- | :--- |
| 0: | 49893 | XT-PIC定时器 |
| 1: | 206 | XT-PIC 键盘 |
| 2: | 0 | XT-PIC 级联 |
| 8: | 3 | XT-PIC RTC |
| 12: | | XT-PIC PS/2 鼠标 |
| 13: | 1 | XT-PIC fou |
| 14: | 57363 | XT-PIC ide0 |

你可以使用以下命令查看当前正在使用的 iports：

```bash
bash-2.03# cat /proc/ioports
```

它将产生类似下面的输出：

```
0000-001f : dma1
0020-003f : pic1
0040-005f : timer
0060-006f : keyboard
0070-007f : rtc
0080-008f : DMA page reg
00a0-00bf : pic2
00c0-00df : dma2
00f0-00ff : fpu
01f0-017f : ide0
02f8-02ff : serial(auto)
03c0-03df : vga+
03f6-036f : ide0
03f8-03ff : serial(auto)
e800-e807 : ide0
e808-e80f : ide11
```

如果看起来与另一个设备没有冲突，你只需要更改声卡上的跳线设置，或者更改 `/etc/conf.modules` 中的值，使其与你卡上的跳线设置相对应。

在对 `/etc/conf.modules` 文件进行了必要的修改后，保存它。现在你应该测试配置是否可以手动加载模块。你现在只需要手动加载你正在测试的模块以验证它们是否正常。在验证之后，你就不需要再考虑它们了，因为它们会在内核需要它们时被自动加载。

- 1. 首先，由于你修改了模块配置文件，你需要通过执行以下命令来更新模块依赖文件：

```bash
bash-2.03# depmod -a
```

你可能会收到一条消息，说有一些未解决的依赖关系，你不需要对它们感到。。

- 2. 当文件更新后（命令行提示符再次出现），尝试加载你声卡的模块。在这个示例中，对于 Soundblast，模块是 `sb`（注意，加载模块时我们不使用全名），命令看起来所示：

```bash
bash-2.03# modprobe sb
```

如果模块加载成功，你将看不到任何错误信息。你可以通过显示当前模块列表来验证该模块已加载：

```bash
bash-2.03# lsmod
```

它将给你一个类似下面的输出：

| 模块 (Module) | 大小 (Size) | 使用情况 (Used by) |
| :--- | :--- | :--- |
| bttv | 6808 | 0 (autoclean) |
| i2c | 206 | 0 (autoclean) |
| videodev | 3144 | 0 (autoclean) |
| adlib_card | 5552 | 0 (autoclean) |
| sound | 3125 | 0 (autoclean) |
| sb | 2008 | 0 (autoclean) |
| uart401 | 5576 | 0 (autoclean) |
| serial | 4194 | 0 (autoclean) |
| memstat | 1544 | 0 (autoclean) |
| lsmod | 1412 | 0 (autoclean) |
| snd_pcm | 8736 | 0 (autoclean) |
| snd_sb | 4000 | 0 (autoclean) |
| snd_card | 12000 | 0 (autoclean) |

此外，如果没有错误，你可以通过执行以下命令测试声卡：

```bash
bash-2.03# cat /proc/interrupts
```

它将产生类似下面的输出：

```
内核模块: 2.0.33-x86-2
加载于: Jan 1 00:00:00 UTC 2001
CPU: 0
SMP: 0 processor(s) available
processor(s): 0
中断:
00000000 00000000 00000000 00000000 00000000 00000000 00000000 00000000
00000000 00000000 00000000 00000000 00000000 00000000 00000000 00000000...
```

如果没有与另一个设备发生冲突，你只需要更改声卡上的跳线设置，或者更改 `/etc/conf.modules` 中的值，使其与你卡上的跳线设置相对应。

