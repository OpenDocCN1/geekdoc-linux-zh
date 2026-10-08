
| 字符 | 匹配 | 操作 |
| :--- | :--- | :--- |
| ^ | 行首 | 引用行的开头。 |
| $ | 行尾 | 引用行的末尾。 |
| . | 任意字符 | 匹配模式中的任意单个字符。 |
| * | 重复字符 | 匹配模式中的重复字符。 |
| [] | 字符类 | 匹配模式中的字符类（一组字符）。 |

**表 8-10** 正则表达式特殊字符

正则表达式的特殊字符包括脱字符（circumflex）、美元符号、星号、句点和方括号：`^`、`$`、`*`、`.`、`[]`。脱字符和美元符号分别匹配行的开头和结尾。星号匹配重复的字符，句点匹配单个字符，而方括号匹配字符类。请参阅表 8-10 了解正则表达式特殊字符的列表。

> **注意** 许多 Linux 过滤器和应用程序广泛使用正则表达式来执行搜索和匹配操作。Vi 和 Emacs 编辑器以及 sed、diff、grep 和 gawk 过滤器都使用正则表达式。

假设你想使用 `ls` 的长格式输出来仅显示你的目录。一种方法是生成长格式的所有目录列表，并将该列表通过管道传递给 `grep`，然后由它挑选出目录条目。你可以通过使用 `^` 特殊字符来指定行的开头来实现这一点。请记住，在 `ls` 的长格式输出中，第一个字符指示文件类型。`d` 表示目录，`l` 表示符号链接，而 `a` 表示普通文件。使用模式 `'^d'` 时，`grep` 将仅匹配以 `d` 开头的行。

```bash
$ ls -l | grep '^d'
drwxr-x--- 2 chris 512 Feb 10 04:30 reports
drwxr-x--- 2 chris 512 Jan 6 01:20 letters
```

## 第 9 章
## Shell 配置

我们在 Linux 系统上常用的主要 shell 包括：Bourne Again shell (BASH)、AT&T Korn shell、TCSH shell 和 Z shell。BASH shell 是 Bourne shell 的高级版本，它包含了为 Korn shell 和 C shell 开发的大多数高级功能。TCSH 是 C shell 的增强版本，最初是为 Unix 的 BSD 版本开发的。包含在 Fedora 中的 AT&T Unix Korn shell 是开源的。Z shell 是 Korn shell 的增强版本。PDKSH shell（公共领域 Korn Shell），作为 Unix Korn shell 的子集，不再随 Fedora Linux 提供。尽管它们的 Unix 对应物差异很大，但 Linux shell 共享许多相同的功能。在 Unix 中，Bourne shell 缺乏其他 Unix shell 中的许多功能。然而，在 Linux 中，BASH shell 整合了 Korn shell、C shell 以及 TCSH shell 的所有高级功能。所有这四种 shell 都可供你使用，尽管 BASH shell 是默认选项。

到目前为止，本书中的所有示例都使用了 BASH shell，它是 Red Hat 和 Fedora 的默认 shell。如果你登录到命令行界面，系统将自动将你置于默认 shell 中，并给出一个 shell 提示符供你输入命令。BASH shell 的提示符是美元符号 ($)。在 GNOME 或 KDE 等图形用户界面中，你可以打开一个终端窗口，该窗口将显示带有默认 shell (BASH) 提示符的命令行界面。虽然你登录到默认 shell 或在终端窗口中自动显示它，但你可以通过输入其名称来切换到其他 shell。`tcsh` 调用 TCSH shell，`bash` 调用 BASH shell，`ksh` 调用 Korn shell，`zsh` 调用 Z shell。你可以使用 `Ctrl-D` 或 `exit` 命令退出 shell。你只需要一种类型的 shell 即可完成工作。表 9-1 显示了用于调用不同 shell 的不同命令。一些 shell 添加了链接，你可以使用这些链接来调用相同的 shell，例如 `sh` 和 `bsh`，它们链接到并调用 BASH shell 的 bash 命令。

本章描述了 BASH shell 的常见功能，例如别名，以及如何使用 shell 变量和初始化文件来配置 shell 以满足你自己的需求。其他 shell 共享许多相同的功能，并使用类似的变量和初始化文件。

