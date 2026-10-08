

# make 程序 325

由程序员指定的目录树，并设置了相应的访问权限。

列表 11.2 显示了一个稍微复杂的 Makefile，它同时使用了变量和默认规则进行编译，而不是直接调用 gcc。

这个 Makefile 与常用的 Makefiles 具有某种相似之处。在第一部分，设置了一些变量，这些变量稍后可以在规则或依赖项中使用。通过变量 `CFLAGS`，设置了 C 编译器的选项。在这里，该选项是优化选项 `-2`。变量 `LDFLAGS` 包含了链接器的选项；这里使用了 `-s` 选项。

在这个 Makefile 中，`prune` 程序通过两个步骤创建：首先，将源代码翻译成所谓的对象格式（文件名 `prune.o`）。随后，将该对象文件与标准 C 库链接，以创建一个可执行程序。这两者都是默认规则；可以通过 `make -p` 命令显示所有默认规则的定义。

```
CFLAGS=-2
LDFLAGS=-s
INSTALLDIR=/usr/local/sbin

all: prune

install: prune
    install -m 755 prune $(INSTALLDIR)/prune
echo "edit /etc/prune.conf to suit your system"

prune: prune.o
clean:
    rm -f prune.o
```

列表 11.2 一个稍微复杂的 Makefile。

在 `install` 目标中，程序被复制到目录 `INSTALLDIR` 中。一个新成员是目标 `clean`，它会删除之前生成的程序或对象文件。下一次 `make` 调用必须完全重新编译程序，这是很有意义，例如在配置发生变化的情况下。另一个经常使用的目标是 `dist`，它通常会创建一个包含源代码的 tar 文件。

在较大的程序中，通常需要在编译之前调整单个参数；例如，配置文件或锁文件的名称，或者安装目录。通常，这些变量可以在 Makefile 的开头找到，在那里你也可以找到关于变量含义的注释。

`make` 程序有一系列可以影响 `make` 操作的选项。一个重要且实用的选项是 `-n`，它导致 `make` 显示必要的命令而不是执行 `make`。因此，例如可以使用命令 `make -n install` 代替 `make` 来验证哪些文件将被安装。

`make` 可以同时启动多个程序，因此在内存足够的计算机上，CPU 可以尽可能处于满负荷状态。选项 `-j` 允许多个程序的并行执行。如果该选项后面跟着一个数字，则 `make` 同时启动的程序数量被限制为该数字。如果没有指定，则没有限制。

随着许多进程的启动，“负载”（load），即竞争处理器时间的进程数会增加。使用选项 `-l` 后后跟一个数字，如果其他进程仍在运行且负载大于此值，则会启动新进程。如果没有指定数字，则不考虑负载。因此，如果你启动了 `make` 进程，必须密切关注主内存占用情况和处理器负载，以获得使用的收益。显然，多处理器机器具有显著优势。

```
report.dvi:report.tex figure1.eps figure2.eps
latex report

%.eps:%fig
fig2dev -L ps $< $
```

列表 11.3 用于 LaTeX 的 Makefile

列表 11.3 展示了使用 `make` 生成 DVI 文件 `report.dvi` 的示例。该文件依赖于源文本 `report.tex` 以及插图 `figure1.eps` 和 `figure.eps`。这些插图是用 `xfig` 程序生成的并转换为 eps 格式（封装式 PostScript）。使用 `make` 自动化了插图的转换，并确保最新的插图始终包含在 DVI 文件中。

这个示例还展示了 `make` 的进一步功能。符号 `$` 代表所需的输入文件，符号 `$$` 在运行时被替换为要生成的文件名。这些符号用于描述插图（.fig）与其格式（.eps）之间通用依赖关系的规则中。因此，没有必要为每幅插图指定规则。

