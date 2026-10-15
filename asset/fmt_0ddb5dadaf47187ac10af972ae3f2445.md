
- `F9` 打开菜单，你可以使用方向键进行导航。
- `F5` 复制文件。
- `Tab` 在两个窗格之间切换。

# 磁盘空间使用

要查看当前目录下的文件占用了多少空间，你可以使用 `du` 命令（考虑磁盘使用）。`du` 列出目录和每个子目录的磁盘使用情况。`du -h` 以“人类可读”格式列出输出（即以 KB、MB 或 GB 为单位）。`du -s` 摘要）告诉你目录的总使用量。

要查看每个文件系统占用了多少磁盘，使用 `df` 命令（考虑磁盘满）。通常，最好对 `df` 使用 `-h` 选项，以便你可以很容易地理解输出。

# 查找文件

有时，你可能想要查找具有给定名称的文件。在命令行中有两种常用的方法：使用 `find` 命令和 `locate` 命令。

## 使用 find

`find` 命令拥有数量令人眼花缭乱选项，有时你会遇到复杂的 `find` 使用示例。但在大多数你想使用它的情况下，情况通常是这样的：你认为某个目录（例如 `~/temp`）下方存在一个具有特定名称的文件。切换到目录并输入：

```
user@bible:~/temp find
```

你将看到当前目录下的所有内容。因此，如果你正在寻找一个文件并输入：

```
user@bible:~/ find . | grep
```

你将得到一些输出，显示如果在 `~/temp` 目录下任何位置存在一个包含 `alias` 字符串的文件（或任何包含该字符串的文件名），路径将会显示。在大多数情况下，这就是你所需要的，你会在其他地方读到“正确”使用 `find` 命令的方法是执行：

```
user@bible:~/ find . -name -print
```

这会找到当前目录下任何具有精确匹配名称的文件。

有时，你可能想将 `find` 的输出管道到另一个程序，如 `cpio`（在章节中查看更多关于 `cpio` 的信息），或使用 `find` 内置的 `-exec` 选项对文件列表执行另一个命令。例如：

```
find -name -exec lpr {} \;
```

