
Adabas-D 系统的文档位于 Adabas-D 根目录下的 doc 目录中（例如 `/opt/adabas-d/doc`）。

## LINCKS

LINCKS 是一个面向对象的数据库管理系统。如果您打算在网络环境中使用 LINCKS 并通过 RPC 调用共享数据，它是一个很好的系统。为了充分利用这个软件包，您需要具备一定的网络经验以及现有的网络基础设施。这个软件包并不适用于单节点系统，因为对于此类平台来说它过于复杂（overkill）。

> **注意**
> 您可以从 sunsite.unc.edu 的 `/pub/linux/apps/database/lincks` 目录中获取 LINCKS。

LINCKS 基于一种仅追加的面向对象结构。对象可以从其他对象派生。可以在对象之间建立链接以定义关系。您可以为对象定义视图。视图用于指定对象中的数据如何呈现给用户。同一个对象可以存在多个视图。视图可以被继承。

主要接口是 `xlincks` 程序。通过类似于 emacs 的命令，您可以交互式地浏览数据库。该界面类似于网页的超文本功能。您点击高亮的条目，程序就会引导您进入一个包含关于该主题更多信息的页面。

帮助有两种形式：上下文敏感帮助或可浏览的数据库。帮助文件触手可及——要访问帮助，只需按下帮助按钮即可。帮助文件的内容组织良好，是了解 LINCKS 的良好起点。手册的 PostScript 版本也可在 sunsite 归档中找到。

LINCKS 的分发软件包中包含几个程序。您可以使用 `droot` 命令创建新数据库。要修剪数据库中未被引用的对象，请使用 `cutoff` 命令。该应用程序的主要服务器是 `netserv` 程序，它为每个连接的客户端启动一个 `dbs` 进程。

## 其他数据库产品

当然，我们之前讨论过的 xBase 工具并不是 Linux 上唯一的数据库。市面上有许多非 dBASE 兼容的工具。我们可以快速概览一些其他用于 Linux 的数据库管理系统。其中大多数是免费的，可以在互联网上找到。

- mbase v5.0 是一个最初为 Amiga 编写并移植到其他平台的关系数据库系统。它使用类似 C 的语言格式进行数据库编程。使用 mbase 进行编译需要 ncursor 和 time。Makefile 中存在一些问题，可能需要您手动编辑。如果您真的想要低成本、类似 C 的 DBMS 访问，可以使用这个软件包。否则，请获取 FlagShip 或 dbMan，因为它们更稳定且更成熟。

- onyx 是一个基于类似 C 语言格式的数据库原型程序。执行 make config 命令会启动流程，并弹出一系列问题。回答这些问题将正确配置 Linux 上的数据库。

- DBF 是一个 xBase 操作软件包，是一组用于操作 dbf 文件实用程序的集合。其中一些实用程序，如 dbfadd，会在数据库中添加记录或信息层。dbflist 列出数据库中的记录；dbft 列出每个数据库及其项目的结构。

- typhoon 是另一个 RDBMS。这个 RDBMS 最显著的特点（取决于您的观点）是完全像 C。问题在于，该产品在被认为是一个可行的 RDBMS 之前仍需成熟。

## 总结

FlagShip 和 dbMan 是将现有的 dBASE 和 dBASE 兼容程序移植到 Linux 的优秀手段，在这些情况下，它们通常无需修改即可运行，并且在几乎所有情况下速度都更快。FlagShip 的一个 X 版本正在开发中，可在 FreeX86 或其他基于 Linux 的 X 版本下运行，预计 1997 年可用。不过目前，FlagShip 的演示版本允许 xBase 开发者继续在 Linux 下使用其数据库系统。带有 1500 页厚重文档的商业版价格为 199 美元，对于开发者来说物超所值。对于不需要 FlagShip 编译器功能和扩展功能的用户，dbMan 是一个合理的替代方案。

# StarOffice

作者：Tim Parker

## 本章内容

- 安装 StarOffice 1000
- 启动 StarOffice 1001
- 导入和导出文件 1005

![StarOffice 图像](img/e8e6b47ac20475e23d48b4c476f5d891_1036_0.png)

