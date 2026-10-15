
如果你从软盘进行安装，还应该使用类似下面的命令将`Emacpea`软件包包拷贝到软盘上：

```
C copy m:/contrib/emacpea.tgz a:
```

对于实际安装，请按照以下步骤操作：使用拨号调制器连接运行`DOS`并配备语音输出的计算机（我将其称为“DOS 机器”）与你想要安装`Linux`的计算机（“Linux 机器”）。

启动`DOS`机器并启动你的终端仿真程序。将其设置为`9600`波特率、无校验、`8`位数据位、`1`位停止位。

在`Linux`机器上，插入“启动”磁盘并启动（开启电源、`cntl-alt-del`或按下重位键）。它应该读取磁盘大约五秒钟，发出哔声，然后停止显示以下文本：

> （注意：安装磁盘上的大段文本以前以 "- begin quote" 开头，以 "- end quote" 结尾。要跳转到引用的末尾，你可以搜索从第一列开始的两个连字符。我包装了部分内容以限制行长度）

```
+ -- begin quote

欢迎使用 Slackware96 Linux (3.1.0) 启动内核磁盘！

如果你有任何额外的参数要传递给内核，请在下方有效配置名称（ramdisk, mount, drive2）之后的提示符处输入。

这里是一些示例（可以在 BOOTING 文件中找到）：

ramdisk hd=cyl,hds,secs (其中 "cyl"、hds" 和 "secs" 是磁盘上的磁道数、扇数和磁头数。大多数机器不需要这个。）

在紧急情况下，你可以可以使用下面的命令启动系统：

mount root=/dev/hda1

在内存较低的机器上，你可以使用 `root=/dev/fdi` 或 `mount root=/dev/fd0` 在不使用 ramdisk 的情况下安装。详情请参见 `LOWMEM.TXT`。

如果你愿意从第二个软盘驱动器加载根/安装磁盘：drive2（甚至可以使用这个：ramdisk root=/dev/fdi）

先不要切换任何磁盘！此提示符用于输入额外参数。如果你不需要输入任何参数，按回车（ENTER）继续。

boot:

-- end quote
```

在这个这一点，我几乎总是能够按下回车键。

在你输入后，`Linux`机器应该再次读取软盘大约二十秒钟，然后引导内核。它打印的第一行是`"Loading..."`，这有点误导性。在这种情况下，`"ramdisk"`实际上是内核配置的名称。

内核中的每个设备驱动程序都会显示一两行。我正在使用的特定磁盘（`"bare.i"`启动磁盘）显示的内容超过了一个屏幕。可以通过`shift-page up`向上滚动文本。在我的机器上，启动信息如下：

```
-- begin ramdisk...
Uncompressing Linux....
Now booting the kernel
Console: colour VGA+ 80x25, 1 virtual console (max 63)
Calibrating loop.. ok - 35.94 BogoMIPS
Memory: 2302k/24768k available (688k kernel code, 384k reserved,
68k data)
Swansea University Computer Society NET3.035 for Linux 2.0
NET3: Unix domain objects 5.6.0 for NET3.035.
Swansea University Computer Society TCP/IP for NET3.034
IP Protocols: ICMP, UDP, TCP
VFS: Diskquotas version dquot 5.6.0 initialized
Checking 386/387 coupling... Ok, fpu exception using 16 error reporting.
Checking 'hlt' instruction... OK.
Linux version 2.0.0 (root@darkstar) (gcc version 2.7.2) #1 Mon Jun 10
21:11:56 CDT 1996
Serial driver 4.12 with no serial options enabled
tty00 at 0x3f8 (irq 4) is a 16550
PS/2 auxiliary device detected -- driver installed.
Ramdisk initialized : 16 ramdisks of 49152K size
hda: IBM-DBAO-2720, 689MB w/64K Cache, LBA, CHS=
hda: IBM-DBAO-2720, 689MB w/64K Cache, LBA, CHS=
hda: IBM-DBAO-2720, 689MB w/64K Cache, LBA, CHS=
```

