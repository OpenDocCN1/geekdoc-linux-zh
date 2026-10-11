
然后是文件，即 `/etc/printers.conf` 文件；最后是 nis，在 `printers.conf.byname` 表中。

- 对于 nis+ 名称服务，“printers; user nisplus files xfn”。打印客户端按以下顺序查找信息：首先是 user，在 \$home/.printers 文件中；然后是 nisplus，在 printers.org_dir 表中；接着是 files，在 /etc/printers.conf 文件中；最后是 xfn，在 FNS 打印机上下文中。

你可以使用 Solaris 打印管理器的“查找”命令（而不是本地打印管理器）来定位网络上的打印机。在查找对话框中输入打印机名称，该工具将在上述列表中搜索资源以定位打印机。

SunSoft 打印客户端命令用于在网络上查找打印机。打印命令将定位打印机并确定打印机的配置，如下所示：

1.  确定打印机名称或打印机类是否有效。
2.  如果打印机名称不是有效的名称或类格式，则 print 命令将检查用户的 <PRINTER> 或 <LPDEST> 环境变量以查找默认打印机名称。
3.  如果未作为环境变量找到打印机名称，则 print 命令将检查用户主目录中的 .printers 文件以确定 _默认打印机别名。
4.  如果无法使用上述三种方法中的任何一种确定匹配项，SunSoft 打印客户端将检查 /etc/printers.conf 文件以查找打印机配置。
5.  最后，打印机将访问诸如 NIS+ 等名称服务，以检查打印机是否存在。

在名称服务中发布打印机的优势在于，任何 SunSoft 打印客户端都可以通过名称访问该打印机并获取其配置信息。在 Solaris 8 中，支持 NIS、NIS+ 以及带 FNS 的 NIS+ 名称服务。在检查名称服务时，SunSoft 系统会根据名称或类检查原子、POSIX 或上下文打印机。

## 添加打印机

当你在本地或网络上添加打印机时，你需要通过执行以下操作提供一些信息：

- 定义打印机名称、打印机描述和打印机端口。
- 选择打印机类型及其可接受的文件内容类型。
- 定义故障通知行为和默认打印机。
- 设置用户对打印机的访问权限。
- 设置打印机类。
- 指定是否打印横幅页。
- 确定故障恢复行为。

如上所述，其中许多任务可以在网络打印机的 Solaris 打印管理器或本地打印机的 AdminTool 中完成。目前，打印管理器不支持打印机类或故障恢复；你需要使用 `lpadmin` 命令来设置这些选项。你还会发现，虽然你可以使用打印管理器来指定文件内容、故障通知、横幅页以及对打印机的访问权限，但 `lpadmin` 命令在这些方面的功能更强大。

打印机名称必须在你域中是唯一的，并且可以包含多达 14 个字母数字字符。描述是一个注释字段，有助于人们定位打印机或理解打印机类型。

将打印机添加到计算机时，你需要指定打印机连接的设备或打印机端口。你可以在打印管理器中或通过 `lpadmin` 命令设置打印机端口。通常，系统配有三个端口（`/dev/term/a` 和 `/dev/term/b` 两个串行端口以及一个并行端口）。你可以使用任何识别的端口名称。在 IA 系统上，只有第一个端口被启用。其他端口默认禁用。要在 IA x86 系统上使用其他端口，必须编辑 `/platform/i86pc/kernel/drv/any_conf` 和 `/platform/i86pc/kernel/1p_conf` 下的两个端口配置文件。

`lpadmin -T` 命令最适合用于建立打印机类型。打印机类型是打印机类型的通用名称，通常与制造该打印机的制造商相关联。DECWriter 打印机指定为 `decwriter`。PostScript 打印机包括各种类型的 Apple LaserWriter 打印机。有关打印机类型的信息可在 `terminfo` 数据库（`/usr/share/lib/terminfo`，如图 10.4 所示）中找到。如果使用 `ls` 命令查看该数据库的目录，你将看到许多单数字和字母组合的条目。每个单字母条目是一个子目录，包含与特定制造商文件相关的多个文件。例如，`e` 子目录包含 Epson 打印机文件，而 `n` 目录包含 NEC 打印机文件。只要可能，如果你的打印机支持 PostScript 打印机类型，即使你找到了系统文件类型，也尝试使用 PostScript 打印机类型。你可以使用 `lpadmin -t` 选项将多个打印机类型分配给一个打印机。

