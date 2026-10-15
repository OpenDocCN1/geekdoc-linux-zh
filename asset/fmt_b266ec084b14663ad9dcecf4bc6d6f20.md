
我们建议阅读 `http://www.tld.org/HOWTO/Networking-Overview-HOWTO` 以及 `http://www.tld.org/HOWTO/Interfaces-HOWTO` 以及 `man` 手页。如果我们不需要网卡来执行测试，我们可以始终求助于 `dummy`；在这种情况下，不是被名为 `eth0`，而是为了在同一台电脑上配置多个网卡（这在用网关以及其他情况下很常见），有必要在启动过程中向内核输入参数，以避免设备之间的冲突。`/etc/network/interfaces` 中的所有服务都可以使用 `/etc/init.d/networking` 脚本启动，该脚本启动特定接口的网络服务，并停止它们。因此，对于上述配置，我们想要停止并重启 `eth0` 服务，我们按照如下步骤操作，可以使用 `ifconfig` 命令检查结果：

```
ifconfig eth0 link encap:Ethernet Waddr 00:01:02:b4:3a:61 inet addr:158.109.69.132 bcast:158.109.255.255 Mask:255.0.0.0 BROADCAST RUNNING MULTICAST MTU:1500 Metric:1 RX packets:3609683 dropped:0 overrun:221 frame:35938 errors:0 dropped:0 overruns:0 carrier:0 txqueue:10 RX bytes:148927310 (1 GiB) TX bytes:20116974 (19 MiB) Interrupt:5 Base address:0x94010 link: Loopback addr:127.0.0.1 Mask:255.0.0.0 UPBACK MTU:16436 Metric:1 RX packets:823 errors:0 dropped:0 overrun:0 frame:823 errors:0 overruns:0 carrier:0 txqueue:10 RX bytes:361919 (3.0 MiB) TX bytes:361919 (3.0 MiB)
```

CUPS（通用 Unix 打印协议）是一个模块化的打印系统，它使用 IPP（互联网打印协议）来处理队列。这是一个现代且复杂的系统，可以用于 GNOME 或 KDE 等桌面环境。此外，它还提供了维护传统的 BSD `lpr` 命令行系统的选项。

GNU/Linux 系统中打印系统的通用拓扑结构是客户端-服务器架构。服务器 CUPS 是一个守护进程类型的服务器，因此我们将其视为该类型进行处理。服务器的配置文件为 `/etc/cups/cupsd.conf`。在该文件中，我们可以根据需要配置任意数量的打印机。

要安装 cups 系统，我们必须运行命令：

```
# apt-get install cupsys cupsys-client cupsys-bsd printerconf fomatic-filters-ppds
```

最后一个包包含了 Adobe 的 PPD 文件（Postscript 打印机定义），CUPS 使用它们来定义打印机。

CUPS-PDF 是一个虚拟打印机，用于将文档打印到 PDF 文件。要在我们的系统中安装它，我们将运行以下命令：

```
# apt-get install cupsys-pdf
```

在 CUPS 中，配置打印机有两种方法。其中一种是通过 GNOME 或 KDE 桌面提供的工具。另一种是通过网站。在这两种情况下，我们都需要管理员权限来配置打印机。

## 打印文本文件

格式化程序（Formatters）是主要用于将文本格式的文件转换为 Postscript 格式的程序（从历史来看，Postscript 语言在打印领域有更广泛的实现）。这些程序非常有用，因为它们允许我们将帮助命令、配置文件等打印在纸上，以便于阅读。这些程序中的一个是 `mpage`（包含在同名的包中），另一个是 `enccript`（也包含在同名的包中），它比第一个更强大。下面给出了一个我们如何使用它的示例：

```
man man | mpage -2 -o lpr
```

使用这行命令，我们将 `man` 的输出重定向到 `mpage`，它将其格式化为每页两列，且不留页边距，然后我们将其输出重定向到打印机客户端 `lpr`：

```
endscript /etc/fstab -B -fTimes-Roman -r
```

通过这行命令，我们将打印 `/etc/fstab` 文件的内容，不带页眉，使用 Times-Roman 字体，大小为 7 且采用宽格式。

## 配置声卡

由于市场上大量的声卡，因此最有可能提供一份关于如何配置它们的描述。我们建议阅读 `http://tldq.org/HOWTO/Sound-HOW-TO/` 并访问 GNU/Linux 下最重要的声学项目网站：`http://www.opensound.com` 和 `http://www.alsa-linux.org`。

高级 Linux 音频架构（ALSA）是一个在 GNU 许可证下运行的项目，为 Linux 提供音频和 MIDI 设备。

现在我们讨论一下如果需要配置常用的声卡该如何操作：SoundBlasterPCI（芯片组 ES1371）。对于此类显卡，我们将如下所示使用 `lspci` 命令：

```
00:0d.0 Multimedia audio controller: Ensoniq 5880 AudioPCI (rev 02)
```
