
如果你的分区已经以写访问权限挂载，并且你尝试运行`dosemu`，该分区将打印警告消息并退出。这防止了 DOS 和 Linux 对你的磁盘进行独立写入，从而导致分区上的数据崩溃（95/8/11）。

如果安装了`LILO`，上述方法将无效。但是……

Thomas Mockridge (thomas@aztec.co.za) 报告（94/8/5）：

为了用`LILO`和`Stacker 4.0`启动`dosemu`，我做了一个小变通方法……

1. 将 MBR dd 到一个文件（或 Norton unity 等，512 字节）
2. 启动 dos（从全启动模拟器），执行`fdisk /mbr`，使用 (dos) `fdisk` 将你的 dos 分区设为活动状态。
3. 将新的 MBR 复制到文件。
4. 替换原始 MBR。
5. 将第二个 MBR 复制到`/var/lib/dosemu/partition.hda`？（取决于你的 dos 分区是哪个）
6. 设置`dosemu.conf`：

```
disk { partition "/dev/hda?" }
```

启动`dosemu`，搞定了！不需要`LILO`。

Holger Schemel (q99492@pbhrrz.uni-paderborn.de) 报告（94/2/10）：

在`dosemu`下配合`MS-DOS 6.0`运行良好良好。如果你遇到问题，必须手动编辑`DBLSPACE.INI`文件，并将磁盘器符更改你在`dosemu`中使用的盘器符。

Darren J Moffat (moffat@dcs.glia.ac.uk) 也报告了（94/3/27）：

……使用 6.2 版本可以实现！只需确保你手头有一个`LILO`启动盘，因为`dos 6.{2}`会更改启动硬盘的 MBR。

## 并行端口、串口和鼠标

### 4 个并行端口、串口和鼠标 

#### 4.1 端口访问在旧版本中可以工作，但现在不行了！

请阅读`../doc/README.port-io`和`../etc/config.dist`中的端口部分。

#### 4.2 端口访问在旧版本中更快！

你有机会记录端口访问，默认情况下，每次端口访问都会在`vm86`模式外产生一个异常。这需要一些时间。如果你不想记录端口访问，请在适当的端口语句中使用“`fast`”关键字。

#### 4.3 （微软兼容）鼠标驱动程序在哪里？

Tom Kimball (tk@pspare2.oc.com) 报告（93/11/24）：

几个人建议使用不同的鼠标驱动程序并推荐了一些。我发现了几个看起来运行良好的。

```
oak.oakland.edu:/pub/msdos/mouse/mouse701.zip (mscmouse)
oak.oakland.edu:/pub/msdos/mouse/gmous102.zip (gmouse)
```

通常你可以使用`dosemu`的内部驱动程序，在`winemu`之外的`dosemu`不需要任何额外的鼠标驱动（97/2/10）。

#### 4.4 为什么鼠标驱动不起作用？

Rejhon (mdrejhon@magi.com) 报告（95/4/7）：

如果你启动鼠标驱动程序后它一直挂起（实际上可能需要 30-60 秒），但如果你等待鼠标驱动程序启动的时间超过一分钟，请在鼠标驱动程序的命令行中指定鼠标所在的 COM 口。

#### 4.5 为什么 dosemu 占用了 COM4？

Rob Janssen (rob@peichl.ampr.org) 报告（94/3/24）：

根据 jmorriso@bogomips.ee.ub.ca，`dosemu`占用了`COM4` (`0x2e, IRQ 5`)。`0x2e`不在`ports{}`中，我必须在`dosemu`退出后运行`/dev/cuas3 irq 5`。

这是由你的 VGA BIOS 引起的。我发现开启 IO 端口跟踪并查看它在哪里被占用的。

禁用配置中的“`allowvideoportaccess on`”行，它就能正常工作。当你遇到视频出现问题时，尝试选择更具选择性的 IO 地址范围（例如 40-43）。

#### 4.6 我如何通过串口使用 dosemu？

#### 4.7 如何在串口线上进行 dosemu 和 shell 之间的切换？

John Taylor (taylor@pollux.cs.uga.edu) 报告（94/5/25）：