这些信息旨在帮助你理解 Makefiles。在开始编写自己的 Makefiles 之前，你应该阅读 GNU make 的手册，该手册是以 Texinfo 格式分发的。它提供了关于使用 `make` 和创建 Makefiles 的详尽文档。如果你经常编辑 Makefiles，可以使用 emacs 编辑器的 `makefile-mode`模式，它提供了一系列实用的函数。

对于 GNU 项目程序，文档 `standards.texinfo` 提供了一份“处方”，以及要采用的 C 编程和风格，同时也概述了 Makefile 最重要的函数。你可能不同意所有的处方，但该文档确实包含一系列实用的提示。

| 附加信息和来源 |
|---|---|
| 文档: | make(1), Texinfo 手册 |
| ftp 服务器: | ftp.gnu.org |
| ftp 路径: | /pub/gnu |
| 文件名: | make-3.72.1.tar.gz |
| 大小: | 约 550 KB |

# 11.2 imake 程序

`imake` 程序是 X Window 系统的一部分，因此经常被用于编译 X 程序。对于任何此类程序，都会创建一个 `Imake`，用于描述要编译的程序和库。基于系统特定的配置文件，从 `Imake` 生成一个 Makefile，然后用于程序的编译。

通常，系统特定的 Makefile 是通过 `xmkmf` 命令生成的。如果程序的源分分布在多个目录中，也可以通过 `xmkmf -a` 命令在子目录中自动生成 Makefiles。为此，`xmkmf` 在内部启动 `make` 生成 Makefiles，随后启动 `make` 生成包含文件并可能依赖项。

`imake` 程序的配置文件可以在 `/usr/X11R6/lib/X11/config` 目录下找到。`linux.cf` 文件包含了 LINUX 的所有必要适配。用户定义的适配可以在 `site.def` 文件中进行，但通常不需要。关于 `imake` 使用和配置的完整介绍，例如可以在 Dubois(1993) 中找到。

# 11.3 程序的安装

UNIX 系统管理员经常面临的一项重复性任务是安装新程序或现有程序的新版本。在 LINUX 下使用的几乎所有程序都是免费的，也就是说源代码是可用的。由于这些软件通常也用于其他 UNIX 系统，因此它们必须在不同平台上具有可移植编译性。因此，程序必须在不同系统之间是可以通的。

# 11.3.1 安装 GNU 程序

自由软件基金会（FSF）的目标是创建一个自由的、类 UNIX 的操作系统（The Hurd）。所有本质的 UNIX 程序都在范围内范围内最不同的 UNIX 版本下被开发和使用。在 Linux 上使用的许多程序都是标准 UNIX 服务程序的 GNU 版本。因此，Linux 被描述为基于 Linux 基础的 GNU 系统。没有了这些程序，Linux 将不会有它今天的模样。

GNU 程序是可移植且功能强大的，因此除了标准的 UNIX 服务程序外，它们还被安装在许多计算机上。可移植性通过在程序编译前分析系统并相应地调整程序来实现。系统分析是由许多 `configure` 脚本启动的。GNU 项目对于创建程序和 Makefile 有一些标准，几乎所有的 GNU 程序都遵循这些标准。你可以在每个 GNU 镜像的 `standards.texi` 文件中找到 GNU 编码标准。

`configure` 脚本分析系统并为程序编译一系列测试。然而，我们首先来看一些 GNU 程序配置的示例。我们从 `gzip` 的配置开始。GNU 对 UNIX compress 的替代品 `gzip` 要好得多，并且其优点是使用时不需要基于现有专利的许可。

```
(Linux):> tar zxf /tmp/gzip-1.2.4.tar.gz
(Linux):> cd gzip-1.2.4
(Linux):> ~/gzip-1.2.4 ./configure
```

列表 11.4 解压和配置 GNU 程序。

脚本显示了一系列消息，允许你跟踪配置过程。较新版本的 GNU 程序分发带有 `configure` 脚本，这些脚本还会显示分析结果。在 `configure` 运行结束，会创建一个 Makefile，可以使用它来编译程序。可以通过 `--verbose` 或 `--quiet` 选项影响显示消息的数量。