你应该使用的第二个有用的分配是使用 `lpadmin` 命令来指定文件内容类型。打印过滤器将文件的内容类型转换为打印机可接受的内容类型。文件内容类型由 LP 打印服务用于确定打印机可以在不经过过滤的情况下直接打印的文件类型。所需的字体需要驻留在打印机中，或在处理未过滤的文件之前提供给打印机。无法直接处理的其他文件类型首先通过打印过滤器，然后由打印机处理。

### 图 10.4
*打印机类型的 terminfo 数据库*

![](img/256e02a6afce528d264a8d911fa0ff20_429_0.png)

大多数打印机可以打印与打印机类型相同的类型（PostScript 打印机为 PS）或用于 ASCII 文本文件的 *simple* 类型。将文件发送到打印机时，你可以使用 `lp -T <content_type>` 命令指示内容类型。如果不指定内容类型，LP 打印服务将检查打印请求中的第一行以确定文件类型。如果 `^D`! 或 `!` 符号是第一个符号，则该文件被视为 PostScript 文件（这些是 PostScript 控制代码），否则，文件类型被视为 ASCII 文本文件。PostScript (postscript)、ASCII (*simple*) 或 PostScript 和 ASCII 组合 (*simple,postscript*) 不需要过滤。当选择 None (`*`) 作为文件内容类型时，任何与打印机类型不匹配的文件必须经过过滤，当选择 Any (any) 时，不需要过滤。如果文件内容类型 Any 无法直接处理，则不会打印。

Solaris 不像 Windows 那样内置广泛的打印机支持，但有很多受支持的打印机，你可以从几家公司为更多打印机购买第三方支持。Sun 不提供过滤器的非 PostScript 打印机包括 Daisy (*daisy*)、Datagraphix (*datagraphix*)、DEC LA100 (la100)、DEC LN03 (ln03)、DECwriter (*decwriter*)、Diablo (*diablo* 和 *diablo*-m8)、Epson 2500 (*epson2500*)、DEC*emx (-80)、*epson*-2500-hi 和 *epson2500*-hi80)、Hewlett-Packard HPCL 打印机 (*hplaser*) 以及 IBM Proprinter (*ibmproprinter*)。

从 Solaris 2.6 开始，Sun 在打印服务器上为客户端和服务器安装所有打印包。打印客户端可能仅安装其自身的包。对于 PostScript 打印，过滤软件作为其自身的打印包安装。表 10.4 列出了当前的打印包集合。在处理网络打印机之前，你需要安装 Solaris 打印管理器包。通过在命令行中输入以下命令来检查是否安装了打印管理器：`pkginfo | grep SUNwppm`。

| **软件包** | **描述** |
|---|---|
| **SUNwpcr** | SunSoft 打印客户端 |
| **SUNwpcu** | SunSoft 打印客户端 |
| **SUNwpsr** | SunSoft 打印 LP 服务器 |
| **SUNwpsu** | SunSoft 打印 LP 服务器 |
| **SUNWPSF** | PostScript 过滤器 |
| **SUNsclp** | SunSoft 打印源代码兼容性 |
| **SUNwppm** | Solaris 打印管理器 |

## 打印机状态

`lpstat` 命令用于确定由 LP 打印服务管理的打印机的状态。该命令提供关于打印队列中的打印作业、打印机可用性以及特定打印请求 ID 的信息。当 `lpstat` 不带任何额外选项使用时，该命令返回你提交的打印队列中文件的列表，每个打印作业一行，如下所示：

```
$ `lpstat`
$ flash-3 barries 1382 Dec 15 23:45 on sunrise
$
```

显示内容告知你 flash 作业队列中的作业编号（3）、指定打印作业的用户、打印 ID、作业提交的日期和时间，以及充当打印服务器或本地连接的系统。

`lpstat` 接受以下选项：

- `-a option`：`-a` (accept) 选项指定打印机目的地是否接受请求。
- `-c option`：`-c` (class) 选项显示打印类及其成员。
- `-d option`：`-d` (destination) 选项显示默认目的地。
- `-f option`：`-f` (form) 选项显示正在使用的表单。
- `-o option`：`-o` (output) 选项显示你的输出的状态。