我正在运行`dosemu`，并希望在串口线上进行`dosemu`和 shell 之间的切换。我正在运行`dosemu`，并希望在串口线上进行`dosemu`和 shell 之间的切换。我正在运行`dosemu`，并希望在串口线上进行`dosemu`和 shell 之间的切换。我正在运行`dosemu`，并希望在串口线上进行`dosemu`和 shell 之间的切换。我正在运行`dosemu`，并希望在串口线上进行`dosemu`和 shell 之间的切换。我正在运行`dosemu`，并希望在串口线上进行`dosemu`和 shell 之间的切换。我正在运行`dosemu`，并希望在串口线上进行`dosemu`和 shell 之间的切换。我正在运行`dosemu`，并希望在串口线上进行`dosemu`和 shell 之间的切换。我正在运行`dosemu`，并希望在串口线上进行`dosemu`和 shell 之间的切换。我正在运行`dosemu`，并希望在串口线上进行`dosemu`和 shell 之间的切换。我正在运行`dosemu`，并希望在串口线上进行`dosemu`和 shell 之间的切换。我正在运行`dosemu`，并希望在串口线上进行`dosemu`和 shell 之间的切换。我正在运行`dosemu`，并希望在串口线上进行`dosemu`和 shell 之间的切换。我正在运行`dosemu`，并希望在串口线上进行`dosemu`和 shell 之间的切换。我正在运行`dosemu`，并希望在串口线上进行`dosemu`和 shell 之间的切换。我正在运行`dosemu`，并希望在串口线上进行`dosemu`和 shell 之间的切换。我正在运行`dosemu`，并希望在串口线上进行`dosemu`和 shell 之间的切换。我正在运行`dosemu`，并希望在串口线上进行`dosemu`和 shell 之间的切换。我正在运行`dosemu`，并希望在串口线上进行`dosemu`和 shell 之间的切换。我正在运行`dosemu`，并希望在串口线上进行`dosemu`和 shell 之间的切换。

#### 4.8 如何让并行端口工作？

## 5. 用户和非交互会话

### 5.1 我能否在多用户系统上使用 dosemu？

### 5.2 如何非交互式运行？

串口线进行`dosemu`和 shell 之间的切换。我正在运行`dosemu`，并希望在串口线上进行`dosemu`和 shell 之间的切换。我正在运行`dosemu`，并希望在串口线上进行`dosemu`和 shell 之间的切换。我正在运行`dosemu`，并希望在串口线上进行`dosemu`和 shell 之间的切换。我正在运行`dosemu`，并希望在串口线上进行`dosemu`和 shell 之间的切换。我正在运行`dosemu`，并希望在串口线上进行`dosemu`和 shell 之间的切换。我正在运行`dosemu`，并希望在串口线上进行`dosemu`和 shell 之间的切换。

## 6 dosemu 与网络

### 6.1 我如何从 dosemu 获取网络访问？

一如既往，优选通过 Linux 文件系统进行访问。请使用`Caldera`的网络工具或 Volker Lindecke 的`ncpfs`实用（`http://ftp.gwd.de:/pub/linux/misc/ncpfs`）挂载你的网络驱动器。如果你需要真实的`IPX`访问（例如运行`Novell`的`"syscon"`），请阅读`../doc/NOVELL-HOWTO.txt`。

## 7 dosemu 与 X-windows(97/2/9)

### 7.1 我可以在运行 X 的同时在控制台模式下运行 dosemu 吗？

Ronald Schalk (R.Schalk@uci.kun.nl) 报告 (94/1/17)

可以，没问题。只需记住使用`ctrl-alt-<Fn>`切换到虚拟控制台 (VC)，你就可以运行任何 Linux 应用程序（`dosemu`就是一个 Linux 应用程序）。我在一个会话中运行了几乎整个`WP5.1`。

[注意：如果 X 运行在`VC7`上，请使用`ctrl-alt-F7`切换到 X dosemu]。

### 7.2 可以在 X-windows 中以窗口形式运行 dosemu 吗？

如果你已安装 X 并且成功编译了`dosemu`并在 X-windows 之外成功运行了它，你应该能够立即运行`"xdos"`或`"dos -X"`来弹出一个`dosemu`窗口。如果这不起作用，请确保：
