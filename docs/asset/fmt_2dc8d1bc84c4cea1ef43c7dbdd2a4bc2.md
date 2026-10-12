
## Syntax:

```
gcc [options] file-list
```

**用途**：此 `gcc` 命令可用于调用 C 编译系统。在执行时，它会进行处理、编译、汇编和链接，以生成可执行文件。可执行代码默认放在 `a.out` 文件中。该命令接受多种类型的文件，并根据命令行中指定的选项进行处理。文件可以是归档文件（`.a` 扩展名）、C++ 源文件（`.c`, `.cc` 或 `.cpp`）、汇编文件（`.s` 扩展名）、预处理文件（`.i` 扩展名）或对象文件（`.o` 扩展名）。当文件扩展无法识别时，命令假设该文件为对象文件或库/归档文件。文件由 `file-list` 指定。

**常用选项/功能**：

- `-ansi` 强制完全符合 ANSI 标准
- `-c` 抑制链接阶段并保留对象文件（`.o` 扩展名）
- `-g` 创建符号表、性能分析和调试信息，以供 `gdb`（GNU 调试器）使用
- `-lm` 链接 `libm` 库
- `-mconfig` 为指定的 CPU 优化代码，可以指定多种 CPU，包括 Intel 80386、80486、Motorola 68k 系列、RS6000、AMD 29K 系列和 MIPS 处理器
- `-o` 在文件中创建可执行文件，而不是默认的文件 `out`
- `-level` 优化。你可以指定 0-3 为级别；通常数字越大，优化级别越高。如果级别为 0 则不进行优化
- `-pg` 提供性能分析信息，供性能分析工具 `profg` 使用
- `-S` 不汇编 `.c` 文件或链接 `.c` 文件，并将汇编版本留存在对应的 `.s` 扩展名文件中
- `-v` 详细模式：显示正在被调用的命令
- `-w` 抑制警告

```
$ cat first.c

#include <stdio.h>

int main ()

{

    printf("Linux Rules the Networking World!\n");

    return (0);

}
```

如果你的搜索路径不包含当前目录（`.`），你将收到类似 `a.out: Command not found` 的消息，如下面的会话所示。如果发生这种情况，你有两个选择：你可以运行 `./a.out`（即显式告诉 shell 应该运行当前目录下的 `a.out` 文件），或者将当前目录包含在 shell 的搜索路径中，并重新运行命令 `a.out`。下面的会话演示了这两个选项。

```
$ a.out

a.out: Command not found.

$ ./a.out

Linux Rules the Networking World!

$ PATH=$PATH:.

$ a.out

Linux Rules the Networking World!

$
```

注意，搜索路径的更改仅对当前会话有效。若要对搜索路径进行永久更改，你需要修改 `~/.profile` 文件中 `PATH` 变量的值。详情请见第 2 章。

## 14.5.3.2 处理多个源文件

你可以使用 `gcc` 命令在单行命令行中编译并链接 C 源文件并创建可执行文件。例如，你可以使用以下命令行为 C 源文件 `driver.c`、`stack.c` 和 `misc.c` 创建名为 `polish` 的可执行文件。

```
$ gcc driver.c stack.c misc.c -o polish

$
```

如果三个文件中的其中一个被修改了，你需要重新输入命令行，这会产生两个问题：首先，所有三个文件都被编译成各自的对象模块，尽管只有其中一个需要重新编译。这会导致时间变长，特别是当文件很大时。其次，重新输入整行可能意味着当有更多文件时也要这样做。为了避免这些问题，你应该为所有源文件创建对象模块，然后只提取那些更新的模块。所有对象模块将被链接生成单个可执行文件。

你可以使用带有 `-c` 选项的 `gcc` 命令为 C 源文件创建对象模块。使用 `-c` 选项编译程序时，编译器会在当前目录下留一个对象文件。该对象文件的名称与源文件名相同并带有 `.o` 扩展名。你可以通过另一个 `gcc` 命令链接多个对象文件。在下面的会话中，我们分别编译三个源模块——`driver.c`、`stack.c` 和 `misc.c` 以创建它们的对象文件，然后使用另一个 `gcc` 命令链接并创建一个单一的可执行文件 `polish`。

```
$ gcc -c driver.c

$ gcc -c stack.c

$ gcc -c misc.c

$ gcc misc.o stack.o driver.o -o polish

$ polish
```

你也可以用 `-c` 选项一次编译多个文件。在以下命令的第一条中，我们用一个命令编译所有源文件以生成对象文件。文件在命令行中列出的顺序并不重要。第二条命令链接对象文件并生成一个可执行文件 `polish`。

```
$ gcc -c driver.c stack.c misc.c

$ gcc misc.o stack.o driver.o -o polish
```

现在，如果你更新了源文件之一，你需要使用 `-c` 命令仅为该源文件生成对象文件。然后使用第二个命令再次链接所有对象文件生成可执行文件。

## 14.5.3.3 链接库

Linux 上的 C 编译器会在编译程序时将适当库与你的程序链接。有时，你必须显式告诉编译器链接所需的库。你可以通过使用 `-l` 选项的 `gcc` 命令并在后紧跟库名来实现。你使用的大多数库为每个需要链接的库使用一个独立的 `-l` 选项。在 `/lib` 目录下，有数学库。

# 用于软件开发的 Linux 工具

通过使用 `perl`、`python` 和 `ruby` 命令来完成。如果不确定，可以使用 `which` 命令来查找解释器在文件系统中的位置，如下所示所示。

```
$ which perl

/usr/bin/perl

$ which python

/usr/bin/python

$ which ruby

/usr/bin/ruby

$
```

Linux Mint 默认未安装 Ruby。你可以请求你的系统管理员为你安装。你也可以按照附录 A 中提供的说明在你的 Linux 机器上自行安装。

Perl、Python 和 Ruby 脚本文件的扩展名分别为 `.pl`、`.py` 和 `.rb`。和 Linux 中所有的脚本一样，第一行指定了解释器的路径，随后是脚本内容。Perl、Python 和 Ruby 脚本的执行方式与 shell 脚本的执行相同：创建脚本文件，赋予该文件可执行权限，然后使用相关文件的文件名或将脚本文件作为相关解释器命令（`perl`、`python` 或 `ruby`）的参数来运行脚本。以下会显示了“Hello, World!” Perl 脚本的样子以及如何执行它。

```
$ cat Hello.pl

#!/usr/bin/perl

# The Hello World program in Perl

print "Hello, World!\n"

$ chmod +x Hello.py

$ Hello.py

Hello, World!

$ perl Hello.py

Hello, World!

$
```

以下会显示了“Hello, World!” Python 脚本的样子以及如何执行它。

```
$ cat Hello.py

#!/usr/bin/python

# The Hello World program in Python

print "Hello, World!"

$ chmod +x Hello.py

$ Hello.py

Hello, World!

$ python Hello.py

Hello, World!

$
```

最后，以下会显示了“Hello, World!” Ruby 脚本的样子以及如何执行它。

```
$ cat Hello.rb

#!/usr/bin/ruby

# The Hello World program in Ruby

puts "Hello, World!"

$ chmod +x Hello.rb

$ Hello.rb

Hello, World!

$ ruby Hello.rb

Hello, World!

$
```

你也可以从命令行运行 Perl 和 Python，如下节所示。

```
$ perl -e 'print "Hello, World!\n'

Hello, World!

$ python -c 'print "Hello, World!\n'

Hello, World!

$ ruby -e 'puts "Hello, World!\n'

Hello, World!

$
```
