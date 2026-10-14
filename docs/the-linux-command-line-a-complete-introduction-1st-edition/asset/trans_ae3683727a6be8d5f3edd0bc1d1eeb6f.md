

许多程序都会执行此任务，但让每个程序都实现自己的打开文件例程是浪费的。更合理的做法是有一段程序专门知道如何打开文件，并允许所有需要它的程序共享它。通过所谓的库来提供对常见任务的支持。它们包含多个例程，每个例程执行多个程序可以共享的某个常见任务。如果我们查看 /lib 和 /usr/lib 目录，就可以看到它们中的许多所在的位置。程序链接器用于在编译器的输出和编译后的程序所需的库之间形成连接。此过程的最终结果是可执行的程序文件，准备好使用。

## 所有程序都需要编译吗？

不是。 正如我们所见，一些程序，例如 shell 脚本，不需要编译，而是直接执行。这些是用所谓的脚本或解释型语言编写的。这些语言近年来变得越来越流行，其中包括 Perl、Python、PHP、Ruby 等。

脚本语言由一个名为解释器的特殊程序执行。解释器输入程序文件并读取并执行其中包含的每个指令。一般来说，解释型程序的执行速度比编译型程序慢得多。这是因为解释型程序中的每条源代码指令在执行时都会被翻译，而对于编译型程序，源代码指令只翻译一次，并且这种翻译永久记录在最终的可执行文件中。

那么为什么解释型语言如此受欢迎呢？对于许多编程任务，结果“足够快”，但真正的优势是，与编译型程序相比，开发解释型程序通常更快、更轻松。程序通常在代码、编译、测试的重复循环中开发。随着程序规模的增长，循环中的编译阶段可能会变得相当长。解释型语言去除了编译步骤，从而加快了程序开发速度。

## 编译 C 程序

让我们编译一些东西。在此之前，我们需要一些工具，如编译器、链接器和 make。在 Linux 环境中几乎通用使用的 C 编译器称为 gcc（GNU C 编译器），最初由 Richard Stallman 编写。大多数发行版默认不安装 gcc。我们可以通过以下方式检查编译器是否存在：

```text
[me@linuxbox ~]$ which gcc
/usr/bin/gcc
```

此示例中的结果表明编译器已安装。

**Note:** *Your distribution may have a metapackage (a collection of packages) for software development. If so, consider installing it if you intend to compile programs on your system. If your system does not provide a metapackage, try installing the gcc and make packages. On many distributions, they are sufficient to carry out the exercise below.*

## 获取源代码

对于我们的编译练习，我们将从 GNU 项目编译一个名为 diction 的程序。这个方便的小程序会检查文本文件的写作质量和风格。作为程序而言，它相当小且易于构建。按照惯例，我们首先将创建一个名为 src 的源代码目录，然后使用 ftp 将源代码下载到其中：

```text
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
-rw-r--r-- 1 1003 65534  68940 Aug 28  1998 diction-0.7.tar.gz
-rw-r--r-- 1 1003 65534  90557 Mar 04  2002 diction-1.02.tar.gz
-rw-r--r-- 1 1003 65534 141062 Sep 17  2007 diction-1.11.tar.gz
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

**Note:** *Since we are the maintainer of this source code while we compile it, we will keep it in `~/src`. Source code installed by your distribution will be installed in `/usr/src`, while source code intended for use by multiple users is usually installed in `/usr/local/src`.*

正如我们所见，源代码通常以压缩的 tar 文件形式提供。有时称为 *tarball*，该文件包含 *source tree*，即构成源代码的目录和文件的层次结构。到达 FTP 站点后，我们检查可用的 tar 文件列表并选择最新版本进行下载。使用 ftp 中的 get 命令，我们将文件从 FTP 服务器复制到本地机器。