注：提供的`OCR`文本包含大量的重叠/干扰噪声。我已根据提供的内容提供干净后的版本。

## 4. 阶段 3 终端到本地 Linux 系统

安装脚本会询问你是否要准备一张软盘。你应该这样做，因为这是启动`Linux`最稳妥的方法。你可能还想安装`ililo`（`"Linux loader"`的缩写）和/或`loadlin`（`"Load Linux"`的缩写）。安装脚本可以安装`ililo`。`Loadlin`是一个`DOS`程序，可以让你从它启动`Linux`。将它安装在在一个`DOS`分区上，并将一个压缩文件（通常命名为`image`）拷贝到该分区。在运行时，你可以使用类似`loadlin root=/dev/sda3 ro/`的命令启动`Linux`。（内核镜像位于同一目录中）。你可能会发现将内核子目录存储在与内核版本相同的目录下会更方便。

当`Slackware`设置完成主安装后，它会提示你通过按`ctl-alt`重启。在在此之前，你应该安装`emacspeak`。你可以在其他“贡献”软件中找到它。它位于`slackway/contrib`。假设你正直接从光驱安装`Linux`，设置程序会将光驱挂载到`/CDROM`目录下，你可以使用以下命令安装`emacspeak`：

```bash
# installpkg /CDROM/slackware/contrib/emacspeak.tgz
```

如果你安装的是软盘，请插入之前制作的软盘并输入：

```bash
# mount -tmsdos /dev/fd0 /floppy
# cp /floppy/emacspeak.tgz /tmp/emacspeak.tgz
# installpkg /tmp/emacspeak.tgz
```

你不应该直接从软盘上安装包，因为`DOS`文件系统不支持完整的文件名，所以`installpkg`程序会认为包名为`"emacspeak"`并以该名称存储其记录。

如果你有`DoubleTalk`或`LiteTalk`合成器，你还应该安装`emacspeak-dt`包。

使用新的启动软盘重启`Linux`，同时保持`DOS`机器的连接状态。你应该会在`DOS`机器上看到登录提示。庆祝吧！在让这个系统运行起来后，你需要学习`emacs`（第三种选择）和`Unix`系统管理。

## 4.2 学习 Unix 系统管理

大多数情况下，你会在需求产生时学习系统管理。首先是添加用户（你自己），然后是安装程序等等。唯一的例外是备份，你应该在需要备份之前学会它。

在需要学习的许多程序中，包含这些：

- `adduser`: 注册新用户，包括创建家目录和在`/etc/passwd`中添加条目。

- `tar`: 创建和解压`.tar`文件，这些是文件的集合（类似于`.zip`文件）。要列出存档的内容，使用`tar -tf foobar.tar`。要查看更详细的列表，使用`tar -tvf foobar.tar`。解压存档，使用`tar -xf foobar.tar`。

- `chmod`: 修改文件或目录的权限。

- `chown`: 修改文件或目录的所有者。

- `find`: 递归搜索目录。例如，命令`find -name '*alpha*' -print`意味着在当前目录(`.`)中搜索文件名包含字符串`"alpha"`(`-name '*alpha*'`)的文件，并打印其路径和名称(`-print`)。（使用`GNU find`，`-print`是可选的。）

- `du`: 显示文件或子目录占据的空间。对于带有“空洞”的文件，此值可能小于文件长度。

- `df`: 显示文件系统的容量、可用空间以及挂载点。

- `mount`: 显示文件系统、挂载位置以及挂载标志。

- `ifconfig`: 配置和检查互联网协议(`IP`)网络接口，包括以太网卡、`SLIP`链接和`PLIP`链接。

- `route`: 在接口配置后配置和检查`IP`网络路由。

- `ping`: 在接口和路由配置后检查`IP`网络连通性。

- `ftp`: 跨互联网传输文件。

这里是你可能想要安装的程序：

- `agrep`: 用于近似而非精确字符串匹配的近似`grep`搜索（也称为“模糊字符串搜索”）。
