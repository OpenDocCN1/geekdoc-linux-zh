

## 注意

有关通过服务器消息块（SMB）Windows 网络设置其他服务的信息，请参阅第 17 章“Samba”。您需要更详细的指导，说明如何从 Red Hat Linux 系统打印到 Windows 95/98/NT 系统中的打印机，或从 Windows 95 打印到 Linux 打印机吗？请访问 http://www.redhat.com/support/docs/tips/Samba-Tips/Samba-Tips.html。您还可以通过位于 http://samba.anu.edu.au/samba 的中央 Samba Web 页面找到有关 Samba 的最新信息。

再次，在您填写局域网打印机信息并点击“确定”后，printtool 会在 /etc/printcap 中创建一个打印机条目。该打印机条目可能类似于以下内容：

```
##PRINTTOOL3# SMB cdj500 300x300 letter { $DeskJet500 8 1\nlp0:\n\t:sd=/var/spool/lpd/lp0:\n\t:mx#0:\n\t:sh:\n\t:af=/var/spool/lpd/lp0/acct:\n\t:lp=/dev/null:\n\t:if=/var/spool/lp0/filter:\n
```

## 注意

如果您未为 SMB 打印机选择打印过滤器，则 /etc/printcap 条目中指定的 smbprint 过滤器与 /usr/bin 目录下的 smbprint 命令完全相同！此外，当您使用 printtool 为 Red Hat Linux 创建 SMB 或 NCP 打印机时，您会收到一个警告。当您使用 printtool 创建 SMB 打印机条目时，会在打印机的 /var/spool/lpd 目录（或 spool 目录）下创建一个名为 .config 的文件。该文件包含共享（服务器）名称、打印机用户名、工作组和密码，且未加密，系统中的任何人都可以读取它。

在您可以打印到 SMB 打印机之前，您应该拥有一个活动的网络连接。然后，您可以使用 lpr 命令的 -P 选项，后跟新局域网打印机的名称和您要打印的文件名。使用 /etc/printcap 中已定义的打印机 lp0 条目，使用 lpr 打印名为 myfile.txt 的文件：

```
# lpr -Plp0 myfile.txt
```

您还可以使用 **smbprint** 命令，它是 Andrew Tridgell 的 Samba 软件包中程序集的一部分，来打印到局域网打印机。**smbprint** 命令是一个 shell 脚本，位于 /usr/bin 目录下，使用 **smbclient** 命令将文件发送到共享打印机。事实上，当使用 **printtool** 创建 SMB 打印机条目时，**smbprint** 的一个修改版本被用作 Red Hat 的打印机过滤器。有关 **smbclient** 的详细信息，请参见其 man 页面。

## 本地打印机

Red Hat 的 **printtool** 可以轻松快速地设置直接连接到计算机的并口打印机。为此，运行 **printtool**，点击 **Add**（添加）按钮，选择 **Local**（本地），然后点击 **OK**（确定）。

然后 Linux 会尝试加载并口打印模块 **lp**，并出现一个 **Info**（信息）对话框框（如图 19.6 所示）。该对话框会告诉您检测到哪些并口打印机设备。如果 **printtool** 报告未找到设备，请检查 /etc/modules.conf 条目中 **lpparport** 驱动程序的情况。

![](img/6bd28cbdb5cafd4e9d424d0c660b83ee_671_0.png)

![](img/6bd28cbdb5cafd4e9d424d0c660b83ee_671_1.png)

点击 **OK**（确定）后，您会看到一个 **Edit Local Printer Entry**（编辑本地打印机条目）对话框框（如图 19.7 所示）。如果您想为打印机命名，请在 **Names**（名称）字段中输入名称。如果您希望限制任何已排队打印机文件的大小（因为硬盘空间不足），请输入一个数字（例如 1024 表示 1 MB）。完成后，点击 **Select**（选择）按钮。

![](img/6bd28cbdb5cafd4e9d424d0c660b83ee_671_2.png)

![](img/6bd28cbdb5cafd4e9d424d0c660b83ee_671_3.png)

出现“配置过滤器”对话框框（如图 19.4 所示）。在选择完选项后，点击“确定”。您定义的打印机现在应该会出现在主 printtool 对话框中的打印机队列列表中。选择它，然后从“测试”菜单中选择 ASCII 或 PostScript 测试。

## 看不到列出的打印机？

如果在“配置过滤器”对话框中没有看到打印机的确切型号，别担心！很可能您的打印机与同一系列中的另一台打印机工作方式相似。除非您拥有一台需要专用驱动程序的特殊打印机，否则来自同一制造商的许多打印机过滤器条目都能正常工作。例如，HP 340 打印机用户可以使用 HP500 系列打印机的任意条目，Canon BJC 50 和 80 用户可以使用 Canon BJC 600 条目。

printtool 客户端（使用 Python 语言编写）首先定义您的打印机，然后将该定义插入 /etc/printcap 条目中，并附上 /var/spool/lpd 目录下使用 bash 编写的过滤脚本的指针。过滤器及相关脚本位于 /var/spool/lpd 下的一个目录（或打印机队列）中，具有您选择的名称或分配的默认名称。

## 自定义 RHS 打印机过滤器

主打印机过滤器集以及 printtool 数据库中打印机条目的定义位于 /usr/lib/rhs/rhs-printfilters 目录下。您可以通过编辑 printerdb 文件来更改所选打印机的选项。例如，如果您发现只想为 HP DeskJet 400 使用黑白打印，请以 root 身份使用您喜欢的文本编辑器打开 printerdb 文件。滚动浏览文件，直到找到 HP 400 条目，如下所示：

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

要为该系列打印机添加简单的黑白打印选项，请在 Resolution: 条目后添加 BitsPerPixel 条目：

BitsPerPixel: {1} {Normal B&W printing with black cartridge}

**注意**

您可以拆分打印机过滤器定义，为不同的打印机创建自定义条目，或者使用 StartEntry: 和 EndEntry 关键字之间的正确语法创建自己的打印机条目，这些关键字提供打印前选项以及由 Ghostscript 解释器对 PostScript 文档进行翻译。包含一个仅限单色的 DeskJet500 条目，但您可以重命名条目以更具体地描述打印机类型，并重命名安装在 LAN 上的打印机条目。尽管 printerdb 文件中有指针，但有关 Ghostscript 选项的详细信息可以在 /usr/share/doc/ghostscript-5.50 中的 devices.htm 文件中找到。

如您所见，printtool 可以添加、编辑或删除打印机。另一个不错的功能是能够给排队文件分配大小限制，如果您磁盘空间有限或不希望用户填满文件系统，这可能会很有帮助。如果您有一台打印机，需要更换打印墨盒才能打印黑白或彩色页面，您会发现 printtool 不可或缺。试一试吧！

虽然当前版本的 printtool，3.48，每次您进行更改时都会创建 /etc/printcap 数据库的备份，但当您删除打印机时，它不会删除相关的打印机队列或 spool 目录。

## Linux 打印命令

当然，您不必使用 printtool 命令来设置打印机。您可以直接编辑 /etc/printcap，但您应该知道自己在做什么，并理解 printcap 的格式。此文件是系统本地和网络打印机的 ASCII 数据库，详细描述了每台打印机的功能。有关完整详细信息，请参见 printcap 的 man 页面了解命令，以及 termcap 的 man 页面了解文件的布局。

