

一般来说，解释型程序的执行速度比编译型程序慢得多。这是因为在解释型程序中，每条源代码指令在执行时都会被翻译一次，而在编译型程序中，源代码指令只翻译一次，并且该翻译永久记录在最终的可执行文件中。

那么为什么解释型语言如此流行呢？对于许多编程任务，结果已经“足够快”了，但真正的优势在于，通常开发解释型程序比编译型程序更快、更容易。程序通常在代码、编译、测试的循环中开发。随着程序规模的增大，循环中的编译阶段可能会变得相当长。解释型语言去除了编译步骤，从而加快了程序开发速度。

## 编译 C 程序

让我们编译点东西。在此之前，我们需要一些工具，比如编译器、链接器和 make。在 Linux 环境中几乎通用使用的 C 编译器称为 gcc（GNU C 编译器），最初由 Richard Stallman 编写。大多数发行版默认不安装 gcc。我们可以通过以下方式检查编译器是否存在：

```
[me@linuxbox ~]$ which gcc
/usr/bin/gcc
```

本示例中的结果表明编译器已安装。

**提示：** 你的发行版可能有一个元包（包的集合）用于软件开发。如果是这样，如果你打算在系统上编译程序，请考虑安装它。如果你的系统没有提供元包，请尝试安装 gcc 和 make 包。在许多发行版上，这足以完成下面的练习。

## 获取源代码

对于我们的编译练习，我们将编译 GNU 项目的一个程序 diction。这是一个很方便的小程序，用于检查文本文件的写作质量和风格。作为程序而言，它相当小且易于构建。

按照惯例，我们首先将创建一个名为 src 的源代码目录，然后使用 ftp 将源代码下载到其中：

```
[me@linuxbox ~]$ mkdir src
[me@linuxbox ~]$ cd src
[me@linuxbox src]$ ftp ftp.gnu.org
Connected to ftp.gnu.org.
220 GNU FTP server ready.
Name (ftp.gnu.org:me): anonymous
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> cd gnu/diction
250 Directory successfully changed.
ftp> ls
200 PORT command successful. Consider using PASV.
150 Here comes the directory listing.
-rw-r--r--   1 1003  65534   68940 Aug 28  1998 diction-0.7.tar.gz
-rw-r--r--   1 1003  65534   90957 Mar 04  2002 diction-1.02.tar.gz
-rw-r--r--   1 1003  65534  141062 Sep 17  2007 diction-1.11.tar.gz
226 Directory send OK.
ftp> get diction-1.11.tar.gz
local: diction-1.11.tar.gz remote: diction-1.11.tar.gz
200 PORT command successful. Consider using PASV.
150 Opening BINARY mode data connection for diction-1.11.tar.gz (141062 bytes).
226 File send OK.
141062 bytes received in 0.16 secs (847.4 kB/s)
ftp> bye
221 Goodbye.
[me@linuxbox src]$ ls
diction-1.11.tar.gz
```

注意：由于我们在编译时是此源代码的“维护者”，我们将把它保存在 ~/src 中。由发行版安装的源代码将被安装在 /usr/src 中，而供多用户使用的源代码通常安装在 /usr/local/src 中。

正如我们所见，源代码通常以压缩的 tar 文件形式提供。有时称为 tarball，该文件包含源代码树，即构成源代码的目录和文件的层次结构。到达 ftp 站点后，我们查看可用的 tar 文件列表并选择最新版本进行下载。使用 ftp 中的 get 命令，我们将文件从 ftp 服务器复制到本地机器。

下载 tar 文件后，必须将其解包。这是用 tar 程序完成的：

```
[me@linuxbox src]$ tar xzf diction-1.11.tar.gz
```

```
[me@linuxbox src]$ ls
diction-1.11      diction-1.11.tar.gz
```

提示：diction 程序像所有 GNU 项目软件一样遵循源代码打包的某些标准。Linux 生态系统中大多数其他源代码也遵循此标准。标准的一个要素是，当源代码 tar 文件被解包时，将创建一个包含源代码树的目录，并且该目录将命名为 project-x.xx，从而包含项目的名称及其版本号。此方案允许轻松安装同一程序的多个版本。然而，在解包之前检查树的布局通常是个好主意。一些项目不会创建目录，而是直接将文件交付到当前目录。这会在你原本井然有序的 src 目录中造成混乱。为避免这种情况，使用以下命令检查 tar 文件的内容：

```
tar tzvf tarfile | head
```

## 检查源代码树

解包 tar 文件会创建一个名为 diction-1.11 的新目录。该目录包含源代码树。让我们看一下内部：

```
[me@linuxbox src]$ cd diction-1.11
[me@linuxbox diction-1.11]$ ls
config.guess   diction.c      getopt.c       nl
config.h.in    diction.pot    getopt.h       nl.po
config.sub     diction.spec   getopt_int.h   README
configure      diction.spec.in INSTALL        sentence.c
configure.in   diction.texi.in install-sh     sentence.h
COPYING        en             Makefile.in    style.1.in
de             en_GB          misc.c         style.c
de.po          en_GB.po       misc.h         test
diction.1.in   getopt1.c      NEWS
```

其中，我们看到许多文件。GNU 项目的程序以及许多其他程序会提供文档文件 README、INSTALL、NEWS 和 COPYING。这些文件包含程序的描述、如何构建和安装它的信息以及其许可条款。在尝试构建程序之前，仔细阅读 README 和 INSTALL 文件始终是个好主意。

