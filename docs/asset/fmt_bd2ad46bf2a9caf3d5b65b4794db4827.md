
在我的情况下，正如我之前提到的，我有一个带有 USB 接口的 iPAQ。由于我使用的是 USB 接口，我必须遵循一些特殊说明，并使用 `modprobe` 来启用 iPAQ USB 串口模块。

以下三个命令必须由 root 用户执行。

```bash
$ /sbin/modprobe ipaq
```

下一步是配置 Synce 使用正确的端口进行连接。这是通过 `synce-serial-config` 命令完成的。在我的情况下，我连接的是 USB 端口 0，因此需要的命令是：

```bash
# synce-serial-config ttyUSB0
```

识别端口后，启动检测连接的守护进程的命令是：

```bash
# synce-serial-start
synce-serial-start is now waiting for your device to connect
```

如果有需要，可以将此添加到系统启动项中。

接下来，你需要设置任何将与你的设备同步的用户来运行 `dcc`。此命令必须从用户账户运行。如果需要，可以将该命令添加到用户的 `.login` 文件中。

```bash
$ dccm
```

完成上述步骤后，你应该能够通过 PC 上的 Windows CE 活动同步（Active Synch）图标开始手动同步。

如果你遇到困难，特别是在使用 USB 连接时，以下 Source Forge Sync 网页非常有帮助。

```
http://synce.sourceforge.net/synce/usb_linux.php
```

此外，检查或查看（tail）`/var/log/messages` 文件以获取来自 `synce-serial-start` 和 `dccm` 命令的错误。

### 8.7.3 Synce 工具

在你 Windows CE 设备与 Linux 桌面设备之间成功建立同步连接后，有多种命令行工具可对你的设备执行各种操作。

#### pstatus

允许获取连接状态以及有关你已连接设备的信息。

示例：

```
$ pstatus
Version
===
Version: 3.0.11171 (Merlin: Pocket PC 2002)
Platform: 3 (Windows CE)
Details: ""

System
===
Processor architecture: 5 (ARM)
Processor type: 2577 (StrongARM)
Page size: 0x1000

Power
===
ACLine: 01 (Online)

Status for main battery
================
Flag: 1 (High)
LifePercent: 100%
LifeTime: Unknown

Status for backup battery
================
Flag: 1 (High)
LifePercent: 100%
LifeTime: Unknown

Store
===
Store size: 48922624 bytes (46 megabytes)
Free space: 15883432 bytes (15 megabytes)

Memory for storage: 49061888 bytes (46 megabytes)
Memory for RAM: 17145856 bytes (16 megabytes)
```

获取 Windows CE 设备上的文件列表。

```
$ pls

Archive 315 Tue 04 Jan 2005 08:33:45 EST

BatmanBeginsMovi56.asxArchive 849 Tue 04 Jan 2005

08:32:12 EST EnjoythisLiveper0k.asx
```

#### Archive

```
Playlist.as 898 Sun 01 Feb 2004 09:48:44 EST

Archive 970420 Sun 08 Jun 2003 10:28:56 AM EDT

Recording1.wav 109631 Thu 22 Nov 2001 08:00:48 EST

More.pdf 399120 Fri 16 Nov 2001 08:00:26 EST

Reader User Guide.pdf Directory Tue 20 Aug 2002 10:14:18 EDT

Annotations/ Directory Mon 03 Sep 2001 08:00:01 AM EDT

Business/ Directory Mon 03 Sep 2001 08:00:01 AM EDT

Personal/ Directory Templates/ Mon 03 Sep 2001 08:00:00 AM EDT
```

#### mkdir

将在你的 WinCE 设备上创建一个目录（或文件夹）。在下面的示例中，从 Linux 桌面在 Windows CE 设备上创建一个名为 patrick 的文件夹，然后我使用 `pls` 列出 Windows CE 设备上的文件和文件夹。

```
$ mkdir

$ pls

Directory patrick/

Wed 05 Jan 2005 08:34:13 PM EST

Archive 315 Tue 04 Jan 2005 08:33:45 PM EST

BatmanBeginsMovi56.asxArchive 849 Tue 04 Jan 2005

08:32:12 PM EST EnjoythisLiveper0k.asx
```

## 病毒与垃圾邮件防护

桌面电脑的两个最大敌人是垃圾邮件和病毒。这两个反派让所有管理员都非常头疼。使用 Linux 桌面系统的好处是 Linux 病毒非常少；然而，垃圾邮件仍然是一个反派！Linux 有许多工具可以对付这两个大恶棍之徒；有些关键配置可以帮助保护你的系统免受病毒侵害。病毒最常见的入侵方式是通过电子邮件，因此本章将集中于如何让 Linux 机器的电子邮件安全。

## 9.1 如何阻止垃圾邮件？

我们必须承认，垃圾邮件是一个巨大的痛苦。为了对抗垃圾邮件，Linux 盒子里有多种工具可用；这些工具可以在用户级或全系统级实现。某些工具会从被标记为垃圾邮件的消息中学习，而另一些则需要手动控制。最广泛使用的工具之一是 SpamAssassin。SpamAssassin 将所有功能和学习控制整合在一个高度可配置软件包中。该工具允许你使用远程服务以及其自身的规则来判断邮件是否为垃圾邮件，你还可以使用其他邮件传输程序的 procmail 子系统来对其进行全局配置。由于 sendmail 是最常用的邮件传输程序，我们将介绍它的用法。

如果正在使用运行 SpamAssassin 的 IMAP 服务器，否则 SpamAssassin 对通过这些工具组合交换的邮件将不起作用。SpamAssassin 设计为通过 procmail 子系统作为系统邮件传输程序的一部分，该子系统用于用户本地的电子邮件投递，或者使用其他机制可以作为系统级邮件过滤器（milter）。如果邮件被投递到服务器本地，milter 可以在调用其他传输机制（包括 POPmail 和 IMAP）之前找到垃圾邮件。因此，SpamAssassin 可用于通过 IMAP 或 POPmail 服务器获取邮件的 Outlook 客户端。SpamAssassin 的额外优势是它是作为许多 Linux 版本的一部分自带的。要使用 SpamAssassin 处理本地投递的电子邮件，你可以如下所示使用 procmail：

创建 `.forward` 文件：

```
"IFS=' '& exec /usr/bin/procmail -f - || exit 75 #user"
```

创建 `.procmail` 文件：

```
:0fw: spamassin.lock

* <256000

| spamassin
```

输入这些指令后，本地 sendmail 投递代理将运行 spamassin 或 sporc（基于服务器）程序，并将你所有的邮件标记为垃圾邮件（spam）或正常邮件（ham，不是垃圾邮件，而是良好的邮件）。由于在某些情况下，合法邮件会被错误标记为垃圾邮件，因此可能不将所有垃圾邮件重定向到收件箱更好。你可以向 `.procmail` 文件添加以下命令，将所有垃圾邮件转发到你你不感兴趣的其他文件夹中。然而，这种行为可能最好留给你的邮件客户端处理。

```
:0

* ^X-Spam-Level: \*|\*|\*|\*|\*

spam-folder
```

```
:0

* ^X-Spam-Status: Yes

possible-spam-folder
```
