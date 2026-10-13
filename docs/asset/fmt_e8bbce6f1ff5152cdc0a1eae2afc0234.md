
# 硬件连接与设备
第三部分

> 如果你发现终端状态被搞乱了，通常可以使用命令 `stty sane` 和 `Ctrl+J` 来修复。请注意该命令是以 `Ctrl+J` 结尾的，而不是 Enter（等同于 `Ctrl+M`）。这是因为 `icrnl` 选项被关闭了。通过 `stty sane` 可以再次修复。GNU bash 无论如何都能处理未转换为 LF 的 CR，但某些程序不会。

如果这起不起作用，且屏幕看起来被弄乱了，请尝试输入 `echo`，按下 `Ctrl+V` 和 `Esc`，输入 `c`，然后按下 `Ctrl+J`。按下 `Ctrl+V` 可以让终端驱动程序传递下一个键而不进行处理。你可以通过输入 `reset` 并按下 `Ctrl+J` 获得类似的效果，但只有在安装了 `ncurses` 包的情况下才可以使用 `reset`。

程序可以关闭行驱动默认开启的处理；产生的行为（原始模式）允许程序从终端驱动程序读取未处理的输入（例如，CR 不会被映射为 LF），并且控制字符不会触发本节前面表格中描述的信号。`stty sane` 命令将把一切恢复正常。

## 串口通信

虽然 Linux 下最常用的终端接口是控制台驱动和由 `xterm`、`script` 和 `expect` 等程序驱动的伪终端，但原始的终端接口涉及串口通信。事实上，这仍然存在于与 xterm 窗口关联的伪终端上，它关联的波特率如“终端驱动程序”节所示。更改波特率没有实际效果，但对于真实的串口，波特率和许多其他参数有直接关系。与串口相关的设备节点由两个“组”组成，分别为 `/dev/cua*` 和 `/dev/tty#`。正如“使用调制调器”节所解释，这些串口硬件可用于入出串口通信。

## 配置串口端口

串口端口配置主要通过 `stty` 命令或直接通过程序使用 `termios` 手册概述的接口完成。`stty` 命令提供了 `termios` 提供的所有可能性；然而，串口硬件存在 `stty` 未解决的配置问题。`setserial` 命令允许为每个串口配置正确的 IRQ 设置以及标准 `termios` 规范未提供的极高速波特率。更多详细信息，请参考 Linux Serial-HOWTO 和 `serial` 的手册页。

## 使用调制调器

调制调器（“WinModems”之外）是非常灵活的设备。它们允许拨号终端访问和广域网，还允许发送和接收传真、语音邮件。之前提到的两组串口设备专门用于提供良好的调制调器支持，它们看起来如下：

```
$ ls -l /dev/ttyS* /dev/tua* /dev/mo*

crw-rw-- 1 root uucp 5, 64 Jan 1980 08:56 /dev/tua0

crw-rw-- 1 root uucp 5, 65 Jan 1980 08:56 /dev/tua1

crw-rw-- 1 root uucp 5, 66 Jan 1980 08:56 /dev/tua2

crw-rw-- 1 root uucp 5, 67 Jan 1980 08:56 /dev/tua3

lrwxrwxr-x 1 root uucp 4 Jun 14:16 /dev/modem -> /dev/ttyS0

crw-r-- 1 root 4, Nov 08 08:56 /dev/ttyS0

crw-r-- 1 root 4, 65 May 1995 24:55 /dev/ttyS1

crw-rw-- 1 root 4, 66 Jan 1980 08:56 /dev/ttyS2

crw-rw-- 1 root 4, 67 Jan 1980 08:56 /dev/ttyS3
```

`/dev/cua*` 设备用于输出，而 `/dev/ttyS*` 设备用于拨号。当你打开指向硬件的相应 `/dev/cua*` 时，此类进程将在 `/dev/ttyS0` 设备上等待 `open` 系统调用完成（即等待调制调器信号指示有入电电话）。因为在你在使用调制调器时，该路路上不能有入电电话，所以 `getty` 会锁定所有人，防止同时尝试使用同一个设备。

如今，网络互连远是调制调器最常用的用途。有很多资源可以帮助你配置机器通过调制调器访问互联网。请参见第 13 章中的“通过 PPP 连接网络”节。其他资源还包括 Red Hat PPP-Tips 文档（可以在 Red Hat 网站的支持部分找到）、EzPPP 包，以及 ISP-HOOKUP 和 PPP HOWTO。还有大量实用的 mini-HOWTO，每个都能帮助解决特定的问题；这些包括 Dial、Dip+Slip、Dynamic-IP-Hacks、IP-Masquerade、PPP-over-ISDN、PPP-over-minicom、Slip+proxyARP 以及 Tiny-Linux 的 mini-HOWTO。另一方面，如果你通过 UUCP 发收邮件，请参考 Linux Sendmail+UUCP mini-HOWTO。

## 通用 SCSI 设备

并非所有的 SCSI 设备都是硬盘、光驱驱动器或磁带驱动器。有些也是扫描仪、电子显微镜。内核没有抽象所有 SCSI 设备接口，因此允许用户通过通用 SCSI 设备访问硬件。SCSI 命令通过向设备写入数据来发送，结果通过从设备读取反馈。

## 光驱读取器

SCSI 设备是用于在介质上记录数据的设备。写入光盘有两个阶段：生成光盘镜像和将镜像写入介质。

CD-R（刻录光盘）表面只能写入一次，如果 `mkimage` 创建镜像。

## 测试镜像

正如你可以使用 `mkimage` 创建文件系统一样，你可以挂载之前描述的文件系统。

## 其他字符设备

还有其他几种字符设备，某些被频繁使用。例如，`/dev/null`。

## 控制终端设备 dev/tty

大多数进程都有控制终端，特别是当它们由用户交互启动时。控制终端（我将其称为 `/dev/tty`）用于与用户直接对话（例如提问）。一个例子是 `crypt`：

```
$ fmt diary.txt | crypt | mail -s /tty confidant@linux.com

$ 
```

在这里，`crypt` 命令打开了 `/dev/tty` 以获取密码。它无法使用标准输出提示和标准输入读取密码，因为这些正用于要加密的数据。

> 注意 当然，使用 `crypt` 发送邮件是不寻常的。更好的选择是 PGP。PGP 可以以 RPM 格式提供，可以在 http://ftp.replay.com/pub/linux/redhat 找到。

## 非串口鼠标

许多计算机使用总线或 PS/2 鼠标而不是串口鼠标。它的优点是空出了两个串口，但缺点是使用了另一个 IRQ。这些设备被 `gpm` 和 X Window 系统使用，但大多数其他程序并不与之直接交互。为这些鼠标配置系统非常简单；Red Hat Linux 安装过程几乎帮你处理好了。如果你对鼠标出现问题，应该阅读 `gpm` 的手册页和 Linux Mouse-HOWTO。

## 音频设备

Linux 系统上有几个音频相关的设备节点，包括：

- `/dev/sndstat` 指示音频驱动状态
- `/dev/audio*` 兼容 Sun 的音频输出设备
- `/dev/dsp*` 音频采样设备
- `/dev/mixer` 用于控制声卡的混音器硬件
- `/dev/music` 一个高层序列器接口

```
/dev/sequencer*
/dev/midi*
```
