
| `^` | Start of a line | References the beginning of a line |
| `$` | End of a line | References the end of a line |
| `.` | Any character | Matches on any one possible character in a pattern |
| `*` | Repeated characters | Matches on repeated characters in a pattern |
| `[]` | Classes | Matches on classes of characters (a set of characters) in the pattern |

注意 正则表达式在许多 Linux 过滤器和应用程序中被广泛用于执行搜索和匹配操作。`Vi` 和 `Emacs` 编辑器以及 `sed`、`diff`、`fgrep`、`gzip`

假设你想使用 `ls` 的长格式输出仅显示你的目录。一种方法是生成所有目录的长格式列表并将其通过管道传输到 `grep`，然后 `grep` 可以挑选出目录条目。你可以通过使用 `^` 特殊字符来指定行的开头来实现这一点。请记住，在 `ls` 的长格式输出中，第一个字符表示文件类型。`d` 表示目录，`l` 表示符号链接，`-` 表示普通文件。使用模式 `'^d'`，`grep` 只会匹配以 `d` 开头的行。

```
$ ls -l | grep '^d'
drwxr-x---  2 chris 512 Feb 10 04:30  reports
drwxr-x---  2 chris 512 Jan 6  01:20  letters
```

### 第 9 章：Shell 配置

#### 概述

在 Linux 系统上通常使用四种主要 shell：Bourne Again shell（`BASH`）、Public Domain Korn shell（`PDKSH`）、`TCSH` shell 和 `Z` shell。`BASH` shell 是 Bourne shell 的高级版本，其中包含了为 Korn shell 和 C shell 开发的大多数高级功能。`TCSH` 是 C shell 的增强版本，最初为 BSD 版本的 Unix 开发。`PDKSH` 是 Unix Korn shell 的子集，而 `Z` shell 则是 Korn shell 的增强版本。尽管它们的 Unix 对应版本差异很大，但 Linux shell 共享许多相同的功能。在 Unix 中，Bourne shell 缺少其他 Unix shell 中找到的许多功能。在 Linux 中，`BASH` shell 包含了 Korn shell 和 C shell 以及 `TCSH` shell 的所有高级功能。四种 shell 都可供您使用，其中 `BASH` shell 为默认。

到目前为止，本书中的所有示例都使用了 `BASH` shell。您登录到默认 shell，但可以通过输入其名称切换到另一个 shell。`tcsh` 调用 `TCSH` shell，`bash` 调用 `BASH` shell，`ksh` 调用 `PDKSH` shell，`zsh` 调用 `Z` shell。您可以使用 `CTRL-D` 或 `exit` 命令离开 shell。您只需要一种类型的 shell 来完成工作。本章描述了 `BASH` shell 的常见功能，例如别名，以及如何使用 shell 变量和初始化文件将 shell 配置为您自己的需求。其他 shell 共享许多相同的功能并使用类似的变量和初始化文件。

#### 别名

您使用 `别名` 命令为命令创建另一个名称。`别名` 命令像宏一样操作，扩展为它所代表的命令。别名不会从字面上替换命令的名称；它只是为该命令提供另一个名称。`别名` 命令以关键字 `别名` 和命令的新名称开头，后跟等号和别名将引用的命令。

注意 在 `别名` 命令中使用的等号周围不能有空格。

在下一个示例中，`list` 成为 `ls` 命令的另一个名称：

```
$ alias list=ls
$ ls
mydata today
$ list
mydata today
$
```

#### 别名命令和选项

您也可以使用别名来代替命令及其选项，但需要将命令和选项都用单引号括起来。任何包含空格的别名命令都必须用单引号括起来。在下一个示例中，别名 `lss` 引用带有 `-s` 选项的 `ls` 命令，别名 `lsa` 引用带有 `-F` 选项的 `ls` 命令。带有 `-s` 选项的 `ls` 列出文件及其按块计算的大小，而带有 `-F` 选项的 `ls` 在目录名称后放置斜杠。注意单引号如何将命令及其选项括起来。

