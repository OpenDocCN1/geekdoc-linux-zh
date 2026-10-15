
caught attribute error

在这种情况下，你将异常处理代码从函数移动到调用代码中，并更新它以处理特定的异常。在 `except` 子句中，你定义了要处理的特定错误（在这种情况下，你知道如果传递一个整数，就会产生 `AttributeError`）。这允许调用者以其确定的任何方式处理问题。如果需要由一个异常子句处理多个异常，可以在括号中提供异常列表。用户还可以使用 `raise` 语句抛出已有的或新的异常。

Python 还允许创建新的异常（异常本身本身类类）。表 27.2 提供了标准异常的列表。

### 表 27.2 Python 中的典型异常（不完整）

| Python 异常 | 含义 |
|---|---|
| ArithmeticError | 表示溢出、除以零、浮点错误 |
| AssertionError | 当 `assert` 断言失败时抛出 |
| AttributeError | 对象不支持属性引用 |
| MemoryError | 操作运行内存不足 |
| NameError | 命名空间中未找到本地或全局变量 |
| RuntimeError | 解释器内部错误 |

### 总结

希望这段短的回顾提供了 Python 优势的示例，以及为什么它是当今最流行的脚本语言之一。凭借 Python 的内置功能和海量的标准库，可以轻松构建简单的程序来实现惊人的功能，且其代码量比其他高级语言小几个数量级。Python 是已经拥挤的领域中的另一种面向对象的脚本语言，但非常值得你花时间去学习和使用。

### 资源

- Python 编程语言——官方网站：http://www.python.org/
- 维上的 Python 编程语言：http://en.wikipedia.org/wiki/Python_(language)。
- Python 在线文档：http://docs.python.org/

### 引言

本章从开发者的角度探索了系统管理。这意味着诸如基本配置、用户管理等主题未被涵盖。相反，本章探讨了如何导航文件系统、包管理和其他主题。

### 导航 LINUX 文件系统

在许多 UNIX 和 Linux 发行版中，它们很容易发生分支，从而导致不兼容。文件系统（其结构和存储内容的位置）是可能导致不兼容的主要区域之一。幸运的是，文件系统层次结构标准（FHS）的创建是为了解决这个问题（不仅是为了大量的 Linux 发行版，也是为了类 UNIX 操作系统）。FHS 定义了根（`/`）文件系统中会出现哪些子目录，以及它们的内容应该是什么的（参见表 28.1）。

### 表 28.1 FHS 标准子目录

