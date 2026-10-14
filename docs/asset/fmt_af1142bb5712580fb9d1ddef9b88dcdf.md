
> 注：由于我们在编译时是该源代码的“维护者”，我们会将其保存在 `~/src` 中。由发行版安装的源代码会安装在 `/usr/src` 中，而供多用户使用的源代码通常安装在 `/usr/local/src`。

正如我们所见，源代码通常以压缩的 `tar` 文件形式提供。有时称为“tarball”，该文件包含源代码树，即构成源代码的目录和文件的层级结构。到达 `ftp` 站点后，我们会查看可用的 `tar` 文件列表并选择最新版本进行下载。使用 `ftp` 中的 `get` 命令，我们将文件从 `ftp` 服务器复制到本地机器。

下载 `tar` 文件后，必须将其解包。这是通过 `tar` 程序完成的：

```
[me@linuxbox src]$ tar xzf diction-1.11.tar.gz

[me@linuxbox src]$ ls

diction-1.11        diction-1.11.tar.gz
```

提示：`diction` 程序像所有 GNU 项目软件一样，遵循一定的源代码打包标准。Linux 生态系统中大多数其他源代码也遵循此标准。标准的一个要素是，通过解包源代码 `tar` 文件，会创建一个包含源代码树的目录，并且该目录将命名为 `project-x.xx`，从而同时包含项目名称和版本号。这种方案允许轻松安装同一程序的多个版本。然而，在解包之前检查树的布局通常是个好主意。某些项目不会创建目录，而是直接将文件交付到当前目录。这会在你原本井然有序的 `src` 目录中造成混乱。为避免这种情况，使用以下命令检查 `tar` 文件的内容：

```
tar tzvf tarfile | head
```

## 检查源代码树

解包 `tar` 文件会创建一个名为 `diction-1.11` 的新目录。该目录包含源代码树。让我们看一下内部：

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

其中，我们看到许多文件。GNU 项目的程序以及许多其他程序都会提供文档文件 `README`、`INSTALL`、`NEWS` 和 `COPYING`。这些文件包含程序的描述、如何构建和安装它的信息以及许可条款。在尝试构建程序之前，仔细阅读 `README` 和 `INSTALL` 文件始终是个好主意。

该目录中其他有趣的文件是以 `.c` 和 `.h` 结尾的文件：

```
[me@linuxbox diction-1.11]$ ls *.c

diction.c getopt.c getopt1.c misc.c sentence.c style.c

[me@linuxbox diction-1.11]$ ls *.h

getopt.h getopt_int.h misc.h sentence.h
```

`.c` 文件包含该包提供的两个 C 程序（`style` 和 `diction`），分为多个模块。对于大型程序，将其拆分为更小、更易管理的部分是常见做法。源代码文件是普通文本，可以使用 `less` 进行检查：

```
[me@linuxbox diction-1.11]$ less diction.c
```

`.h` 文件称为头文件。这些也是普通文本。头文件包含源代码文件或库中包含的例程的描述。为了使编译器连接模块，它必须接收完成整个程序所需的所有模块的描述。在 `diction.c` 文件的开头附近，我们看到这一行：

```
#include "getopt.h"
```

这指示编译器在读取 `diction.c` 中的源代码时同时读取 `getopt.h` 文件，以便“知道”`getopt.c` 中的内容。`getopt.c` 文件提供了 `style` 和 `diction` 两个程序共享的例程。

在 `getopt.h` 的 include 语句之上，我们看到其他一些 include 语句，例如：

```
#include <regex.h>
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>
```

这些也引用头文件，但它们引用的是位于当前源树之外的头文件。它们由系统提供，以支持每个程序的编译。如果我们查看 `/usr/include`，可以看到它们：

```
[me@linuxbox diction-1.11]$ ls /usr/include
```

此目录中的头文件是在我们安装编译器时安装的。

## Building The Program

大多数程序都使用简单的两条命令序列进行构建：

```
./configure
make
```

`configure` 程序是随源树提供的 shell 脚本。它的任务是分析构建环境。大多数源代码旨在可移植。即，它旨在构建在不止一种类 Unix 系统上。但为了做到这一点，源代码在构建期间可能需要进行细微调整以适应系统之间的差异。`configure` 还会检查必要的外部工具和组件是否已安装。让我们运行 `configure`。由于 `configure` 不位于 shell 通常期望程序所在的位置，我们必须通过在命令前加上 `./` 来明确告诉 shell 其位置，以指示程序位于当前工作目录中：

```
[me@linuxbox diction-1.11]$ ./configure
```

`configure` 在测试和配置构建时将输出大量消息。完成后，它看起来会像这样：

```
checking libintl.h presence... yes
checking for libintl.h... yes
checking for library containing gettext... none required
configure: creating ./config.status
config.status: creating Makefile
config.status: creating diction.1
config.status: creating diction.texi
config.status: creating diction.spec
config.status: creating style.1
config.status: creating test/rundiction
config.status: creating config.h
[me@linuxbox diction-1.11]$
```

这里重要的是没有错误消息。如果有，配置就会失败，并且在纠正错误之前程序将无法构建。

我们看到 `configure` 在源目录中创建了几个新文件。其中最重要的是 `Makefile`。`Makefile` 是一个配置文件，它指示 `make` 程序如何精确地构建程序。没有它，`make` 将拒绝运行。`Makefile` 是一个普通文本文件，因此我们可以查看它：

```
[me@linuxbox diction-1.11]$ less Makefile
```

`make` 程序以 `makefile` 为输入，通常命名为 `Makefile`，它描述了构成最终程序的各个组件之间的关系和依赖关系。

`makefile` 的第一部分定义了在 `makefile` 后续部分中被替换的变量。例如我们看到这一行：

```
CC=           gcc
```

它定义 C 编译器为 `gcc`。稍后在 `makefile` 中，我们看到它被使用的一个实例：

```
diction:       diction.o sentence.o misc.o getopt.o getopt1.o
              $(CC) -o $@ $(LDFLAGS) diction.o sentence.o misc.o \
              getopt.o getopt1.o $(LIBS)
```