虽然这里展示了基本的 shell 功能和配置，但你应查阅各个 shell 的在线手册和常见问题解答，以获取更详细的示例和说明（参见第 8 章中的表 8-1）。

| 功能 | 描述 |
| --- | --- |
| bash | BASH shell, /bin/bash |
| bsh | BASH shell, /bin/bsh（指向 /bin/bash 的链接） |
| sh | BASH shell, /bin/sh（指向 /bin/bash 的链接） |
| tcsh | TCSH shell, /usr/tcsh |
| csh | TCSH shell, /bin/csh（指向 /bin/tcsh 的链接） |
| ksh | Korn shell, /bin/ksh（另外增加了链接 /usr/bin/ksh） |
| zsh | Z shell, /bin/zsh |

**表 9-1** Shell 调用命令名称

### 别名

你使用 **alias** 命令为命令创建另一个名称。**alias** 命令的作用类似于宏，它会扩展为其所代表的命令。别名并没有字面意义上替换命令的名称；它只是为该命令赋予了另一个名称。**alias** 命令以关键字 **alias** 和命令的新名称开头，后跟等号以及别名将引用的命令。

**注意** *alias* 命令中使用的等号周围不能有空格。

在下一个示例中，**list** 成为 **ls** 命令的另一个名称：

```bash
$ alias list=ls
$ ls
mydata today
$ list
mydata today
$ 
```

### 别名命令和选项

你也可以使用别名来替代命令及其选项，但你必须将命令和选项都用单引号括起来。任何包含空格的别名命令都必须用单引号括起来。在下一个示例中，别名 **lss** 引用带有 **-s** 选项的 **ls** 命令，而别名 **lsa** 引用带有 **-F** 选项的 **ls** 命令。带有 **-s** 选项的 **ls** 命令列出文件及其块大小，而带有 **-F** 选项的 **ls** 会在目录名称后放置一个斜杠。请注意单引号如何括起命令及其选项。

```bash
$ alias lss='ls -s'
$ lss
mydata 14 today 6 reports 1
$ alias lsa='ls -F'
$ lsa
mydata today reports/
$ 
```

别名有助于简化复杂操作。在下一个示例中，`listlong` 成为带有 `-l` 选项（长格式，列出所有文件信息）以及 `-h` 选项（用于以人类可读格式显示文件大小）的 `ls` 命令的另一个名称。务必将命令及其参数都用单引号括起来，以便它们被视为一个参数，而不是被 shell 解析。

```bash
$ alias listlong='ls -lh'
$ listlong
-rw-r--r--    1 root    root    51K Sep  18  2003 mydata
-rw-r--r--    1 root    root    16K Sep  27  2003 today
```

### 别名命令和参数

你可能经常使用别名将命令名称与参数结合在一起。如果你经常执行带有复杂特殊字符组合参数的命令，你可能希望将其别名化。例如，假设你经常仅列出你的源代码和对象代码文件——那些以 `.c` 或 `.o` 结尾的文件。你需要为 `ls` 使用一组特殊字符作为参数，例如 `*.[co]`。相反，你可以将 `ls` 别名化并附带 `.[co]` 参数，赋予它一个简单的名称。在下一个示例中，用户为命令 `ls *.[co]` 创建了一个名为 `lsc` 的别名：

```bash
$ alias lsc='ls *.[co]'
$ lsc
main.c main.o lib.c lib.o
```

### 别名命令

你也可以将命令的名称用作别名。在某些情况下，这很有帮助，例如当你应该仅使用特定选项时使用命令。对于 `rm`、`cp` 和 `mv` 命令，应始终使用 `-i` 选项，以确保不会覆盖现有文件。与其每次都小心地使用这些命令中的 `-i` 选项，不如将命令名称别名化以包含该选项。在下一个示例中，`rm`、`cp` 和 `mv` 命令已被别名化以包含 `-i` 选项：

```bash
$ alias rm='rm -i'
$ alias mv='mv -i'
$ alias cp='cp -i'
```

单独使用 `alias` 命令会提供已定义的所有别名列表，并显示它们代表的命令。你可以使用 `unalias` 命令删除别名。在下一个示例中，用户列出了当前别名，然后删除了 `lsa` 别名：

```bash
$ alias
lsa=ls -F
list=ls
rm=rm -i
$ unalias lsa
```
