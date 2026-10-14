

虽然存在许多流行的编程语言，但其中两种占主导地位。大多数为现代系统编写的程序都是用 C 或 C++ 编写的。在下面的示例中，我们将编译一个 C 程序。

用高级编程语言编写的程序通过使用另一个程序进行处理将其转换为机器语言，该程序称为编译器。某些编译器将高级指令翻译成汇编语言，然后使用汇编器执行最终的翻译阶段，将其转换为机器语言。

编译时经常使用的一种过程称为链接。程序执行的常见任务有很多。例如打开一个文件。许多程序都会执行此任务，但让每个程序都实现自己的打开文件例程是浪费的。更合理的做法是有一个单一的编程片段知道如何打开文件，并允许所有需要它的程序共享它。通过所谓的库来实现对常见任务的支持。它们包含多个例程，每个例程执行多个程序可以共享的某个常见任务。如果我们查看 /lib 和 /usr/lib 目录，我们可以看到其中许多库的位置。程序链接器用于在编译器的输出和编译后的程序所需的库之间形成连接。此过程的最终结果是可执行的程序文件，准备使用。

## 所有程序都需要编译吗？

不是的。正如我们所见，有 shell 脚本等程序不需要编译。它们是直接执行的。这些是用所谓的脚本或解释型语言编写的。这些语言近年来变得越来越流行，其中包括 Perl、Python、PHP、Ruby 等。

脚本语言由一个名为解释器的特殊程序执行。解释器输入程序文件并读取并执行其中包含的每条指令。一般来说，解释型程序的执行速度比编译型程序慢得多。这是因为解释型程序中的每条源代码指令在执行时都会被翻译，而对于编译型程序，源代码指令只翻译一次，并且这种翻译永久记录在最终的可执行文件中。

为什么解释型语言如此受欢迎？对于许多编程任务，结果“足够快”，但真正的优势在于，通常开发解释型程序比编译型程序更快、更容易。程序通常在代码、编译、测试的重复循环中开发。随着程序规模的增长，循环中的编译阶段可能变得相当长。解释型语言去除了编译步骤，从而加快了程序开发速度。

## 编译一个 C 程序

让我们编译一些东西。在此之前，我们需要一些工具，如编译器、链接器和 make。在 Linux 环境中几乎通用使用的 C 编译器称为 gcc（GNU C 编译器），最初由 Richard Stallman 编写。大多数发行版默认不安装 gcc。我们可以通过以下方式检查编译器是否存在：

```
[me@linuxbox ~]$ which gcc
/usr/bin/gcc
```

本示例中的结果表明编译器已安装。

### TIP
您的发行版可能有一个元包（包的集合）用于软件开发。如果是这样，如果您打算在系统上编译程序，请考虑安装它。如果您的系统不提供元包，请尝试安装 gcc 和 make 包。在许多发行版上，这足以进行以下练习。

## 获取源代码

对于我们的编译练习，我们将从 GNU 项目编译一个名为 diction 的程序。这个方便的小程序会检查文本文件的写作质量和风格。作为程序而言，它相当小，易于构建。

按照惯例，我们首先将创建一个名为 src 的源代码目录，然后使用 ftp 将源代码下载到其中。

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

虽然我们在前面的示例中使用了 ftp，这是传统做法，但下载源代码还有其他方法。例如，GNU 项目也支持使用 HTTPS 下载。我们可以使用 wget 程序下载 diction 源代码。