| 目录 | 目的 |
|---|---|
| `/` | 主根目录（用于整个文件系统） |
| `/bin` | 单用户模式下使用的主要命令 |
| `/sbin` | 系统二进制文件 |
| `/dev` | 设备文件（用户空间到内核的链接） |
| `/etc` | 系统级配置文件 |
| `/home` | 本地用户的家目录 |
| `/lib` | `/bin` 和 `/sbin` 中二进制文件所需的库 |
| `/mnt` | 挂载文件系统的目录 |
| `/opt` | 可选软件软件包的目录 |
| `/proc` | 虚拟文件系统（内核状态和用户空间进程状态） |
| `/tmp` | 临时文件目录 |
| `/usr` | 用户相关层次结构 (`/usr/bin`, `/usr/sbin`, `/usr/include` 等） |
| `/var` | 可变文件（如邮件和打印队列、日志等） |

FHS 深入了更多细节，但这个初级介绍为根文件系统的内容提供了一些视角。标准对文件位置深入探讨了大量细节，包括其原理，因此值得阅读。

### 包管理

包管理是维护软件软件包（安装、升级或卸载）的过程。软件软件包通常在单个文件中分发（为了简单起见），但可能会导致在系统的许多地方安装许多文件。软件包不仅包含软件本身（源码或二进制形式），还包含如何以及何处安装软件包的自动化指令。

本节探索了一些包管理的可能性，从最基础的开始。

### TARBALL 分发

分发软件包最常见且平台无关的方法是通过压缩 tarball（压缩包）。tarball 是一种使用 `tar` 命令创建和处理的文件格式。tarball 通常需要多花一点精力，因为它非常常见，因此理解它是很有用的。

`tar` 命令的名字源于它最初作为磁带备份的格式。该名字本身源于“tape archive”（磁带存档），但在 POSIX 标准下被标准化。`tar` 工具保留了它从旧磁带时代的遗产。例如，访问（如磁带）是顺序的。使用 `tar`，如果要提取最后一个文件，则需要扫描整个存档（就像在磁带的情况下一样）。

> 许多软件包以 tarball 形式分发，是因为 tarball 被普遍理解并且压缩到便于存储的大小。使用 tarball 分发软件通常意味着一组其他工具（如 automate, autoconf, configure 等），这些在第 8 章“使用 autoconf 构建软件包”中介绍。

Tarball 通常遵循标准的命名约定，因此很容易知道文件是如何构造的。标准二进制文件命名为 `.tar`，表示未压缩的 tarball。如果 tarball 经过压缩，则命名为 `.tar.gz`（gzip 压缩）和 `.tar.bz2`（bzip2 压缩）。正如你在本章后面看到的，可以通过命令自动压缩或解压 tarball。

> 下载 tarball 后，处理它的常用地方是 `/usr/local/src`。回想该位置存储特定于主机的本地数据。如果在安装软件软件包后删除 tarball，那么更好的地方是 `/tmp`。这个位置是理想的，因为它会定期和自动清理。但有时最好保留源码，因此在示例中，使用了前面的目录。接下来（参见列表 28.1），下载了要安装的特定 tarball（在本示例中，使用了最新版本的 Ruby 用于演示）。

对于压缩的 Ruby tarball，你对 tarball 调用了 `tar` 并带了三个选项。第一个选项 `x` 表示你正在提取存档（而不是使用 `c` 创建一个）。接下来，你指定命令行上紧跟一个文件名（而不是使用 STDIN）。最后，你指定 `z` 表示这是一个 gzip 压缩的存档，并自动解压 tarball。结果是一个新目录（在这种情况下为 `ruby-1.8.6-p111`），它包含了 Ruby 面向对象脚本语言的源码。

### 544 GNU/Linux 应用程序编程

#### 列表 28.1 将 Tarball包下载到工作目录

```
root@camus:-# cd /usr/local/src

root@camus:-# /usr/local/src# wget http://xyz.lcs.mit.edu/ruby/

ruby-1.8.6-p111.tar.gz

-18:35:21:- -- http://xyz.lcs.mit.edu/ruby/ruby-1.8.6-p111.tar.gz

       => ruby-1.8.6-p111.tar.gz

...

Length: 4,547,579 (4.3M) [application/x-tar]

18:35:41 (260 KB/s) - 'ruby-1.8.6-p111.tar.gz' saved

[4547579/4547579]
```

```
root@camus:/usr/local/src# tar xzf ruby-1.8.6-p111.tar.gz

root@camus:/usr/local/src#
```

下一步是将源码构建到你的包中，因此你需要进入包子目录。如果该子目录包含一个 `Makefile`（它是 `make` way的规范文件），你通常只需要运行 `make` 来构建源码。如果不存在 `Makefile`，则你需要通过配置过程。该过程会自动创建构建源码所需的 `Makefile`。这个过程是必要的，因为系统在许多方面可能存在差异。例如，工具可能存储在不同的地方。你运行的 shell 可能与预期的不同。编译器可能不支持该包的先决条件，或者不存在先决包（需要下载额外的模块）。`configure` 过程会自动检查你的系统并相应地构建 `Makefile`。

接后的过程非常简单（见列表 28.2）。首先，运行工作目录（刚安装源码的目录）中的 `configure` 脚本。接下来，输入 `make` 来构建源码。`configure` 脚本还可以用于提供配置指令——例如安装、带有启用选项的安装等。你通常可以通过输入 `./configure --help` 来查看可用选项列表。

#### 列表 28.2 configure 和 make 过程

```
root@camus:/usr/local/src/ruby-1.8.6-p111# ./configure

checking build system type... i686-pc-linux-gnu

checking host system type... i686-pc-linux-gnu

checking target system type... i686-pc-linux-gnu

checking for gcc... gcc
```
