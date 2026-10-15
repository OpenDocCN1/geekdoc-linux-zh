
我们将使用此 kickstart 文件来设置仅安装 Linux 的类似 PC，并清除之前安装的所有内容。

## 244 第 5 章：高级安装

编辑下面的条目以取消注释所需的配置。请注意，任何范围仅给出第一个值；如果需要，可以进行更改。在满意后，别忘记取消注释激活 (`ACTY`)。

```
(CONFIGURE CTL00EO/-1 (LD 0
# ANSI 字符串 --Audio--
# 多选一时间，仅选择一种！
# 启动相关函数：优先 own
IRQ 5
# 高电有效，边沿触发中断（默认）
# (INT 0 (IRQ 5 (MODE=E))
# 第一个 DMA 通道 1
# 仅位 DMA
# 逻辑设备不是总线主设备
# DMA 可以以字节计数模式执行
# DMA 不可以字计数模式执行
# 兼容模式下的 DMA 通道速度
# (DMA 0 (CHANNEL 1))
# 下一个 DMA 通道 1
# 仅位 DMA
# 逻辑设备不是总线主设备
# DMA 可以以字节计数模式执行
# DMA 不可以字计数模式执行
# 兼容模式下的 DMA 通道速度
# (DMA 1 (CHANNEL 3))
# 逻辑设备代码 16 位 IO 地址线
# 最小 10 基地址 0x0220
# 最大 10 基地址 0x0230
# IO 对齐 1 字节
# 需要的 IO 地址数：16
# (IO 0 (SIZE 16) (BASE 0x0220))
# 逻辑设备代码 16 位 IO 地址线
# 最小 10 基地址 0x0230
# 最大 10 基地址 0x0240
# IO 对齐 1 字节
# 需要的 IO 地址数：2
# (IO 1 (SIZE 2) (BASE 0x0388))
# 逻辑设备代码 16 位 IO 地址线
# 最小 10 基地址 0x0188
# 最大 10 基地址 0x0198
# IO 对齐 1 字节
# 需要的 IO 地址数：4
# (IO 2 (SIZE 4) (BASE 0x0388))
# 启动相关函数：允许优先
IRQ 5, 7 或 9
# 高电有效，边沿触发中断（默认）
[为了清晰起见，已删除多行:]
# 结束相关函数
(NAME "CTL8EIO-1(B)\Audio")
# (ACTY):
```

## 硬件冲突与即插即用 245

```
)
# 逻辑设备 ID 为 CTL705
# 设备支持厂商保留寄存器 @ 0x38
# 设备支持厂商保留寄存器 @ 0x3a
# 设备支持厂商保留寄存器 @ 0x3c
```

编辑下面的条目以取消注释所需的配置。请注意，任何范围仅给出第一个值；如果需要，可以进行更改。在满意后，别忘记激活的 (`ACTY`)。

```
(CONFIGURE CTL00f/-1)
# 兼容设备 ID PNP0b2f
# 字符串 -->Game--
# 多选一时间，选择一个！
# 启动相关函数：允许优先
# 逻辑设备解码 16 位 IO 地址线
# 最小 IO 基地址 0x0201
# 最大 IO 基地址 0x0201
# IO 基对齐 1 字节
# 需要的 IO 地址数：1
# (IO 0 (SIZE 1) (BASE 0x1))
# 启动相关函数：允许优先
# 逻辑设备解码 16 位 IO 地址线
# 最小 IO 基地址 0x0200
# 最大 IO 基地址 0x020f
# IO 基对齐 1 字节
# 需要的 IO 地址数：1
# (IO 0 (SIZE 1) (BASE 0x0200))
# 结束相关函数
(NAME CTL00f/-1)(1(Game
# (ACTY)
# 结束标签... 校验 0x00 (OK)
# 返回所有到“等待按键”状态的
(WAITFORKEY)
```

通过此输出，你可以看到安装了一块 SoundBlaster 16 ISA PnP 卡。这还显示卡上有一个可以单独配置的 Game Port（游戏端口）。你可以看到所有行都已注释。你需要检查 `/proc/interrupts` 和 `/proc/iopports` 来找到可用资源以配置你的声卡。我们将假设 IRQ 5、IO 0x220 和 DMA 0 未被占用。只需取消注释以下行即可指定这些：

## 246 第 5 章：高级安装

