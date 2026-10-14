
```

// 根据需要替换以下行：
// example.com = 你的域名
// ns1 = 你的 DNS 服务器名称
// mta = 你的邮件服务器名称
example.com.      IN               ns1.example.com.
example.com.      IN      MX      10      mta.example.com.

// 将 IP 地址替换为你的 IP 地址。
www               IN      A       192.168.0.2
mta               IN      A       192.168.0.3
ns1               IN      A       192.168.0.1
```

现在，重启 BIND：

`matthew@semour:-$ sudo bind9 restart`

你对其他服务使用 `start`、`stop` 等命令。你现在应该已经准备就绪。

测试你的 DNS 服务器，编辑 `/etc/resol.conf`（备份原始文件！）并将其内容替换为以下，将 `example.com` 替换为你的域名，并将 `192.168.1.1` 替换为你新 DNS 服务器的地址：

```
search example.com
nameserver 192.168.1.1
```

然后，使用 `ping` 测试你的 DNS，查看它对 `example.com` 返回什么：

`matthew@semour:-$ dig example.com`

除了上面提到的 `ping` 工具外，`dig` 也是查看 DNS 记录的优秀工具。你可能还会发现 `nslookup` 和 `whois` 非常有用。此外，BIND9 包含了 `named-checkzone`，这对你可能有用。

## 参考文献

- `www.bind9.net`——一个包含大量关于 DNS 和 Bind 有用信息的网站。

Cricket Liu 和 Paul Albitz 编写的《DNS and BIND》是理解这两种技术的权威指南。

# 第 37 章 为 Ubuntu 使用编程工具

## 本章内容

- 使用 Linux 编程
- 使用 Ubuntu 提供的 C 项目管理工具
- 使用 GNU C 编译器
- 图形化开发工具
- 参考文献

如果你正在学习 C 或 C++ 编程或 Java 编程，这本书的这部分并不是入门的好地方。与 Perl、Python、PHP 甚至 C# 不同，使用这些语言产出某些东西不仅仅是浅尝辄止，因此本章主要关注 Ubuntu 为你作为程序员提供的工具。

无论你是想编译自己的代码还是别人的代码，GNU 编译器集合 (`gcc`) 都能提供帮助。它理解 C、C++、Fortran、Pascal 以及几十种流行语言，这意味着你可以尝试任何你感兴趣的内容。Ubuntu 还附带了数百个可以让你链接的库，从 GNOME 和 KDE 后面的 GUI 工具包到 XML 解析和游戏编码。有些使用 C，有些使用 C++，另一些则对两者都提供支持，这意味着你可以选择你最熟悉的工具。

## 为什么要用 C 或 C++？

每种程序语言都有其优点和缺点。某些语言让程序员的生活更轻松，但是以牺牲运行速度为代价的。像 Perl、Python 甚至 Java 这样的语言让用户更难保证内存是按顺序获取的或符合缓存。

## 使用 Linux 编程

C 是与 Unix 类操作系统（如 Linux 或 BSD）最相关的编程语言。在 20 世纪 70 年代，Unix 操作系统及其应用程序是用 C 编写的。由于 C 语言不直接针对特定的硬件架构，Unix 是最早的可移植操作系统之一。换句话说，Unix 的大部分代码不知道也不关心它运行在什么种计算机上。机器特性被隔离在 Unix 内核的几个模块中，使得当你迁移到不同的硬件架构时很容易修改它们。

Linux 内核大部分由 C 语言编写，这就是为什么 Linux 支持许多不同的 CPU。要了解更多从源码编译 Linux 内核的信息，请参见第 21 章“内核模块管理”。

C 是一种编译语言，这意味着你的源代码首先被处理器分析，然后翻译成汇编语言，最后被翻译成适用于目标 CPU 的机器指令。汇编器从机器指令创建二进制文件或对象文件。最后，链接器将对象文件与所需的软件支持链接起来。C 程序存储在以扩展名结尾的文本文件中，并且包含至少一个例程或函数，例如 `main()`；除非该文件是包含共享变量定义或其他数据或定义的包含文件（以 `.h` 扩展，也称为头文件）。

## 使用 Ubuntu 提供的 C 语言项目管理工具

