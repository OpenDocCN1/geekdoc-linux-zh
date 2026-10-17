
尽管如此，要解决持续存在的字体不匹配问题，唯一的方法是获得正确的字体。这意味着你要么必须购买它们，要么希望你拥有某个包含它们的软件以及使用许可。Adobe 的 Type Basics 将你带到 Level 2，并包含一个光栅化器的许可。盗版字体是卑鄙恶劣的，更不用说违法了，所以不要这样做。

## Ghostscript 选项

以下是 Ghostscript 一些更有用的选项。`gs -h` 也会快速提醒你这些选项。

### `-sDEVICE=devname`

使用输出设备驱动程序 `devname`；例如，`-sDEVICE=epson` 选择与 Epson 兼容的打印机。

### `-sPAPERSIZE=papersize`

选择纸张大小（`papersize` 可以是 `letter`、`legal`、`a4` 等）。

### `-r nxm` 或 `-rn`

指定分辨率，分别为水平 `n` dpi 和垂直 `m` dpi，或者仅用 `n` 表示两者。选择打印机不支持的分辨率可能会导致不可预测的结果。

### `-dQUIET` 和 `-q`

Ghostscript 在解析文件时会输出一些诊断信息。`-dQUIET` 会去掉中间消息，`-q` 会去掉启动消息。在过滤器中，你需要 `-q`，以及 `-dSAFER`、`-dNOPAUSE` 和 `-dBATCH`（见下文）。

### `-dSAFER`

移除文件写入功能。这对过滤器至关重要；你不希望人们仅仅通过打印恶意文件就删除或修改系统文件！

### `-dBATCH`

处理完最后一个文件后退出。

### `-dNOPAUSE`

每页结束后不暂停。

### `-sOutputFile=filename`

将输出写入 `filename`。你可以在此处使用一些特殊选项，例如 `%pipe%cmd`，它将输出发送到 `cmd` 程序，以及 `%stdout`，它发送到标准输出。此外，`filename` 可以包含 `%d`，这意味着每页会输出到单独的文件，并用页码替换 `%d`。

## SMB 版本

如果你必须将输出发送到连接到 Windows 的打印机，你需要在过滤器中添加一条 Ghostscript 命令，将过滤器设置为像 PostScript 打印机一样工作（参见前面关于 Ghostscript 的部分）。

例如，假设你使用了 SAMBA 附带的 `smbprint` 过滤器示例：

```
) | /usr/local/samba/bin/smbclient "\\\\$server\\$service" "$password" -U $server -N -P >> $logfile
```

将其改为两行：

```
) | ghostscript_command | \
/usr/local/samba/bin/smbclient "\\\\$server\\$service" "$password" -U $server -N -P >> $logfile
```

在这里，`ghostscript_command` 调用 Ghostscript——例如：

```
) | /usr/bin/gs -q -dBATCH -dNOPAUSE -r600x300 -sOutputFile=- -sDEVICE=deskjet - | \
/usr/local/samba/bin/smbclient "\\\\$server\\$service" "$password" -U $server -N -P >> $logfile
```

效果是，Ghostscript 对 `lpd` 馈送到打印过滤器的输入运行，然后 Ghostscript 将位图发送给 `smbclient`。

## 5.5 `printcap` 生成与分发

对于拥有许多打印机的大型网络，将正确的 `/etc/printcap` 分发给正确的机器可能需要大量时间。你应该使用打印机主列表来自动完成此任务——你可以根据主机名从该列表生成文件。传统的 Unix 工具是名为 `m4` 的宏处理语言。实际上每个人都有自己的一套系统，所以我们不妨描述一下我们自己的。

在随附 CD-ROM 的 `support/printing/printcap` 目录中，你会找到一组 `m4` 文件和一个 `Makefile`。

如果你运行 `m4 generic-lprng.m4`，输出将是一个通用的 LPRng 客户端 `printcap`，其中包含许多打印机。`printer-list.m4` 定义这些打印机，但在你检查该文件之前，让我们先看看 `generic-lprng.m4` 文件：