```
# ID: pnpdump.c.v 1.18 1999/02/14 22:47:18 fox Exp S
# 这是一个自由软件，详情请参阅源码。
# 此软件无任何保证，风险自自。

# 有关此文件格式的详情，请参见 isannpconf(5)
# http://www.roestock.demon.co.uk/isapnptools/
# 关于 isapnp 和 pnpdump 的最新信息和常见问题：
# 编译器标志：-DREALTIME -DNEEDSETSCHEDULER -DABORT_ONRESERR
# 尝试端口地址 0203
# 板 1 的序列标识符为 6d ff ff ff 00 8c e
# 板 2 的序列标识符为 31 a0 8c f 30 32 76
# (DEBUG)
(REPORT 0x203)
(ISOLATE PRESERVE)
(IDENTIFY *)
(VERBOSITY 2)
(CONFLICT FATAL) (IRQ FATAL) (MEM FATAL)
# 卡 1：序列标识符 6d ff ff ff 00 8c e
# Vendor Id CTL07f，序列号 (-1)，检查 xD6
# 版本 1.0。ANSI 字符串 --Creative VIB16 PnP--
# 逻辑设备 ID CTL043
# 设备支持厂商保留寄存器 @ 0x38
# 设备支持厂商保留寄存器 @ 0x3a
# 设备支持厂商保留寄存器 @ 0x3c
```

编辑下面的条目以取消注释所需的配置。请注意，任何范围仅给出第一个值；如果需要，可以进行更改。别忘记激活 (`ACTY`)。

```
(CONFIGURE CTL07f-1 LD 0
# ANSI 字符串 --Audio--
# 多选一时间，仅选择一种！
# 启动相关函数：允许优先
IRQ 5.
# 高电有效，边沿触发中断（默认）
(INT 0 (IRQ 5 (MODE=E))
# 第一个 DMA 通道 1。
# 仅位 DMA
# 逻辑设备不是总线主设备
# DMA 可以以字节计数模式执行
# DMA 不可以字计数模式执行
# 兼容模式下的 DMA 通道速度
(DMA 0 (CHANNEL 1))
# 逻辑设备解码 16 位 IO 地址线
# 最小 IO 基地址 0x0220
# 最大 IO 基地址 0x0220
# IO 对齐 1 字节
# 需要的 IO 地址数：16
# (IO 0 (SIZE 16) (BASE 0x0220))
# 结束相关函数
(NAME CTL00/-1[0] (Audio)
(ACTY)
# 返回所有到卡的“等待按键”状态
(WAITFORE)
```

## 硬件冲突与即插即用 247

```
# 逻辑设备不是总线主设备
# DMA 可以以字节计数模式执行
# DMA 不可以字计数模式执行
# 兼容模式下的 DMA 通道速度
(DMA 0 (CHANNEL 1))
```

你必须取消注释 `ACTY` 以设置卡。一旦此卡设置妥，可以使用以下命令加载 soundblaster 模块：

```
modprobe sb irq=5 io=0x220 dma=0
```

如果没有摇杆，就没有理由在 `isapnp.conf` 文件中启用它。

## isapnp.conf

这将设置你的卡，资源应该出现在相应的 `/proc` 文件中。每当启动时都需要将 `isapnp.conf` 文件复制到 `/etc` 目录。PCI 卡应该会自动设置。如果你看不到 PCI 卡已设置，可以输入：`cat /proc/pci`；否则你可能会耗尽资源。你的资源取决于你的架构，但 i386 PC 通常有 15 个中断：0–14。如果中断用尽，你可能想要寻找替代方案，例如在一个卡上有两个设备或通用串总线 (`USB`) 设备。

## 248 第 5 章：高级安装

## 认证目标 5.05

## PCMCIA

PCMCIA 设备可能会非常令人沮丧。问题是设备比驱动新，这通常可以通过下载最新的 pcmia 驱动并进行编译来解决。PCMCIA 在 Intel 和 Alpha 笔记本电脑上运行。Mac 笔记本也有有限的支持。以下是检测到的支持的 PCMCIA 控制器列表：

- Cirrus Logic PD6710, PD6720, PD6722, PD6729, PD6730, PD6732, PD6832

- Intel i8265sl B, C, DF DF，82092AA

- O2Micro OZ6729, OZ6730, OZ6832, OZ6833, OZ6836, OZ6860

- Omega Micro82C092G

- Ricoh RF5C296, RF5C396, RL5C465, RL5C466, RL5C475, RL5C476, RL5C478

- SMC 34C90

- Texas Instruments PCI11130, PCI1131, PCI1210, PCI1220, PCI1221, PCI1250A, PCI1251A, PCI1251B, PCI1450
