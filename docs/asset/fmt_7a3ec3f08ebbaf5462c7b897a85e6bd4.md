
在 Linux 中，几乎每个命令、程序和工具都有一个特定的帮助文件，描述如何使用它。例如，如果我需要关于最佳无线破解程序 `aircrack-ng` 的帮助，我可以输入 `kali >aircrack-ng --help`。注意这里的双横杠。在 Linux 中，习惯上在使用仅带单个字母的单词-横杠选项（如“h”）之前使用双横杠（`--`）。当你输入此命令时，你应该收到使用该工具的说明以及对它的简要描述。你可能可以使用 `-h` 或 `?` 来访问帮助文档。例如，如果我需要使用 Nmap（黑客最好的端口扫描工具）的帮助，将输入 `kali >nmap -h`。遗憾的是，尽管许多应用程序接受这三个选项，但不能保证你正在使用的那个一定有效。所以，如果第一个不起作用，请尝试另一个选项。

## 查找文件

在 Linux 中导航在习惯之前可能很乏味，学习一些命令和技巧会让命令行更加用户友好。你可以在终端使用以下命令来查找内容。

`locate` 可能是最用户友好的搜索命令。当此命令与指定要查找内容的关键词一起使用时，它将在整个文件系统中搜索该术语出现的地方。例如，输入以下内容来搜索 `aircrack-ng`：

```
kali >locate aircrack-ng
/usr/bin/aircrack-ng
/usr/share/applications/kali-aircrack-ng.desktop
/usr/share/directories--
/var/lib/dpkg/info/aircrack-ng.gz
```

然而，`locate` 命令并不是完美的。你从 `locate` 结果获得的信息可能太多而无法处理。`locate` 使用通常每天更新一次的数据库，所以如果你最近生成了文件，在第二天之前可能出现在此列表中。了解这些基础命令的缺点可以帮助你决定何时使用每种。

## 使用 where 命令查找二进制文件

如果你正在寻找一个二进制文件，可以使用此命令来找到它。如果可用，你可以使用此命令找到它。例如：

```
kali >which aircrack-ng
/usr/bin/aircrack-ng
/usr/share/applications/kali-aircrack-ng.desktop
```

## 使用 which 命令在根目录下查找二进制文件

使用 `touch` `Touch` 是创建文件的第二种方法。最初，此命令的目的是允许用户编辑文件的元数据，例如创建或修改日期。但默认情况下，如果文件不存在，此操作会创建文件。

让我们使用 `touch` 命令创建 `newfile`：

```
kali >touch newfile
```

之后，我运行 `ls -l` 查看目录的详细列表，可以看到 `newfile` 已作为一个新文件创建。由于 `newfile` 是空的，请注意它的大小为 0。

创建目录的命令是 `mkdir`，它是 "make directory" 的缩写。输入以下命令创建一个名为 `newdirectory` 的目录：

```
kali >mkdir newdirectory
```

输入以下内容进入此最近创建的目录：

```
kali >cd newdirectory
```

## 复制文件

`cp` 命令用于复制文件。通过这种方式，旧文件将保留在原处，并在新位置创建一个它的副本。在这里，我们将使用 `touch` 在根目录下创建一个名为 `oldfile` 文件，并将其复制到 `/root/newdirectory`，同时重命名原始的 `oldfile` 以保留在原处：

```
kali >touch oldfile
kali >cp oldfile /root/newdirectory/newfile
```

你可以简单地在目录路径末尾添加你想要的名称来选择重命名文件。如果你在复制时没有重命名它，系统默认将保留文件的原始名称。当我们下次导航到 `newdirectory` 时，我们可以发现 `newfile` 是 `oldfile` 的完全副本：

```
kali >cd newdirectory
kali >ls
newfile oldfile
```

## 重命名文件

遗憾的是，与 Windows 等其他操作系统不同，Linux 缺少专门用于重命名文件的命令。然而，它有一个 `mv` (move) 命令。`mv` 命令可用于重命名现有文件或目录或将其移动到不同的位置。你可以输入以下内容将 `newfile` 重命名为 `newfile2`：

```
kali >mv newfile newfile2
kali >ls
oldfile newfile2
```

现在 `newfile2` 已经重命名，当你列出 (`ls`) 该目录时，可能会看到它，但看不到 `newfile`。目录也可以进行同样的操作。

## 删除文件

要删除文件，请如下所示使用 `rm` 命令：

```
kali >rm newfile2
```

你可以通过对目录执行详细列出来验证文件是否已删除。

## 目录

用于删除文件的 `rm` 命令带有一个 `dir`（directory 的缩写）参数，如下：

```
kali >rmdir newdirectory
rmdir:failed to remove 'newdirectory': Directory not empty
```

至关重要的是，`rmdir` 不会删除非空目录，正如示例所示，它会通知你目录非空。在删除目录之前，你必须先删除它的所有内容。这将防止你无意中删除不需要删除的项目。如果你想一次性删除目录及其内容，可以在 `rm` 之后使用 `-r` 选项，如下所示：

```
kali >rm -r newdirectory
```

不过提醒一下：在使用 `rm` 时要务必小心 `-r` 选项，因为很容易误删珍贵的文件和目录。例如，在主目录下使用 `rm -r` 将删除那里的每一个文件和目录；这无疑不是你的本意。

## 查找工具和包

在下载软件包之前，你可以检查它是否已经存在操作系统的仓库（数据存储所在）。`apt` 工具的搜索功能允许你查看该包是否已安装。这里使用了简单的语法：

```
apt-cache search keyword
```

记住，要搜索 `apt-cache`——即存储包名称的位置——我们使用 `apt-cache` 命令。例如，你可以执行下面所示的命令来查找入侵检测系统 Snort。

```
kali>apt-cache search snort
fsnort - Snort-to-iptables rule translator
ipple - IP protocols logger
--snip--
snort - flexible Network Intrusion Detection System
sn-common - flexible Network Intrusion Detection System - common files
--snip--
```

如你所示，“snort”一词出现在许多文件中，但在输出的中心，我们发现了短语“snort - flexible Network Intrusion Detection System”。这正是我们要找的内容。

## 安装软件

既然你已经知道 `snort` 包在仓库中可用，现在可以使用 `apt-get` 获取该程序。在终端中使用 `apt-get` 命令、关键字 `install`，后跟你想要安装的包名，即可从你操作系统的默认仓库安装软件。格式如下：`apt-get install package name`。让我们测试一下。格式如下：：

```
apt-get install snort
Reading package lists... Done
Building tree
Reading state information... Done
The following NEW packages will be installed:
snort
--snip--
Do you want to continue?
```

## 卸载软件

要卸载软件，请使用带有 `remove` 选项的 `apt-get`。可能会看到如下所示的输出。

```
apt-get remove snort
Reading package lists... Done
Building tree
Reading state information... Done
The following packages will be removed:
snort
--snip--
Do you want to continue?
```

要删除软件和配置文件，请使用 `apt-get purge`。你可以在下面看到。

```
apt-get purge snort
Reading package lists... Done
Building tree
Reading state information... Done
The following packages will be removed:
snort
--snip--
Do you want to continue?
```

## 软件包升级
