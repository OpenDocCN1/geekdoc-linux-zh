
使用与 Web 服务器相同的协议。客户端应用程序使用 IPP 来查询打印机的功能、提交打印作业，以及查询或取消打印作业。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_515_0.png)

如果您已为连接到 Red Hat Linux 系统的打印机设置了 CUPS 打印队列（按照第一部分第 3 章中的说明操作），则可以从本地局域网上的 Windows XP 和 2000 系统在该打印机上打印。Windows 2000 和 XP 内置支持 IPP —— CUPS 使用的协议。要从 Windows XP 系统打印到 CUPS 打印队列，请在 XP 上添加网络打印机。在添加打印机向导中，选择“连接到 Internet 上的打印机或家庭或办公网络上的打印机”，然后输入 CUPS 打印队列的 URL。例如，对于 IP 地址为 192.168.0.8 的 Red Hat Linux 主机上名为 HPLaserJetRoom210 的 CUPS 打印队列，我输入以下 URL 作为打印队列：

```
http://192.168.0.8:631/printers/HPLaserJetRoom210
```

作为 Red Hat Linux 用户，您使用客户端程序 —— lp 或 lpr —— 通过 TCP/IP 网络连接将待打印文件发送到名为 cupsd 的打印调度程序。cupsd 调度程序随后将文件排队，根据其文件扩展名（如 .txt 或 .ps）进行处理，然后逐个发送到打印机。借助各种配置文件，cupsd 调度程序知道该怎么做，以确保文件 —— 无论是文本文件还是图像文件 —— 都能正确打印。

虽然您通常只在 PC 上连接一台打印机，但 CUPS 打印系统的优点之一是可以打印到网络上另一系统连接的打印机。打印到远程打印机的方式与打印到本地打印机相同：本地 lp 或 lpr 程序只需将文件发送到远程系统的 cupsd 调度程序。

## 使用 lp 命令打印

您可以使用 lp 或 lpr 命令打印文件。例如，要打印文件 /etc/inittab，请在终端窗口中输入以下内容：

```
lp /etc/inittab
```

lp 命令通过将文件和适当的控制信息发送到 cupsd 打印调度程序来排队打印作业。默认情况下，cupsd 打印调度程序接受待打印文件，将其保留在打印队列中，并将其转发到默认打印机（如果默认打印机连接到网络上的远程系统，则转发到另一系统）。默认打印机由 CUPS 配置文件 /etc/cups/cupsd.conf 中的 <DefaultPrinter queuename> 条目标识（其中 queuename 是打印队列的名称）。

## 使用 lpq 检查打印队列

您可以在简单 lp 命令上添加一些选项。如果定义了多个不同的打印队列，您可以使用 -d 选项指定打印作业的目的地。例如，要将打印作业发送到名为 HPLaserJetRoom210 的惠普 LaserJet 打印队列，您应输入以下命令（打印队列名称出现在 /etc/cups/printers.conf 文件中）：

```
lp -d HPLaserJetRoom210 testprint.ps
```

如果您错误地打印了大文件并希望在浪费太多纸张之前停止打印作业，可以使用 lpq 命令查看当前打印作业，然后取消该大打印作业。以下是我在向 HPLaserJetRoom210 打印队列提交文件后输入 lpq 时得到的典型打印作业列表：

```
HPLaserJetRoom210 is ready and printing
Rank Owner Job File(s) Total Size
active root 2 testprint.ps 15360 bytes
```

lpq 命令显示作业编号（2）和我正在打印的文件名称（testprint.ps）。

## 使用 cancel 取消打印作业

要从打印队列中删除作业，请使用 cancel 命令。例如，要删除打印作业 2，请输入以下命令：

```
cancel 2
```

您可以使用以下 lprm 命令获得相同结果：

```
lprm 2
```

如果您急于取消迄今为止提交的所有打印作业，请按如下方式使用 -a 作为 cancel 的参数：

```
cancel -a
```

![](img/a7eec43a54473e95dc5ea333fecf1bd7_516_0.png)

## 使用 lpstat 检查打印机状态

要查看打印作业的状态，请使用 lpstat 命令。以下是 lpstat 命令的典型输出：

```
lpstat
HPLaserJetRoom210-2 root 15360 Wed 25 Jan 2003 04:25:48 PM EST
```

## 控制打印队列

输出的第一字段显示队列名称，后面附加了作业编号（该编号标识打印作业）。您需要该作业编号来取消打印作业。

要查看连接到系统的打印机名称，请使用 `lpc status` 命令。在我的系统上，`lpc status` 命令显示如下：