```
$ alias lss='ls -s'
$ lss
mydata 14 today 6 reports 1
$ alias lsa='ls -F'
$ lsa
mydata today reports/
$
```

别名有助于简化复杂操作。在下一个示例中，`listlong` 成为 `ls` 命令的另一个名称，其中 `-l` 选项用于长格式列出所有文件信息，以及 `-h` 选项用于以人类可读格式显示文件大小。务必将命令及其参数用单引号括起来，以便它们被视为一个参数而不是由 shell 解析。

```
$ alias listlong='ls -lh'
$ listlong
-rw-r--r-- 1 root root 51K Sep 18 2003 mydata
-rw-r--r-- 1 root root 16K Sep 27 2003 today
```

#### 别名命令和参数

您经常可以使用别名来包含带参数的命令名称。如果您定期执行带有复杂特殊字符组合的参数的命令，您可能希望为其创建别名。例如，假设您经常只列出源代码和目标代码文件——那些以 `.c` 或 `.o` 结尾的文件。您需要为 `ls` 使用参数，例如特殊字符组合 `*.[co]`。相反，您可以将 `ls` 与 `.[co]` 参数一起别名，给它一个简单的名称。在下一个示例中，用户为命令 `ls *.[co]` 创建了一个名为 `lsc` 的别名：

```
$ alias lsc='ls *.[co]'
$ lsc
main.c main.o lib.c lib.o
```

#### 别名命令

您也可以使用命令的名称作为别名。这在您应该仅使用特定选项使用命令的情况下很有帮助。对于 `rm`、`cp` 和 `mv` 命令，`-i` 选项应始终使用以确保不会覆盖现有文件。与其每次使用这些命令时都小心使用 `-i` 选项，命令名称可以别名以包含该选项。在下一个示例中，`rm`、`cp` 和 `mv` 命令已被别名以包含 `-i` 选项：

```
$ alias rm='rm -i'
$ alias mv='mv -i'
$ alias cp='cp -i'
```

`alias` 命令提供已定义的所有别名的列表，显示它们所代表的命令。您可以使用 `unalias` 命令删除别名。在下一个示例中，用户列出当前别名然后删除 `lsa` 别名：

```
$ alias
lsa=ls -F
list=ls
rm=rm -i
$ unalias lsa
```

#### 控制 Shell 操作

`BASH` shell 有几个功能使您能够控制不同 shell 操作的工作方式。例如，设置 `noclobber` 功能可防止重定向覆盖文件。您可以使用 `set` 命令像切换一样打开和关闭这些功能。`set` 命令接受两个参数：指定打开或关闭的选项和功能名称。要打开功能，您使用 `-o` 选项，要关闭它，您使用 `+o` 选项。基本形式如下：

```
$ set -o feature      turn the feature on
$ set +o feature      turn the feature off
```

三个最常见的功能是 `ignoreeof`、`noclobber` 和 `noglob`。表 9-1 列出了这些不同的功能以及 `set` 命令。设置 `ignoreeof` 启用一项功能，可防止您使用 `CTRL-D` 从用户 shell 注销。`CTRL-D` 不仅用于从用户 shell 注销，还用于结束直接输入到标准输入的用户输入。`CTRL-D` 常用于 `Mail` 程序或 `cat` 等实用程序。在这种情况下，您很容易输入额外的 `CTRL-D` 并意外注销自己。`ignoreeof` 功能可防止此类意外注销。在下一个示例中，使用 `set` 命令和 `-o` 选项打开 `ignoreeof` 功能。现在用户只能通过输入 `logout` 命令注销。

```
$ set -o ignoreeof
$ ctrl-d
Use exit to logout
$
```

表 9-1：`BASH` Shell 特殊变量和功能

| `BASH` Shell 特殊变量 | 描述 |
|---|---|
| `HOME` | 用户主目录的路径名 |
| `LOGNAME` | 登录名 |
| `USER` | 用户名 |
| `SHELL` | 您所使用 shell 类型的程序路径名 |
