

```
# cat > spooldir/.paprc
printername
^D
```

如果这样马上不起作用，你可以测试几件事。首先 cd 到 spool 目录（包含 .paprc 的那个目录）并使用

```
# papstatus
```

看看是否至少能与打印机通信（papstatus 命令位于你安装 Netatalk 的 bin 目录中）。如果 .paprc 文件不包含正确的名称，你会收到类似这样的错误：

```
printer:LaserWriter%: NBP Lookup failed
```

使用 -p 选项来查找正确的打印机。如果你完全不知道它是什么，尝试 nbplkup 命令（与 papstatus 命令在同一目录中；有关 nbplkup 的更多信息请参见第 4 章）：

```
# nbplkup :LaserWriter
```

你应该会得到提供 LaserWriter 服务的打印机列表及其 AppleTalk 网络号码。要列出不同的区域，将 @zone 加到 :LaserWriter 末尾（Netatalk 的 getzones 命令列出可用区域）。当然，你也可以在 Mac 上使用 Chooser——你想要的是 LaserWriter 8 服务。

一旦你得到打印机状态报告，例如 idle，尝试使用 pap 向打印机发送 PostScript 文件：

```
# pap file.ps
```

顺便说一下，一个相当有趣的选项 -c，告诉打印机此打印作业已经等待了很长时间，并尝试让该作业排在打印队列中其他作业之前。

相关手册页：psf (8), pap (1), nbp (1), getzones (1)

## SMB 打印机

如果你的打印机位于 Windows 机器上的 SMB 共享上，你可以使用 SAMBA 的 smbclient 程序打印到它。printcap 将看起来与 AppleTalk 的类似：

```
smbprinter|Printer on SMB Share:\
	:mx#0:sf:sh:\
	:sd=/var/spool/lpd/smb:\
	:lp=/var/spool/lpd/smb/null:\
:lf=/var/spool/lpd/smb/log:pw#80:\
:lf=/usr/local/lib/filters/smbprint:
```

同样，你需要创建一个新的 null 设备：

```
# mknod spoolidir/null c 1 3
```

其中 spoolidir 是 printcap 中 sd 指定的目录（如上例中的 /var/spool/lpd/smb）。

现在你需要正确设置过滤器。过滤器可能未安装在 /usr/local/lib/filters 中。例如在 Red Hat 6.1 中，你会在 /usr/bin 中找到它，如果你从源码安装 SAMBA，它默认也不会被安装（它在源码中，位于 examples/printing 子目录）。

过滤器只是一个 shell 脚本，需要在打印机 spool 目录中有一个 .config 文件；在本例中为 /var/spool/lpd/smb。

.config 文件如下所示：

```
server=SERVER
service=PRINTER
password="PASSWORD"
```

SERVER、PRINTER 和 PASSWORD 是 SMB 打印机的详细信息（你可能不需要打印密码，因此可以省略该行）。你可能需要更改文件的最后一行以反映你安装 SAMBA 的位置（源码中的示例假定你将其放在 /usr/local/samba/bin）。

> NOTE
> Red Hat 的 smbprint 与示例不同之处在于它将 SMB 日志文件设置为 /dev/null 而不是 /tmp/smb-print.log，并且给出了 smbclient 的正确 Red Hat 位置

你可以使用 smbclient 程序查找机器上可用的共享，如以下示例所示：

```
$ smbclient -L printserver
Password:
Domain=[FOO] OS=[Unix] Server=[Samba 1.9.18p10]
```

| Sharename | Type | Comment |
|----------|------|---------|
| printers | Printer | All Printers |
| hp160b | Printer | HP LaserJet 5Si in room 160b |
| ... | ... | ... |

要使其工作，打印机必须支持 PostScript。如果不支持，你需要在发送之前先通过 Ghostscript 处理文件。

## 5.4 Ghostscript for Non-PostScript Printers

大多数廉价打印机没有内置 PostScript 支持。这些包括大多数喷墨打印机和一些低端或老式激光打印机。然而，计算机通常可以解释和光栅化文件，最终将完成的位图发送到打印机。Ghostscript 由 Aladdin Enterprises 开发，是一款流行的免费解释器和光栅化器，随大多数 Linux 发行版提供，并且已配置了大多数或全部设备。

虽然 Ghostscript 支持许多打印机，但正确的选项和驱动程序并不总是显而易见，其文档杂乱无章，信息分散在多个文件中。某些选项——尤其是彩色喷墨打印机——会显著改变输出质量。例如，Epson Stylus Color 850 的默认值对于透明胶片来说并不理想，尽管打印机能够产生非常好的效果（理想情况下你希望打印头单向移动以减少条纹，并且可能使用与通常不同的抖动方式）。

你通常将 Ghostscript 集成到 Linux 的打印 spooling 系统中作为过滤器。PostScript 进入，打印机就绪数据出来并发送到打印机。过滤器通常是一个 shell 脚本，它解析一些参数然后调用 Ghostscript 并带上一些选项。以下是一个非常简单的脚本：

```
```sh
#!/bin/sh
/usr/bin/gs -q -dNOPAUSE -dBATCH -sOutputDevice=-- -r720x360 -sDEVICE=epson -
```
```

其核心当然是调用 Ghostscript（gs）。当你自定义过滤器时，你可能会在命令行上调用 gs 以避免指定打印过滤器所需的许多参数。

要将 foo.ps 的运行输出直接发送到并行端口，运行以下命令：

```
```sh
# gs -q -dNOPAUSE -dBATCH -sOutputDevice=/dev/lp0 -r720x360
- -sDEVICE=epson foo.ps
```
```

### Using the uniprint Driver

你通常希望按如下方式调用 uniprint 驱动程序：

```
```sh
# gs @name.upp -q -dNOPAUSE -dBATCH -sOutputDevice=device [files]
```
```

name.upp 实际上是 Ghostscript 库目录中的一个参数文件。例如，stc800.upp 是 Epson Stylus Color 800 的 720×720 dpi 普通纸模式。该文件本身是选项的庞大列表，设置 uniprint 为驱动程序并为此特定打印机调整参数。

