
```
StartEntry: DeskJet500
GSDriver: cdj500
Description: {HP DeskJet 400/500C/520/540C}
About: {
  This driver supports the HP inkjet printers which have \
color capability with an optional color cartridge. \
  If your DeskJet can use EITHER a B&W cartridge or \
  a color cartridge, but not both simultaneously, \
  this driver may work for you. \
  Ghostscript supports several optional parameters for this driver: see the document `devices.doc' in the ghostscript directory under `/usr/doc. \
}
Resolution: {300} {300} {}
BitsPerPixel: {3} {Normal color printing with color cartridge}
BitsPerPixel: {8} {Floyd-Steinberg B&W printing for better greys}
BitsPerPixel: {24} {Floyd-Steinberg color printing (best, but slow)}
EndEntry
```

要为该系列打印机添加简单的黑白打印选项，请在 `Resolution:` 条目后添加 `BitsPerPixel` 条目：

`BitsPerPixel: {1} {Normal B&W printing with black cartridge}`

**注意**

您可以拆分打印机过滤器定义，为不同的打印机创建自定义条目，或者使用 `StartEntry:` 和 `EndEntry` 关键字之间的正确语法创建自己的打印机条目，这些关键字提供打印前选项以及由 `Ghostscript` 解释器对 `PostScript` 文档进行翻译。包含一个仅限单色的 `DeskJet500` 条目，但您可以重命名条目以更具体地描述打印机类型，并重命名安装在 `LAN` 上的打印机条目。尽管 `printerdb` 文件中有指针，但有关 `Ghostscript` 选项的详细信息可以在 `/usr/share/doc/ghostscript-5.50` 中的 `devices.htm` 文件中找到。

如您所见，`printtool` 可以添加、编辑或删除打印机。另一个不错的功能是能够给排队文件分配大小限制，如果您磁盘空间有限或不希望用户填满文件系统，这可能会很有帮助。如果您有一台打印机，需要更换打印墨盒才能打印黑白或彩色页面，您会发现 `printtool` 不可或缺。试一试吧！

虽然当前版本的 `printtool`，`3.48`，每次您进行更改时都会创建 `/etc/printcap` 数据库的备份，但当您删除打印机时，它不会删除相关的打印机队列或 `spool` 目录。

## Linux 打印命令

当然，您不必使用 `printtool` 命令来设置打印机。您可以直接编辑 `/etc/printcap`，但您应该知道自己在做什么，并理解 `printcap` 的格式。此文件是系统本地和网络打印机的 `ASCII` 数据库，详细描述了每台打印机的功能。有关完整详细信息，请参见 `printcap` 的 `man` 页面了解命令，以及 `termcap` 的 `man` 页面了解文件的布局。

实际上，你可以为每台打印机配置多个条目，这在需要打印不同尺寸的纸张、通过更换墨盒来打印彩色或黑白文档，或者更改打印机纸盒时非常有用。

旧版本的 `Red Hat Linux` 使用的是 `4.3BSD` 行式打印机（`line-printer`）作业队列系统。该系统包含多种特性及相关程序，用于支持后台打印、多个本地和网络打印机，以及对打印机和排队文档的控制。

旧版打印机作业队列系统使用的主要文件如下：

- `/etc/printcap`
- `/usr/sbin/lpd`
- `/usr/sbin/lpc`
- `/usr/bin/lpr`
- `/usr/bin/lprm`
- `/usr/bin/lpq`
- `/dev/printer`

这些文件提供了从命令行发起和控制打印作业所需的基本功能。有关你在打印过程中可能发现有帮助的其他 `Linux` 命令的精选列表，请参阅表 `19.3`。

`Red Hat Linux` 现在使用 `Patrick Powell` 开发的 `LPRng` 打印作业队列软件，它源自 `4.3BSD` 发布版，但已从头重写。与之前的打印机作业队列软件相比，`LPRng` 提供了一系列优势和特性，例如基于 `GNU GPL` 分发、向后兼容、安全性、诊断功能以及单队列支持多打印机。除了之前列出的命令外，`LPRng` 还使用以下文件：

- `/etc/lpd.conf`
- `/usr/sbin/checkpc`
- `/etc/lpd.perms`
- `/usr/bin/lpstat`

这些额外文件用于站点特定设置、检查或修复 `LPRng` 的安装、设置用户权限，以及报告打印机状态。

当你首次启动 `Linux` 时，位于 `/etc/rc/init.d/` 下的 shell 脚本 `lpd` 会启动 `lpd`（打印机守护进程）。该程序作为一个打印机服务器在后台运行，等待打印请求。当检测到打印队列中有请求时，服务器将连接到指定的打印机，并通过正确的打印机过滤器传递文档流。

打印请求通过 `lpr` 命令启动。例如，以下命令行会将你的文档打印到 `/var/spool/lpd/lp` 目录下的文件中，使用的打印机名为 `lp`：

```bash
# lpr -Plp myfile.txt
```

其他打印作业队列命令可以帮助你跟踪请求。如果你正在打印一个大文档或多个较小的文件，可以使用 `lpq` 命令查看正在运行的打印作业列表。例如，要一次性向默认打印机打印多个文件，请使用以下命令：

```bash
# lpr *
```

**注意**

`LPRng` 系统一次只允许打印 `52` 个文件。如果你想打印更多的文件，你需要将打印作业拆分。

在该命令之后执行以下操作：

```bash
# lpq
```

这将输出以下内容：

```text
Printer: lp@thinkpad
Queue: 1 printable job
Server: pid 3631 active
Unspooler: pid 3632 active
Status: processing `ff6E30@thinkpad.home.org`, size 1309, format `f', IF filter `filter' at 17:40:52.610
        Owner/ID            Class Job Files             Size Time
 active  root@thinkpad+630  A      630 adsl,amd,anacron,apm 14542 17:40:51
```

这显示了相当多的信息，但需要注意的是作业编号（本例中为 `630`）。如果你想停止前面的打印作业，请使用 `lprm` 命令，后跟作业编号，如下所示：

```text
# lprm 630
Printer lp@thinkpad:
        checking perms `root@thinkpad+630'
        dequeued `root@thinkpad+630'
```

这表明 `lprm` 已移除队列文件并停止了该作业。要禁用或启用打印机及其队列、重新排列打印作业顺序或查看打印机状态，你可以从命令行或以交互方式使用 `lpc`，但你必须以 `root` 或超级用户身份登录（通过 `su` 命令）。

`LPRng` 的 `lpc` 命令非常全面，与传统的 `lpc` 命令相比，提供了对系统和网络打印更多的控制。该命令可用于启动或中止打印服务器、禁用或启用打印排队、保留或释放打印作业，甚至将打印作业移动到不同的打印机！在命令行中这样启动 `lpc`：

```bash
# lpc
```

要查看有关命令关键字和语法的内置帮助，请输入 `help` 或按 `?`，如下所示：

```text
lpc> help
```

按下 `Enter` 后，你将看到几页关于 `lpc` 的 `30` 个不同命令的帮助文本。`LPRng` 的 `lpstat` 是一个更简化的命令。像这样使用该命令：

```text
# lpstat
Printer: lp@thinkpad
Queue: no printable jobs in queue
Status: subserver pid 3632 exit status `ABORT' at 17:43:05.111
```

如果有等待的打印作业，你将看到一份作业列表，以及类似由 `lpstat` 返回的信息。
