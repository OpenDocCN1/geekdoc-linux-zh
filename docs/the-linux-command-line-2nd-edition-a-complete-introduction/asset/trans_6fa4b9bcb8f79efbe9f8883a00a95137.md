

这个目录中其他有趣的文件是那些以 `.c` 和 `.h` 结尾的文件：

```
```text
[me@linuxbox diction-1.11]$ ls *.c
diction.c  getopt1.c  getopt.c  misc.c  sentence.c  style.c
[me@linuxbox diction-1.11]$ ls *.h
getopt.h  getopt_int.h  misc.h  sentence.h
```
```

`.c` 文件包含该软件包提供的两个 C 程序（`style` 和 `diction`），被拆分为模块。对于大型程序，将其拆分为更小、更易于管理的部分是常见做法。源代码文件是普通文本，可以使用 `less` 查看：

```
```text
[me@linuxbox diction-1.11]$ less diction.c
```
```

`.h` 文件被称为 *头文件*。这些同样是普通文本。头文件包含源代码文件或库中包含的例程的描述。为了使编译器能够连接模块，它必须接收完成整个程序所需的所有模块的描述。在 `diction.c` 文件开头附近，我们看到这一行：

```
```c
#include "getopt.h"
```
```

这指示编译器在读取 `diction.c` 中的源代码时同时读取文件 `getopt.h`，以便“知道” `getopt.c` 中的内容。`getopt.c` 文件提供了 `style` 和 `diction` 两个程序共享的例程。

在 `getopt.h` 的 `include` 语句之上，我们看到其他 `include` 语句，例如：

```
```c
#include <regex.h>
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>
```
```

这些也引用头文件，但它们引用的是位于当前源树之外的头文件。它们由系统提供，以支持每个程序的编译。如果我们查看 `/usr/include`，可以看到它们：

```
[me@linuxbox diction-1.11]$ ls /usr/include
```

该目录中的头文件是在我们安装编译器时安装的。

## 构建程序

大多数程序都使用简单的两条命令序列构建：

```
./configure
make
```

configure 程序是随源树提供的 shell 脚本。它的工作是分析构建环境。大多数源代码旨在可移植。即，它旨在构建在不止一种类 Unix 系统上。但为了做到这一点，源代码在构建过程中可能需要进行轻微调整以适应系统之间的差异。configure 还会检查必要的外部工具和组件是否已安装。让我们运行 configure。由于 configure 不位于 shell 通常期望程序所在的位置，我们必须通过在命令前加上 ./ 来明确告诉 shell 其位置，以指示程序位于当前工作目录中：

```
[me@linuxbox diction-1.11]$ ./configure
```

configure 在测试和配置构建时将输出大量消息。完成后，它看起来会像这样：

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

这里重要的是没有错误消息。如果有，配置就会失败，直到错误被纠正，程序将无法构建。

我们看到 configure 在源目录中创建了几个新文件。最重要的一项是 Makefile。Makefile 是一个配置文件，指示 make 程序如何精确构建程序。没有它，make 将拒绝运行。Makefile 是一个普通文本文件，因此我们可以查看它：

```
[me@linuxbox diction-1.11]$ less Makefile
```

make 程序以 makefile 作为输入（通常命名为 Makefile），该文件描述了构成最终程序的各个组件之间的关系和依赖关系。

makefile 的第一部分定义了在 makefile 后续部分中被替换的变量。例如我们看到这一行：

```
CC=           gcc
```

它定义 C 编译器为 gcc。稍后在 makefile 中，我们看到它被使用的一个实例：

```
diction:       diction.o sentence.o misc.o getopt.o getopt1.o
$(CC) -o $@ $(LDFLAGS) diction.o sentence.o misc.o \
getopt.o getopt1.o $(LIBS)
```

这里执行了替换，值 $(CC) 在运行时被 gcc 替换。

makefile 的大部分由定义目标的行组成，在本例中是可执行文件 diction，以及它所依赖的文件。剩余的行描述了从其组件创建目标所需的命令。我们在这个例子中看到，可执行文件 diction（最终产品之一）依赖于 diction.o、sentence.o、misc.o、getopt.o 和 getopt1.o 的存在。稍后在 makefile 中，我们看到每个的定义作为目标：

```
diction.o:     diction.c config.h getopt.h misc.h sentence.h
getopt.o:      getopt.c getopt.h getopt_int.h
getopt1.o:     getopt1.c getopt.h getopt_int.h
misc.o:        misc.c config.h misc.h
```