StarOffice 4.0 是一个基于 X 的 Linux 集成办公套件。该软件随某些版本的 Linux（如 Caldera OpenLinux）捆绑提供，也可以在某些 FTP 站点和 WWW 页面上找到。StarOffice 4.0（最新版本）包含三个办公工具：StarWriter 是文字处理程序，StarCalc 是电子表格工具，StarImpress 是演示图形软件包，还可以生成用于网页的 HTML 代码。

虽然 StarOffice 不等同于 Windows 上的 Microsoft Office 套件或 Windows 上的 Corel WordPerfect 套件，但您会对 StarOffice 的强大和实用感到惊讶。该软件包中包含的工具涵盖了日常工作中需要的大部分工具，配合一个数据库软件包（参见第 62 章了解数据库软件包），就构成了一个功能齐全的 Linux 办公平台。它也非常适合家庭使用。

StarOffice 不特定于任何特定的 Linux 版本。只要正在运行 X 服务器，它可以安装在当前可用的所有 Linux 版本上。

> **注意**
> StarOffice 4.0 可用于许多平台，包括 SCO UNIX。在该平台上，该软件包售价为 550 美元！Linux 用户通常可以从像 Caldera 这样的公司以捆绑形式或更低的价格获得 StarOffice。请访问 http://www.caldera.com 获取更多信息。

## 安装 StarOffice

StarOffice 通过脚本安装，而不是通过 Linux 包管理工具。要安装 StarOffice，您必须以 root 身份登录。StarOffice 是一个 X 应用程序，因此您应该启动 X 并打开一个 X 终端窗口来执行以下步骤。

要安装通常通过 CD-ROM 提供的 StarOffice，请将 CD 挂载到您通常使用的挂载点，例如：

```
mount /dev/cdrom /usr/cdrom
```

然后打开 CD-ROM 目录。那里将有几个文件目录，其中一个名为 *StarOffice4.0*。其他目录包含辅助文件以及许可信息。接下来，打开 *StarOffice4.0* 目录，然后打开 *bin* 子目录。要启动安装脚本，输入命令：

```
./setup
```

命令中的 `. /` 部分确保执行当前目录中的 setup 脚本，而不是路径中其他位置的脚本。命令启动后，您会看到一个如图 63.1 所示的窗口。在大多数情况下，选择标准安装例程是最好的选择，除非您不想安装 StarOffice 套件的某个或多个组件。此外，如果您的磁盘空间不足，您可能希望省略一些支持文件。

**图 63.1.** *StarOffice 安装脚本显示此选项列表。*

![图 63.1](img/e8e6b47ac20475e23d48b4c476f5d891_1038_0.png)

启动安装脚本后，StarOffice 会自动复制所有文件，仅显示完成百分比行。安装完成后，脚本退出。

## 启动 StarOffice

默认情况下，StarOffice 安装在目录 /root/Office40 中。如果您选择了手动安装例程，可以更改此路径，但它倾向于适用于大多数 Linux 版本。如果您希望从文件系统中的任何地方执行 StarOffice 套件，应该将此目录和 /root/Office40/bin 目录包含在您的路径中。

要启动 StarOffice，首先打开一个 X 终端窗口（如果尚未提供）。然后使用 cd 打开目录 /root/Office40/bin（如果您未将该目录包含在路径中）并输入命令：

```
soffice&
```

如果路径 /root/Office40/bin 不在您的路径中，并且当前目录 (.) 也不在路径中，您必须输入：

```
. /office &
```

*soffice* 命令后的 &amp; 符号用于强制将 StarOffice 放入后台，以便您可以继续使用发出此命令的 *X* 终端窗口。使用 *soffice* 是启动 StarOffice 最简单的方法，尽管如果您愿意，也可以单独启动各个应用程序。

## 注意

StarOffice 4.0 是现有最稳定的应用程序套件之一。在 Slackware Linux 平台上进行了超过一个月的高强度持续测试，StarOffice 从未崩溃过。很少有应用程序（甚至更少的操作系统）能提出这样的声明！

当启动 *StarOffice* 时，您会看到如图 63.2 所示的主 *StarOffice* 窗口。屏幕被分为左侧的文件浏览器和右侧的应用程序及帮助文件图标集。要查看在线帮助，请点击带有叠加在封面之上的问号图标之一。

![图 63.2](img/e8e6b47ac20475e23d48b4c476f5d891_1039_0.png)
