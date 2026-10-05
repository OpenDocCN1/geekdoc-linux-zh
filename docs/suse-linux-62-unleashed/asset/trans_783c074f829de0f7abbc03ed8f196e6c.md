

# 常用 Linux 命令与工具 附录 C

section ImageMagick 通常在终端窗口的命令行中后台启动：

```
# display &
```

# dmesg

dmesg 命令打印系统启动日志。该程序对于诊断系统问题非常有用，它可以列出系统启动时发现的软件和服务硬件设备。

# du

du 命令显示各种文件或目录占用的磁盘空间，并可以显示系统中磁盘空间占用最多或最少的地方。

# dump

dump 命令通常由 root 用户使用，用于创建整个文件系统或选目录的备份。dump 命令的配套程序是 restore 命令，它可以从 dump 备份中提取文件和目录。

# echo

echo 将字符串打印到显示器。echo 命令通常用于将文本行打印到显示控制台，或者通过重定向输出到文件、设备、程序或 shell 的标准输出。-e 选项允许在输出字符串中使用某些控制字符。

# ed

ed 是一个极其精简的行 编辑器。

# edquota

edquota 程序供 root 用户使用，用于更改用户可以使用的磁盘空间大小。它与 quota、quotaon 或 quotaoff 命令配合使用。

![](img/cbac72550c7126a22162e94d91a0c360_1036_0.png)

# 附录
第五部分

# elm

elm 是一个邮件处理程序，你可以用它创建、编写、编辑和发送邮件。你可以将邮件组织到不同的文件夹中，还可以组织入邮件分类的方式。该程序类似于 pine 邮件。

# emacs

emacs 是 GNU 文本（编辑宏）编辑器，尽管也有 Emacs 编辑器变体。它不仅可以编辑文本文件，还可以作为日历、日记、日程安排等。emacs 还是一个支持编程和电子邮件的完整环境。

# env

env 命令用于查看导出的环境变量。命令的结果是一个列列表，变量名在左侧，与变量关联的值在右侧。该命令执行时不带任何参数。因此，输入 env 可能会得到一个类似于下面的列表（未显示所有输出）：

```
$ env
PWD=/home/bball
PAGER=less
HOSTNAME=stinkpad
LS_OPTIONS=-N --color=tty -T 0
ignoreof=0
POVRAYOPT=-1/usr/lib/povray/include
QTDIR=/usr/lib/qt
OPENWINHOME=/usr/openwin
LESSKEY=/etc/lesskey.bin
LESSOPEN=$lesspipe.sh %%
MANPATH=/usr/local/man:/usr/man:/usr/X11R6/man:/man:/usr/
~/openwin/man/man:/usr/man/de
PS1=@u@h:\w \
PS2=> \
NTPSERVER=news
KDIR=/opt/kde
LESS=-M -S -I
HISTCONTROL=ignoredups
MACHYPE=i686-pc-linux-gnu
XKEYSDB=/usr/X11R6/lib/X11/XkeysDB/n/XkeysDB
MAIL=/var/spool/mail/bball
```
EDITOR=/usr/bin/pico
LANG=POSIX
GNOMEDIR=/opt/gnome
COLORTERM=1
INFPATH=/usr/local/info:/usr/info
DISPLAY=:0.0
LOGNAME=bball
SHLVL=4

MINCOM=-c on
INFDIR=/usr/local/info:/usr/info
SHELL=/bin/bash
PRINTER=lp
HOSTTYPE=i686
OSTYPE=linux-gnu
WINDOWMANAGER=/usr/X11R/bin/kde
HOME=/home/bball
TERM=extern
XLSPATH=/usr/X11R6/lib/X11/nls
no_proxy=localhost
PGDATA=/var/lib/postgresql/data
PATH=/usr/local/bin:/bin:/usr/X11R6/bin:/bin:
...
```

# fc

fc 命令用于编辑历史文件。传递给它的参数（如果有）可以用于从历史文件中选择一个命令范围。然后该列表被放置在一个编辑 shell 中。使用哪个 fc 取决于变量 FCEDIT 的值。如果该变量没有值，命令将查看 EDITOR 变量。如果那里也没有，则使用默认编辑器 vi。

# fdformat

此命令仅对软盘执行低级格式化。此之后，你必须使用 mkfs 命令在磁盘上放置指定的文件系统。

# fetchmail

这个由 Eric S. Raymond 编写的程序可以从你的互联网服务提供商 (ISP) 获取邮件，并且处理除邮局协议 (POP) 之外的电子邮件协议。你可以单独使用此程序或在 shell 脚本中使用它在建立点点连接 (PPP) 后获取邮件。

![](img/cbac72550c7126a22162e94d91a0c360_1038_0.png)

# fg

fg 命令将后台作业带到前台。当有多个作业运行时，fg 命令非常有用。使用哪个 fc 取决于变量 FCEDIT 的值。如果该变量没有值，命令将查看 EDITOR 变量。如果那里也没有，则使用默认编辑器 vi。

# file

file 命令用于确定文件类型。它检查文件内容以猜测文件类型，而不是依赖扩展名。

# finger

finger 命令用于查询用户信息。它可以显示当前登录系统的用户信息。

# fmt

fmt 程序将输入文本格式化为列。它对于对齐文件中的文本有用。

# free

free 命令显示系统使用了多少内存。它对于监控系统资源有用。

# ftp

这是文件传输协议。你可以使用此命令从远程计算机发送和接收文件。

# gnuplot

gnuplot 程序可以生成数据的图形显示。它对于创建图表和其他图形有用。

# grep

grep（全局正则表达式）命令在文件中搜索模式。命令的语法为 grep <text> <file>。在下面的示例中，我正在当前目录的所有文件中搜索该文本：

```
# grep tools *
```

# groff

groff 是 groff 文档格式化程序的前端。该程序默认调用 troff 程序。

# gs

这是 Ghostscript 解释器。该程序可以解释并准备 PostScript 文档，并在三十多种显示器上打印。

# gunzip

使用此程序将通过 gzip 命令压缩的文件解压回原始格式。

# gv

gv 是 PostScript 和 PDF 文档查看器，这个 X11 客户端预览并打印 PostScript 和便携文档，适用于阅读文档或在打印前预览图形或文档。可以在后台启动 gv，或在命令行上指定文件：

```
# gv myPostscriptdoc.ps &
```

# gzip

gzip 是 GNU 版本的 zip 压缩软件。语法可以简单为 gzip <filename>

许多时候，在命令和要压缩的文件名之间还会包含一些参数。

