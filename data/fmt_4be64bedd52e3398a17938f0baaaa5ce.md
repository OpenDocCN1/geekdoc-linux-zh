
`setserial /dev/tty50 uart none`

通过将硬件类型（UART）设置为 `none`，该命令禁用了指定的端口。

> 注意：UART 代表**通用异步收发输传输器**（Universal Asynchronous Receiver Transmitter）。UART 负责串口链路的底层实现，使得 CPU 只需要关注提供待发送的字节和处理接收到的字节即可。

在本章的剩余部分，我们建议你使用 Laddie CD 启动 Laddie 设备并跟随这些练习（ejercicios）。启动 CD 后，退出帧缓冲区 UI（按 ESC），并使用空密码登录 root。在 `laddie:~` 提示符下执行以下命令，以验证端口 COM1 是否已正确配置：

```
laddie:~# setserial /dev/tty50
```

你应该能看到以下输出：

```
/dev/ttySO, UART: unknown, Port: 0x03f8, IRQ: 4
```

UART 类型为未知（unknown），这意味着该端口是可用的。

## 创建设备文件

你可能记得在上一章中使用设备文件 `/dev/fb0` 来暴露帧缓冲区功能。同样，我们必须提供一个设备文件来暴露 `dev/lirc_serial` 功能。以下代码创建了主设备号为 61、从设备号为 0 的字符设备文件 `/dev/lirc`，这符合 lirc 驱动的要求。

```
mknod /dev/lirc c 61 0
```

使用 Laddie CD，通过以下命令验证 `/dev/lirc` 设备文件是否存在：

```
laddie:~# ls -1 /dev/lirc
```

你应该能看到如下输出：

| crw------| 1 root root 61, 2007-01-27 08:03 /dev/lirc |

这表示该文件代表一个字符设备，它 ① 对 root 可读写，② 主设备号为 61，且 ③ 从设备号为 0。

## 将 lirc_serial 模块加载到内核

在串口可用且设备文件就绪后，我们能够使用 `modprobe` 命令加载 `lirc_serial` 设备驱动：

```
modprobe lirc_serial
```

要验证 `lirc_serial` 设备驱动已加载，请执行操作：

```
laddie:~# lsmod grep lirc
```

你应该能看到类似这样的输出：

| lirc_serial 13152 1 |
| lirc_dev 14804 1 lirc_serial |

第一列显示已加载的模块；第四列显示依赖关系。在这里我们看到 ① `lirc_serial` 模块依赖于 ② `lirc_dev` 模块。

如果我们想为接收器使用不同的端口 COM1，我们将通过 `modprobe` 命令为 `lirc_serial` 驱动提供额外的参数。要指定 COM2，我们将使用命令 `modprobe lirc_serial irq=3 io=0xf8`。COM3 和 COM4 的默认 irq 和 io 值分别为 (4, 0x3f8) 和 (3, 0xe28)。

## 测试 lirc_serial

现在我们已经验证 `lirc_serial` 驱动已加载，我们使用 Laddie CD 来测试 IR 接收器硬件。我们首先回顾一下想要测试的内容。记得我们的 LIRC 接收器提供的信号如图 12-14 所示（至少在索尼电视音量命令的情况下）。

![img/a28f005634867270fea0cf7891_235](Figure 12-14: 索尼电视音量命令波形)

`lirc_serial` 内核驱动的作用是测量该信号中间隙（spaces）和脉冲（pulses）的定时。这里显示的波形符合该协议。`lirc_serial` 内核驱动负责测量此信号中的间隙和脉冲定时。此处波形符合该协议。驱动包含一个中断处理程序，每当 DCD 发生变化时就会调用它。驱动使用定时器测量间隙和脉冲，然后通过 `/dev/lirc` 文件发射这些信息。在每个字中，第 0 到 23 位指定间隙，第 24 位是脉冲，第 25 到 31 位为 0。驱动设计为处理任何协议，但这里是 Sony 协议。为了测试 `lirc_serial` 设备驱动，我们需要在按下遥控器时产生这些脉冲。在访问 `/dev/lirc` 设备文件之前，我们需要确保它没有被其他进程占用。在 Laddie 提示符下执行以下命令：

```
laddie:~# laddie stop

laddie~# kill $(pidof lirc)
```

第一个命令后，我们需要等待 Laddie 停止。在第二个命令中，`pidof` 函数提供进程 ID，`$(...)` 结构为 `kill` 命令提供参数，从而终止该进程。我们现在可以访问 `/dev/lirc` 文件进行测试。正如我们在上一章中所看到的，我们可以使用 `cat` 命令访问输出。我们不想直接将 `/dev/lirc` 的输出传到控制台，因为某些输出会被解释为控制字符，导致控制台进入异常状态。一种方法是将输出管道给 `hex` 工具，它会将二进制数据转换为十六进制。输入以下命令：

```
laddie:~# cat /dev/lirc | hexdump
```

现在，DCD 引脚上的任何脉冲都会被 `lirc_serial` 驱动测量，通过 `cat` 命令驱动 `/dev/lirc` 文件，并通过 `hexdump` 以十六进制显示。为了产生此类脉冲，将 IR 接收器连接到 COM1 端口，将遥控器指向 IR 检测器/解调器并按下按钮。如果一切正常，你应该看到如下输出：

```
000000 df67 0091 011b 0000 04f6 0100

000010 0216 0000 04d4 01f0 0000 026e 0100

000020 02d3 0000 028a 01f0 0000 04f7 0100

000030 01f0 0000 02a1 01f0 0000 02a0 0100

000040 01f0 0000 04fc 01f0 0000 02a0 0100

000050 01f0 0000 0283 0118 0000 0289 0100
```

这就是我们通过短按下为索尼电视编程的通用遥控器上的音量键产生的输出。

幸运的是，LIRC 软件包包含一个名为 `mode2` 的工具，它可以理解 `lirc_serial` 驱动的输出并将其显示为脉冲和间隙计时数据。

按下 CTRL-C 终止上一个命令，并执行以下命令：

```
laddie:# mode2
```

现在按下按钮的同时将红外遥控器指向接收器。`mode2` 命令读取 `/dev/lirc` 的输出，解析 23 位计时数据和 1 位脉冲或间隙指示，并产生一系列脉冲和间隙计时信息。例如，当我们用单个 TV 音量命令刺激红外接收器时，我们观察到了以下间隙和脉冲计时序列。

```
laddie:-# mode2 space 5668 pulse 1265

space 5794213 pulse 663 space 517

pulse 2471 space 494 space 663

space 496 space 1260 space 516

pulse 1282 space 497 pulse 633

space 546 pulse 685 space 546

pulse 1263 space 518 space 639

space 517 space 661 space 496

pulse 611 space 515 space 682
```