C++ 是 C 语言的面向对象扩展。由于 C++ 是 C 的超集，C++ 编译器可以正确编译 C 程序，而且在 C++ 中可以编写非面向对象的代码。反之则不然：C 编译器无法编译 C++ 代码。

C++ 通过提供面向对象设计和代码的必要特性，扩展了 C 的功能。C++ 还提供了一些特性，例如将函数与数据结构相关联的能力，而这不需要使用基于类的面向对象技术。由于这些原因，C++ 语言允许通过编写 UNIX 程序，随着时间的推移转向面向对象的方法。

`gcc` 提供了对 C++ 编程的支持，编译 C++ 代码时，使用 `g++` 的名称运行它。

## 使用 Ubuntu 提供的 C 语言项目管理工具

Ubuntu 拥有许多让 C/C++ 程序员生活更轻松的工具。有工具可以创建程序（编辑器）、编译程序（`gcc`）、创建库（`ar`）、控制源码（`Git`、`Mercurial`、`Subversion`）、自动化构建（`make`）、调试程序（`gdb` 和 `ddd`）以及确定低效之处（`gprof`）。

接下来的章节将介绍 Ubuntu 自带的一些编程和项目管理工具。如果你有某些 UNIX 经验，你将熟悉这些程序的大部分，因为它们是程序员软件套件的传统补充。

## 使用 make 构建程序

你使用 `make` 命令来自动构建和安装 C 程序，对于这来说它是一个非常简单的工具！然而，如果你想创建自己的自动化构建，就需要学习 `make` 使用的特殊语法；后续章节将引导你完成基本的 `make` 设置。

## 使用 Makefiles

`make` 命令使用 `makefile` 自动构建和更新应用程序。`makefile` 是一个文本，其中包含了关于传递给编译器预处理器、编译器、汇编器和链接器的选项的指令。此外，`makefile` 还指定了对于特定的代码模块，要编译哪些源文件（以及编译器命令行），以及构建程序时需要哪些代码模块——这种机制称为依赖检查（dependency checking）。

`make` 命令的妙之处在于它的灵活性。你可以配合简单的 `makefile` 使用 `make`，也可以创建包含许多宏、规则或命令的复杂 `makefile`，这些命令可以在单个目录中工作，也可以递归遍历你的文件系统来构建程序、更新系统，甚至作为文档管理系统运行。`make` 命令适用于几乎任何程序，包括像 Tex 这样的文本处理系统。

你可以使用 `make` 来编译、构建和安装软件包，使用如下这样的简单命令：

```
matthew@seymour:-$ sudo make install
```

你可以使用默认的 `make`（通常称为 `Makefile`，首字母大写），或者可以使用 `make` 的 `-f` 选项来指定任何 `makefile`，例如 `MyMakefile`，如下：

```
matthew@seymour:-$ sudo make -f MyMakefile
```

取决于你的 `makefile` 的内容，可能还有其他选项。你可能有一个名为 `h.c` 的源文件，只需运行 `make hi`，其中 `make` 会自动计算出需要执行什么来构建最终的可执行文件。可以通过 `make -p` 查看 `make` 的内置规则。

## 使用宏和 Makefile 目标

在 `make` 中配合宏可以使程序具有移植性。宏允许其他操作系统的用户通过指定本地值（例如任何所需软件工具的名称和位置或文件名）来轻松地配置程序构建。在接下来的示例中，宏定义了编译器的名称（`CC`）、安装程序（`INS`）、链接器应该何处查找所需的库（`LIBDIR`）、所需库的名称（`LIBRARIES`）、源代码文件（`SRC`）、中间对象代码文件（`OBJS`）以及最终程序的名称（`PROG`）：

```
# 一个用于骨架程序的示例 makefile
CC= gcc
INS= install
INSDIR = /usr/local/bin
LIBDIR=-L/usr/X11R6/lib
LIBS=-Lxm -ISM
SRC= skel.c
OBJS=skel.o
PROG=tux

$(PROG): $(OBJS)
	$(CC) -o $(PROG) $(OBJS) $(LIBS)

$(OBJS): $(SRC)
	$(CC) -c $(SRC) $(LIBDIR)

install: $(PROG)
	$(INS) $(PROG) $(DINSDIR)

clean:
	rm -f $(OBJS) $(PROG)
```