```
lpc status
HPLaserJetRoom210:
    printer is on device 'parallel' speed -1
    queuing is enabled
    printing is enabled
    no entries
    daemon present
```

请注意，此打印机的排队和打印均已启用。最后一行告诉您 `cupsd` 守护进程（始终运行的服务器）正在运行并且可用于处理打印作业。

您可以使用 `accept` 和 `reject` 命令启用或禁用打印队列的排队。例如，要停止为 `HPLaserJetRoom210` 打印机排队进一步的打印作业，我输入

```
reject HPLaserJetRoom210
```

此命令禁用为此打印机排队作业。如果有人尝试使用 `lp` 命令发送打印作业，用户会收到如下错误消息：

```
lp: unable to print file: server-error-not-accepting-jobs
```

如果您希望允许排队打印作业，但希望启动或停止打印，请使用 `enable` 和 `disable` 命令。当您禁用打印时，用户可以提交打印作业，但直到您再次启用打印之前不会打印任何内容。例如，我用来禁用 `HPLaserJetRoom210` 打印机打印的命令如下：`disable HPLaserJetRoom210`

![](img/a7eec43a54473e95dc5ea333fecf1bd7_517_0.png)

如果您尝试打印，但打印机似乎没有输出，请使用 `lpc status` 命令检查打印机状态，并确保 `cupsd` 调度程序存在且排队和打印均已启用。要允许排队打印作业，请使用 `accept` 命令，要开始打印，请使用 `enable` 命令。

## 第 6 章：升级和定制内核

### 本章内容

- ✔ 使用 Red Hat 内核 RPM 升级
- ✔ 配置内核
- ✔ 构建新内核
- ✔ 构建和安装模块
- ✔ 安装内核并设置 GRUB

Linux 如此令人兴奋的一个原因是许多程序员不断改进它。例如，一些程序员编写驱动程序以添加对新硬件的支持，例如新的声卡或新的网络卡。所有这些创新都以 Linux 内核的新版本形式呈现给您。

虽然您不必在每次有新版本可用时都升级或修改 Linux 操作系统 —— 内核 —— 但有时您必须升级，仅仅因为新版本纠正了一些问题或更好地支持您的硬件。另一方面，如果较早的内核版本已包含您所需的一切，则无需急于升级。

有时即使没有修复或增强，您也可能想要重建内核。随附 DVD 上的 Linux 内核是通用的，并使用模块来支持所有类型的硬件。您可能希望构建一个新内核，该内核仅链接到您系统上安装的设备的驱动程序。特别是，如果您有 SCSI 硬盘，您可能希望创建一个支持您的 SCSI 适配器的内核。根据您的需要，您可能还希望更改一些内核配置选项，例如创建特定于您的处理器的内核（而不是通用的 Intel 386 处理器）。

在本章中，我将解释如何使用内核 RPM 升级内核，以及如何重建和安装新的 Linux 内核。

## 使用 Red Hat 内核 RPM 升级

Red Hat 以 RPM 文件的形式分发所有软件更新，包括内核的新版本。要下载和安装内核 RPM，请按照以下步骤操作：

- 1. **使用 Web 服务器从 Red Hat 的 FTP 服务器下载内核 RPM 文件（我在下一节中解释了详细信息）。**
- 如果您想重建内核，您必须下载与新内核版本对应的 `kernel-source` RPM。
- 2. **使用 `rpm -i` 命令安装 RPM。**
- 3. **通过运行 `/sbin/mkinitrd` 命令创建新的初始 RAM 磁盘。**
- 4. **重新配置 GRUB 以启动新内核。**
- 5. **通过重新启动系统来尝试新内核。**

我在接下来的几节中进一步描述这些步骤。

### 下载新的内核 RPM

Red Hat 在其 FTP 服务器或 www.redhat.com/download/mirror.html 上列出的镜像站点之一以 RPM —— 包 —— 的形式提供软件更新。更新按 Red Hat Linux 版本号组织在目录中。例如，Red Hat Linux 9 for Intel x86 系统的任何更新都位于 9/en/os/i386 目录中。使用 Web 浏览器（例如 Mozilla）访问 FTP 站点并下载该站点上可用的任何内核 RPM。

### 安装内核 RPM

要安装内核和模块，请按照以下步骤操作：

- 1. **以 root 身份登录。**
- 2. **使用 `cd` 命令将目录更改为 RPM 文件（即从 Red Hat FTP 服务器下载的文件）所在的位置。**
- 3. **输入以下命令以安装内核 RPM：**
  `rpm -ivh kernel*.rpm`

您只有在想要构建新内核时才需要安装 `kernel-source` RPM。
