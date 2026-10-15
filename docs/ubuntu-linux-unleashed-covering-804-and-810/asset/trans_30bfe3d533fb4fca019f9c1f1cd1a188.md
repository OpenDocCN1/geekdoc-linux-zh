

资源需求可以通过其他设置进行定制，例如 MaxCopies 用于设置用户打印作业的最大副本数，MaxJobs 用于设置活动打印作业数量的限制，以及 MaxJobsPerUser 用于设置每个用户活动作业数量的限制。RIPCache 设置（默认 8MB）控制打印过程中用于图形缓存的内存量。

例如，如果你想将打印限制为每次最多 20 份文档或页面，并且每个用户同时最多 10 个打印作业，请使用如下设置

```
MaxCopies 20
MaxJobsPerUser 10
```

### TIP

> 不要忘记在对 CUPS 配置文件进行任何更改后重新启动 CUPS 服务器。更改只有在服务重新启动时（守护进程重新读取其配置文件时）才会激活。参见本章后面的“GUI-Based Printer Configuration Quickstart”部分。

## Configuring and Managing Print Services

作为系统管理员（或工作站的 root 操作员），你的任务是正确定义本地或远程打印机，并确保打印服务已启用并正常运行。幸运的是，Ubuntu 包含一个图形打印服务配置工具，使这项工作变得简单。你应该使用这些工具来配置打印，正如本章这一部分所介绍的那样。但首先，花点时间阅读一下配置过程的快速概述。

你可以使用 system-config-printer 图形界面来配置打印服务。本章的大部分详细内容都涉及 GUI 的使用。然而，以下概述部分为你提供了两种配置方法的坚实基础。你将在本章后面的部分学习这些过程的细节。

## GUI-Based Printer Configuration Quickstart

使用 system-config-printer 工具为 Ubuntu 配置打印机非常简单，该工具位于 System, Administration, Printing 下。如果你不确定 cupsd 是否正在运行，你可以快速切换到终端并使用 /etc/init.d/cupsys 命令配合 status 关键字，如下所示：

```
$ sudo /etc/init.d/cupsys status
```

你将看到以下内容之一

Status of Common Unix Printing System: cupsd is not running.

或，如果 cupsd 正在运行，则会看到类似以下的确认信息

```
Status of Common Unix Printing System: cupsd is running.
```

如果 cupsd 已安装但未运行，请按如下方式启动守护进程：

```
$ sudo /etc/init.d/cups start
```

要访问 GUI，请选择 System, Administration, Printing。

然后你只需按照提示定义打印机并添加本地或远程打印服务。在保存更改之前，你应该打印测试页。可使用打印机配置客户端或从 GNOME 或 KDE 客户端的 File 菜单的 Print 菜单项。

### NOTE

system-config-printer 实用程序是 gnome-cups-manager 的替代品，后者曾是 Ubuntu 的默认打印机配置工具。这个新实用程序实际上最初是为 Fedora 开发的，后来被 Ubuntu 采用。

## Managing Printing Services

定义打印机后，你可以使用命令行查看和控制你的打印作业，或者如果为 root，则可以查看和控制系统上的所有打印作业和打印机。表 8.1 包含 Ubuntu 中包含的部分 CUPS 及相关打印命令和驱动程序列表。

## TABLE 8.1 Print-Related Commands and Drivers

| Name | Description |
|------|-------------|
| a2ps | Formats text files for PostScript printing |
| accept | Controls CUPS print job destinations |
| cancel | Cancels a CUPS print job |
| disable | Controls CUPS printers |
| dvi[l1], l[4], l[2p], l[4] | Converts TeX DVI files to specific PCL format |
| enable | Controls CUPS printers |
| enscript | Converts text files to PostScript |
| escputil | Epson Stylus inkjet printer utility |

大多数 Linux 系统使用 PostScript 作为打印的默认文档格式。Ubuntu 使用 gs 命令与 CUPS 结合来管理本地和远程打印作业以及打印作业期间传输的数据类型。gs 命令用于将文档流翻译成目标打印机接受的格式（该打印机很可能使用 PCL）。

你可以使用 Ghostscript 解释器 gs 通过使用其 --help 命令行选项来显示其内置打印机设备，如下所示：

```
# gs --help
```
