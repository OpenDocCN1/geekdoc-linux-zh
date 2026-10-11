
## 排版约定

与所有计算机类书籍一样，我们使用特定的排版约定来传达信息。*定义*或术语的首次出现以*斜体*显示，例如本句开头的“*定义*”一词。*斜体*还用于*强调*、引用其他作品以及示例中的评论。变量项（如参数或文件名）以*这种*方式呈现。偶尔，当需要**强烈**强调某一点时，我们会使用粗体字体。

计算机上存在的事物使用等宽字体，例如文件名（*foo.c*）和命令名称（*ls*、*grep*）。你输入的简短片段还会被单引号包围：'`ls -L *.c`'。

$` 和 >` 分别是 Bourne shell 的主提示符和次提示符，用于显示交互式示例。在示例中，**用户输入**的字体与*常规计算机输出*不同。示例如下所示：

```
$ ls -1               查看文件。选项是数字 1，而不是字母 I
foo
bar
baz
```

我们更倾向于使用 Bourne shell 及其变体（*ksh93*、*Bash*），而非 C shell；因此，我们所有的示例仅展示 Bourne shell。请注意，C shell 的引号和续行规则有所不同；如果你使用 C shell，那就得自己负责了。^[6]

当引用程序中的函数时，我们在函数名称后添加一对空括号：*printf()*、*strcpy()*。当引用手册页（可通过 *man* 命令访问）时，我们遵循标准的 Unix 约定，将命令或函数名称以斜体书写，并在其后以正常字体括号标注章节号：*awk(1), printf(3)*。

## 获取 Unix 和 GNU 源代码的位置

你可能希望拥有本书中使用的程序的副本，以便进行自己的实验和回顾。所有源代码都可通过互联网获取，并且你的 GNU/Linux 发行版包含了 GNU 工具包的源代码。

> 6 请参阅 *csh(1)* 和 *tcsh(1)* 手册页，以及 Paul DuBois 所著的书籍 *Using csh & tcsh*（O'Reilly & Associates 出版社，美国加利福尼亚州塞巴斯托波尔，1995 年）。ISBN：1-56592-132-1。

## Unix 代码

各种“古老”版本的 Unix 档案由 UNIX 遗产协会（TUHS）维护，地址为 `http://www.tuhs.org`。

最感兴趣的是，你可以浏览旧的 Unix 源代码的网络档案。请从 `http://minnie.tuhs.org/UnixTree/` 开始。本书中的所有示例代码都来自第七版研究版 UNIX 系统，也称为“V7”。

TUHS 网站物理位置位于澳大利亚，但世界各地的存档都有镜像——请参见 `http://www.tuhs.org/archive_sites.html`。该页面还指出，可以使用 `rsync` 对存档进行镜像。（如果你没有 `rsync`，请参见 `http://rsync.samba.org/`：它在 GNU/Linux 系统中是标准的。）

你需要大约 2–3 GB 的磁盘空间来复制整个档案。要复制档案，请创建一个空目录，并在其中运行以下命令：

```
mkdir Applications 4BSD PDP-11 PDP-11/Trees VAX Other

rsync -avz minnie.tuhs.org::U4_Root .
rsync -avz minnie.tuhs.org::U4_Applications Applications
rsync -avz minnie.tuhs.org::U4_4BSD 4BSD
rsync -avz minnie.tuhs.org::U4_PDP11 PDP-11
rsync -avz minnie.tuhs.org::U4_PDP11_Trees PDP-11/Trees
rsync -avz minnie.tuhs.org::U4_VAX VAX
rsync -avz minnie.tuhs.org::U4_Other Other
```

你可能希望省略复制 `Trees` 目录，该目录包含几个 Unix 版本的解压内容，占用大约 700 MB 的磁盘空间。

你也可能希望查阅 TUHS 邮件列表，看看是否有人能为你提供存档的 CD-ROM 副本，以避免通过互联网传输如此多的数据。

澳大利亚南方风暴软件公司（Southern Storm Software, Pty. Ltd.）的同仁们已将 V7 用户级代码的一部分“现代化”，使其可以在当前系统（最显著的是 GNU/Linux）上编译和运行。可以从他们的网站下载此代码。^[7]

值得注意的是，V7 代码中不包含任何版权或许可声明。作者主要为自己和他们的研究编写代码，将许可问题留给 AT&T 的企业许可部门。

## GNU 代码

如果你正在使用 GNU/Linux，那么你的发行版会附带源代码， presumably 采用其使用的某种打包格式（Red Hat RPM 文件、Debian DEB 文件、Slackware .tar.gz 文件等）。书中许多示例来自 GNU Coreutils 版本 5.0。找到适合你的 GNU/Linux 发行版的相应 CD-ROM，并使用相应的工具提取代码。或者按照下面几段说明获取代码。

如果你更喜欢自行从 GNU ftp 站点检索文件，你可以在 `ftp://ftp.gnu.org/gnu/coreutils/coreutils-5.0.tar.gz` 找到它们。

你可以使用 `wget` 实用程序检索文件：

```
$ wget ftp://ftp.gnu.org/gnu/coreutils/coreutils-5.0.tar.gz
获取发行版
... 文件获取时会有大量输出 ...
```

或者，你可以使用古老的传统 ftp 来检索文件：