这会执行 `lpr` 命令并打印 `find` 命令找到任何文件。`{}`（大括号）代表 `find` 输出中找到的每一个文件。`\` 用于终止命令。

## 使用 locate

`locate` 命令是 `findutils-locate` 软件包的一部分。它获取的关于系统文件位置的信息每天更新一次，因此除非手动更新数据库，否则它无法找到最近创建或移动的文件。如果安装了该软件包，数据库将每天自动更新，但你可以使用 `updatedb` 命令创建或更新数据库。

使用 `locate` 查找文件就像这个示例一样简单：

```
user@bible:~ locate traceroute
/usr/bin/traceroute
/usr/bin/traceroute6
/usr/share/man/man1/traceroute1.gz
/usr/share/man/man1/traceroute6.gz
```

## 处理文件

请注意，任何包含给定字符串（在此处为 `traceroute`）的文件都将被找到。

> 注意：`locate` 实用程序位于 `/usr/bin/locate`，但默认不安装。它非常有用，但在桌面系统上，它每天更新数据库时会占用资源。这就是为什么它没有包含在默认安装中的原因。在现代系统上，你几乎察觉不到它的存在，你会对能够轻松找到系统上的任何文件感到感激。

`locate` 数据库的更新每天通过 `/etc/cron.daily/updated` 文件完成，该文件从 `/etc/sysconfig/locate` 读取参数并调用 `updatedb` 命令。在 `/etc/sysconfig/locate` 中，你可以设置是否进行自动更新，以及你想从数据库中排除哪些路径（默认排除临时文件和队列文件，以及可移动介质）。

## 使用 Konqueror 查找文件

`Konqueror` 有一个菜单（工具 -> 查找文件，快捷键为 `Ctrl+F`），当它以管理器模式运行时（如图 13-1 所示），它可以搜索显示目录下的文件，该图显示了在整个系统中搜索文件模式 `*` 的部分过程。

图 13-1

`Konqueror` 查找文件

![](img/e749d3c47634a5bbb94e11699efbe992_386_0.png)

# 第三部分 在 SUSE Linux 中使用命令行

## 在 GNOME 中查找文件

在最近的 SUSE 版本中，GNOME 文件管理器 `Nautilus` 内了 `Beagle` 桌面搜索功能（见图 13-2）。因此你既按名称也可以按内容查找文件。你可以通过点击绿色的“+”图标添加下拉列表，将搜索标准限制在特定位置和特定文件类型。

## 在 mc 中查找文件

`mc` 也具有查找功能，并且搜索文件内内容的能力。要使用 `mc` 中的查找功能，从“命令”菜单中选择“查找文件”（或按 `Alt+?`）。然后你可以在出现的对话框中输入文件名模式和要搜索的文本内容（见图 13-3）。![](img/e749d3c47634a5bbb94e11699efbe992_387_0.png)

# 图 13-3

按名称查找文件

![](img/e749d3c47634a5bbb94e11699efbe992_388_0.png)

## 按内容查找文件：Beagle

`openSUSE` 和 `SLED 10` 的最新版本包含 `Beagle` 搜索工具。它始终后台运行，并通过文本内容对系统上的文件建立索引。它可以读取多种文件类型，并在主目录下的隐藏目录 `~/.beagle` 中维护索引。`Beagle` 默认索引你访问过的网页和电子邮件。索引目录可能会变得很大。在我的桌面机器上，它目前的大小约为 2GB，包含超过 25 万个文件。

`GNOME` 和 `KDE` 桌面都通过启动菜单访问 `Beagle` 搜索。有一个搜索框，可以搜索词语并包含该词语的文件列表（见图 13-4）。

# 第三部分 在 SUSE Linux 中使用命令行

图 13-4

使用 `Beagle` 搜索

![](img/e749d3c47634a5bbb94e11699efbe992_389_0.png)

## 查看文件和文件类型

通常我们 own想要查看文件的内容，因为它们包含某些有用信息。问题是文件有很多，在 Windows 世界中，扩展名（`.doc`, `.txt` 等）决定了系统使用哪种应用程序。Linux 比此更好：使用命令查看文件的真实类型。

## file 命令

要使用 `file` 命令，只需输入 `file` 后跟你想分析的文件。例如：

```
user@bible:~/temp file index.html
index.html: HTML document
user@bible:~/temp file realworld.doc
realworld.doc: Office Document
```

我们知道 `index.html` 是真实文件，`realworld.doc` 是一个文档。让我们看看更改扩展名会发生什么：

```
user@bible:~/temp cp index.html strange.doc
user@bible:~/temp file strange.doc
strange.doc: HTML document
```

在这里，`file` 没有被扩展名欺骗。实际上这并不很难，但你需要将 Word 文档的前 8 个字节拷贝到一个新文件中来这样做：

```
user@bible:~/temp dd if=realworld.doc of=newfile.doc bs=1 count=8
user@bible:~/temp cat index.html > newfile.doc
user@bible:~/temp file newfile.doc
newfile.doc: Office Document
```

你可以检查 `file` 是如何做的：

```
user@bible:~/temp grep /usr/share/misc/magic
0 string \317067\01043 Office Document
0 string \320317\021340\241261\032341 Office Document
0 string \333245\0100 Office Document
user@bible:~/temp -b newfile.doc more
000000 310 317 021 034 262 031 342 074 041 117 103 124 131 120
```

该命令提供了文件的实际转储，你可以看到 Office 文档的第二种可能的签名位于开头。由于你正在将输出管道到 `q` 来退出 `more` 命令，你可以随时终止它。

如果你遇到一个 `file` 命令无法提供有用信息的文件（它可能只报告“data”），可能尝试使用 `cat -v`、`less` 查看，

## strings, ghex, khedit, 和 antiword

## 第三部分 在 SUSE Linux 中使用命令行
