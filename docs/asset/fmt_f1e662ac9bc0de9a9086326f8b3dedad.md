
# 第 12 章 打印服务

## 配置和管理打印服务

在本例中，`mf_wrapper` 实用程序被用作打印过滤器，当 `mf_wrapper` 调用相关实用程序（`magicfilter`）时，根据初始字节头或 `/usr/share/printconf/mf.magic` 中列出的魔数将文件流识别为文本文件、文档或图像。

> 注意
> 这些魔数包含许多文档的起始字节。它们被 `file` 命令使用，即使文件名有扩展名也可以显示文件的类型。例如，PostScript 文档通常具有 `.ps` 扩展名。然而，如果缺少扩展名，文档格式可能并不显而易见。可以使用 `file` 命令确定一个或多个文件类型，如下：

```
# 配置和管理打印服务

$ file tiger art_collection
tiger: PostScript document text conforming to level 2.0 - type EPS
art_collection: Zip archive data, least v2.0 to extract
```

在本例中，名为 `tiger` 的文件是 PostScript 文档，而名为 `art-collection` 的文件是压缩归。

`magicfilter` 实用程序随后管理流到 PostScript，使用位于 `/usr/share/printconf/mf_rules` 目录的规则。这些规则返回的值根据目标打印机的类型为 Ghostscript PostScript 解释器 `gs` 分配适当的参数。解释器读取输入文件作为 PostScript，然后将流转换为目标打印机理解的格式或语言。使用 PCL 或 PostScript（如果打印到目标打印机）。

Red Hat 的打印系统可以用于打印到本地（连接）或远程（网络）打印机。如果你使用本地打印机，它由打印设备表示，例如 `/dev/lpd0` 或 `/dev/usb/lpd0`（如果你有 USB 打印机）。本地和远程打印机定义（称为打印队列）包含在系统的打印机能力数据库 `/etc/printcap` 中。此数据库中列出的每个打印机都将在 `/var/spool/lpd` 下有一个对应的打印队列缓存区，其名称为打印机名称。正在打印的文档被称为打印作业，你可以在缓存区目录中查看队列列表或当前打印作业的列表。

要向你的 Red Hat Linux 系统添加打印机，请使用 `redhat-config-printer` 客户端来创建、配置和定义打印机。该客户端将定义保存为系统打印机能力数据库 `/etc/printcap` 中的一个条目。每个定义包含一个指向 `/var/spool/lpd` 下相应命名缓存区的文本字段。此缓存区将保存等待打印的打印文档副本。

与缓存区一起，打印机的 `printcap` 列表包含一个指向 `/usr/share/printconf/util/mf/wrapper` 的条目。该文件是一个调用 `/usr/bin/magicfilter` 实用程序的脚本。

带有 `if:` 条目的示例打印机描述（调用实用程序的 shell 脚本指针）如下：

```
lpd:

:ml0:

:mx#:

:sd=/var/spool/lpd/lp:

:af=/var/spool/lpd/lp/lpd.acct:

:sh:

:lp=/dev/lpd0:

:lpd_bounce=true:

:if=/usr/share/printconf/util/mf/wrapper:
```

### 管理打印服务

打印服务和打印作业由 `lpd` 守护进程处理，它由 `/etc/rc.d/init.d/lpd` 启动脚本启动，其内容如下（部分）：

```
start () {

  echo -n $'Starting $prog: ""

  # Is this a printconf system?

  if [[ -x /usr/sbin/printconf-backend ]]; then

    run printconf-backend to rebuild printcap and spools

    if ! /usr/sbin/printconf-backend; then

      # If the backend fails, we dont start no printers defined

      echo -n "No Printers Defined"

      echo_success

    fi

    return 0

  fi

}
```

请注意这里显示了整个脚本。然而，如你所见，脚本首先报告服务正在启动。接下来，使用与 Red Hat `printconf` 实用相关的命令来检查你系统的 `/etc/printcap` 数据库是否存在。脚本启动 `lpd` 守护进程，该进程作为进程在后台运行，等待 `/var/pool/lpd` 目录下定义的打印机目录出现任何文件。

在定义打印机后，你可以使用一个或多个传统的行打印机池实用程序来控制打印服务、管理打印（或打印作业），并启用、禁用或授权远程打印服务（参见本章后文“打印工具”部分）。

### 表 12.1 打印相关的命令和驱动程序

| 名称 | 描述 |
| --- | --- |
| a2ps | 为 PostScript 打印格式化文本文件 |
| dvi[lj,l4,l2p,l4] | 将 TeX D 文件转换为特定的 PCL 格式 |
| encscript | 将文本文件转换为 PostScript |
| escputil | Epson Stylus 喷墨打印机工具 |
| grolbp | 用于 Canon LBP-4 和 LBP-8 激光打印机的 groff 驱动 |
| gs | Ghostscript 解释器 |
| gsbj[dj500, lp] | Ghostscript 喷墨打印机驱动程序 |
| gsdj[dj500,lj,lp] | Ghostscript 喷喷打印机驱动程序 |
| lpc | 打印机控制工具 |
| lpd | 打印池守护进程 |
| lpf | 通用打印机过滤器 |
| lpm | 打印队列管理工具 |
| mpage | PostScript 文本格式化工具 |
| pap | 基于 Appletalk 的打印机客户端 |
| pbm[2ppa,page,to10x,toepson, tappa,toptx] | 便携式位图转换工具 |
| pr | 文本格式化命令 |
| psmandup | 非双面打印机的双面打印工具 |
| setup | 启动打印机配置工具 |
| smbclient | $MB 打印池 |
| smprint | $MB 打印 shell 脚本 |
| smbspool | $MB 打印池 |
| thinkjetopbm | 便携式位图到 Thinkjet 打印机的转换工具 |

你可以通过使用 `gs` 解释器配合 `--help` 命令行选项来显示其内置的打印机设备，如下：

```
# gs --help
```

> 注意
> Red Hat 提供了你可以查看许多不同类型文档的图形客户端。例如，要显示 PostScript 文档（包括压缩的 PostScript 文档）或 PostScript 图像，请使用 g 客户端。要显示 PDF（便携文档格式），你可以使用 ev 或 xpdf 查看器。

`gs` 命令从命令行输出许多行文本，并列出内置的打印机和设备。获取此信息的另一种方法是启动 `gs` 并如下所示使用 `denicenames ==` 命令：

```
# gs

GNU Ghostscript 7.05 (2002-04)

Copyright (C) 2002 artofcode LLC, Benicia,.. rights...此此提供任何保证：详情请见 PUBLIC。

Loading NimbusRom9-Regu font from /user/share/fonts/default/Type1/

~n210031.pfb...

241068 103596 164250 347466 0 done.

Loading NimbusSans-Regu font from /user/share/fonts/default/Type1/n0190031.pfb...

278562 137984 166216 35865 0 done.

Using NimbusSans-Regu font for NimbusSans-Regu.

[/miff24/psmono/alc8500/lp2563/pmkraw /stp/iwlq /pbm/md1x
```

Red Hat 提供了你可以查看许多不同类型文档的图形客户端。例如，要显示 PostScript 文档（包括压缩的 PostScript 文档）或 PostScript 图像，请使用 g 客户端。要显示 PDF（便携文档格式），你可以使用 ev 或 xpdf 查看器。