```
define(this_host,generic-host)dnl
```

此行定义获取 `printcap` 的主机。这个特定定义可以被许多主机使用，这些主机都没有连接本地打印机。我们使用名称 `generic-host`，它与网络上的任何主机名都不匹配（稍后将详细介绍主机名匹配）。

```
include(common.m4)dnl
include(lprng-printcap.m4)dnl
```

这些行从其他文件引入 `m4` 源代码。第一个 `common.m4` 定义了一些对所有输出通用的宏，例如假脱机目录前缀。第二个 `lprng-printcap.m4` 为 LPRng 创建自定义输出。

```
include(printer-list.m4)dnl
```

最后，`m4` 读取打印机列表并创建输出。

### `printer-list.m4` 文件

文件 `printer-list.m4` 是一个打印机和描述的列表，条目如下：

```
HP4SI(hp160b,HP LaserJet 5Si,hp160b|160b,room 160b Ryerson,
    printerserv.cs.uchicago.edu,
    HP_LaserJet_4Si_300_dpi,hp160b.cs.uchicago.edu)dnl
```

第一个参数是打印机的主名称，第二个是描述，第三个是别名列表，第四个是其物理位置。这些信息构成了 `printcap` 条目的第一个字段。

由于你可以将打印机本地连接到不同的机器，`printcaps` 在网络中各不相同。例如，如果主机 `mikado` 将喷墨打印机连接到其并行端口，其 `/etc/printcap` 将包含发送文件到该打印机所需的 spool 目录和过滤器信息。网络上除 `mikado` 之外的任何机器都需要一个 `printcap`，其中包含一条说明该打印机位于 `mikado` 上的条目。这就是 `printer-list.m4` 文件中第四个参数的作用——它是该打印机所连接的机器。如果第四个参数与 `this_host` 的定义匹配，你会得到针对本地打印机的输出；否则它就是远程打印机条目。

要添加一个新的 `printcap` 变体，如上面在主机 `mikado` 上的本地打印机那样，你需要创建一个名为 `mikado.m4` 的新文件：

```
define(this_host,mikado)dnl
include(common.m4)dnl
include(lprng-printcap.m4)dnl
include(printer-list.m4)dnl
```

之后，命令

```
$ m4 mikado.m4 > mikado
```

将为 `mikado` 创建一个新的 `printcap`。然而，`Makefile` 提供了一种一次性生成所有内容的方法；请查看下面的说明。

### Macro Definitions

打印机列表是一组宏调用。对于 LPRng `printcap`，宏定义在 `lprng-printcap.m4` 中，它们看起来像广义的 `printcap` 定义。每种打印机（或打印机配置）都有不同的宏定义，而且大多数非常相似（比较 `HPPSD` 与 `HP4SI`）。添加一种新类型的打印机通常只需要复制一个类似的定义，然后根据需要进行修改即可。

请注意，当你添加新的打印机类型时，你可能还需要在其他文件中做一些工作。该 `printcap` 生成系统足够灵活，可以容纳需要有关打印机信息的其他类型文件。这些包括原始 `lpd`（非 LPRng）的 `printcaps`（在此处在 `lpd-printcap.m4` 中完成）、Netatalk（`netatalk-source.m4`）和 SAMBA（`samba-source.m4`）配置文件，用于允许 AppleTalk 和 SMB 访问、创建适当 spool 目录的脚本（`mkdirs.m4`），以及你能为其编写宏列表的任何其他内容。

如果你添加了一种新的打印机类型并使用这些额外文件（例如 `samba-source.m4`）来生成其他文件，你需要将该类型的打印机添加到它们中。幸运的是，你可能已经完成了艰难的工作，因为其中一些文件非常简单（请查看 `netatalk-source.m4` 作为示例）。

最后，`Makefile` 将其收尾。在 `printcap` 目录中执行 `make` 将生成所有文件。

#### Example: Generating a New `printcap` for `mikado`

假设我们要为前面提到的机器 `mikado` 添加新的 `printcap`。`Makefile` 中的一个定义如下：