```
$ ftp ftp.gnu.org
连接到 GNU ftp 站点
已连接到 ftp.gnu.org (199.232.41.7)。
220 GNU FTP 服务器就绪。
Name (ftp.gnu.org:arnold): anonymous
使用匿名 ftp
331 请指定密码。
Password:
密码不会在屏幕上回显
230-如果你在使用 GNU 软件或其下载方面遇到任何问题，
230-请将你的问题提交给 <gnu@gnu.org>。
230 登录成功。玩得开心。
远程系统类型是 UNIX。
使用二进制模式传输文件。
省略了大量措辞
ftp> cd /gnu/coreutils
切换到 Coreutils 目录
250 目录更改成功。
ftp> bin
200 正在切换到二进制模式。
ftp> bash
使用 # 符号作为进度指示器
井号标记打印已开启（1024 字节/井号标记）。
ftp> get coreutils-5.0.tar.gz
获取文件
local: coreutils-5.0.tar.gz remote: coreutils-5.0.tar.gz
227 进入被动模式 (199,232,41,7,86,107)
150 正在为 coreutils-5.0.tar.gz 打开 BINARY 模式数据连接 (6020616 字节)
######...###...####...#########...#####...###...##...##...###########...
- 226 文件发送成功。
在 2.03e+03 秒内接收了 6020616 字节 (2.9 Kbytes/sec)
ftp> quit
注销
221 再见。
```

获取文件后，按如下方式提取：

```
$ gzip -dc < coreutils-5.0.tar.gz | tar -xvpf -
. . 文件提取时会有大量输出 . . .
提取文件
```

使用 GNU tar 的系统可以使用此命令：

```
$ tar -xvpf coreutils-5.0.tar.gz
提取文件
. . 文件提取时会有大量输出 . . .
```

为了遵守 GNU 通用公共许可证，以下是本书引用的所有 GNU 程序的版权信息。所有程序都是“自由软件；你可以重新分发它和/或根据自由软件基金会发布的 GNU 通用公共许可证的条款修改它；许可证版本为 2 或（由你选择）任何更高版本。”请参见附录 C“GNU 通用公共许可证”第 657 页，了解 GNU 通用公共许可证的文本。

| Coreutils 5.0 文件 | 版权日期 |
| :--- | :--- |
| lib/safe-read.c | 版权所有 © 1993–1994, 1998, 2002 |
| lib/safe-write.c | 版权所有 © 2002 |
| lib/utime.c | 版权所有 © 1998, 2001–2002 |
| lib/xreadlink.c | 版权所有 © 2001 |
| src/du.c | 版权所有 © 1988–1991, 1995–2003 |
| src/env.c | 版权所有 © 1986, 1991–2003 |
| src/install.c | 版权所有 © 1989–1991, 1995–2002 |
| src/link.c | 版权所有 © 2001–2002 |
| src/ls.c | 版权所有 © 1985, 1988, 1990, 1991, 1995–2003 |
| src/pathchk.c | 版权所有 © 1991–2003 |
| src/sort.c | 版权所有 © 1988, 1991–2002 |
| src/sys5.2.h | 版权所有 © 1997–2003 |
| src/wc.c | 版权所有 © 1985, 1991, 1995–2002 |

| Gawk 3.0.6 文件 | 版权日期 |
| :--- | :--- |
| eval.c | 版权所有 © 1986, 1988, 1989, 1991–2000 |

### Gawk 3.1.3 文件

| 文件 | 版权日期 |
|:-----|:----------------|
| awk.h | 版权所有 © 1986, 1988, 1989, 1991–2003 |
| builtin.c | 版权所有 © 1986, 1988, 1989, 1991–2003 |
| eval.c | 版权所有 © 1986, 1988, 1989, 1991–2003 |
| io.c | 版权所有 © 1986, 1988, 1989, 1991–2003 |
| main.c | 版权所有 © 1986, 1988, 1989, 1991–2003 |
| posix/gawkmisc.c | 版权所有 © 1986, 1988, 1989, 1991–1998, 2001–2003 |

### Gawk 3.1.4 文件

| 文件 | 版权日期 |
|:-----|:----------------|
| builtin.c | 版权所有 © 1986, 1988, 1989, 1991–2004 |

### GLIBC 2.3.2 文件

| 文件 | 版权日期 |
|:-----|:----------------|
| locale/locale.h | 版权所有 © 1991, 1992, 1995–2002 |
| posix/unistd.h | 版权所有 © 1991–2003 |
| time/sys/time.h | 版权所有 © 1991–1994, 1996–2003 |

### Make 3.80 文件

| 文件 | 版权日期 |
|:-----|:----------------|
| read.c | 版权所有 © 1988–1997, 2002 |

## 获取本书使用的示例程序

本书使用的示例程序可在 `http://authors.phttr.com/robbins` 找到。

## 关于封面

> “这是绝地武士的武器……，一种更文明时代的优雅武器。一千多个世代以来，绝地武士是旧共和国中正义与和平的守护者。在黑暗时代之前，在帝国之前。”
> —欧比旺·克诺比—

你可能想知道我们为什么选择在封面上放一把光剑，并在书的内部一直使用它。它代表什么，以及它如何与 Linux 编程相关？

