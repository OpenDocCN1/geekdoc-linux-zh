

## 命令到底是什么？

命令可以是以下四种情况之一：

- **可执行程序**，就像我们在 `/usr/bin` 中看到的所有那些文件。在此类别中，程序可以是 *编译后的二进制文件*，例如用 C 和 C++ 编写的程序，或是用 *脚本语言* 编写的程序，例如 shell、Perl、Python、Ruby 等。
- **内置于 shell 本身的命令。** bash 支持一些内部称为 *shell 内置* 的命令。例如，cd 命令就是一个 shell 内置。
- **shell 函数。** *Shell 函数* 是合并到 *环境* 中的微型 shell 脚本。我们将在后面的章节中介绍如何配置环境和编写 shell 函数，但现在只需知道它们存在即可。
- **别名。** *别名* 是我们自己可以定义的命令，由其他命令构成。

## 识别命令

经常需要知道正在使用的是四种命令中的哪一种，而 Linux 提供了几种方法来查找。

## type—显示命令的类型

type 命令是 shell 内置，它会显示 shell 将要执行给定命令名称的种类。其用法如下：

```
type command
```

其中 *command* 是你想要检查的命令的名称。以下是一些示例：

```
[me@linuxbox ~]$ type type
type is a shell builtin
[me@linuxbox ~]$ type ls
ls is aliased to 'ls --color=tty'
[me@linuxbox ~]$ type cp
cp is /bin/cp
```

这里我们看到了三个不同命令的结果。请注意，ls 命令（取自 Fedora 系统）实际上是带有 --color=tty 选项的 ls 命令的别名。现在我们知道为什么 ls 的输出会显示颜色了！

## which—显示可执行文件的所在位置

有时系统中安装了多个版本的某个可执行程序。虽然在桌面系统上这种情况并不常见，但在大型服务器上并不罕见。要确定给定可执行文件的确切位置，可使用 which 命令：

```
[me@linuxbox ~]$ which ls
/bin/ls
```

which 仅适用于可执行程序，不适用于内置命令或作为实际可执行程序替代的别名。当我们尝试对 shell 内置（例如 cd）使用 which 时，我们会得到无响应或错误信息：

```
[me@linuxbox ~]$ which cd
/usr/bin/which: no cd in (/opt/jre1.6.0_03/bin:/usr/lib/qt-3.3/bin:/usr/kerberos/bin:/opt/jre1.6.0_03/bin:/usr/lib/ccache:/usr/local/bin:/usr/bin:/bin:/home/me/bin)
```

这是一种花哨的说法，表示“未找到命令”。

## 获取命令的文档

有了对命令是什么的了解后，我们现在可以为每种类型的命令搜索可用的文档。

## help—获取 shell 内置的帮助

bash 为每个 shell 内置提供了一个内置的帮助功能。要使用它，请键入 help 后跟 shell 内置的名称。例如：

```
[me@linuxbox ~]$ help cd
cd [-L|-P] [dir]
Change the current directory to DIR. The variable $HOME is the default DIR.
The variable CDPATH defines the search path for the directory containing DIR.
Alternative directory names in CDPATH are separated by a colon (:). A null directory name is the same as the current directory, i.e. "..". If DIR begins with a slash (/), then CDPATH is not used. If the directory is not found, and the shell option "cdable_vars" is set, then try the word as a variable name. If that variable has a value, then cd to the value of that variable. The -P option says to use the physical directory structure instead of following symbolic links; the -L option forces symbolic links to be followed.
```

关于表示法的说明：当命令语法描述中出现方括号时，它们表示可选项目。竖线字符表示互斥项目。例如上面的 cd 命令：cd [-L|-P] [dir]。

这种表示法表示 cd 命令可以 optionally 后跟 -L 或 -P 中的一个，并且进一步可选地后跟参数 dir。

虽然 help 对 cd 命令的输出简洁而准确，但它绝不是教程，而且正如我们所见，它似乎也提到了很多我们尚未讨论过的内容！不用担心。我们会慢慢学到的。

## --help—显示使用信息

许多可执行程序支持 --help 选项，可显示命令支持的语法和选项的描述。例如：

```
[me@linuxbox ~]$ mkdir --help
Usage: mkdir [OPTION] DIRECTORY...
Create the DIRECTORY(ies), if they do not already exist.

    -Z, --context=CONTEXT (SELinux) set security context to CONTEXT
Mandatory arguments to long options are mandatory for short options too.
    -m, --mode=MODE      set file mode (as in chmod), not a=rwx - umask
    -p, --parents        no error if existing, make parent directories as needed

    -v, --verbose        print a message for each created directory
        --help           display this help and exit
        --version        output version information and exit
Report bugs to <bug-coreutils@gnu.org>.
```

有些程序不支持 --help 选项，但仍可尝试。通常它会产生错误信息，从而揭示相同的用法信息。

## man—显示程序的手册页

大多数用于命令行使用的可执行程序都提供一份正式的文档，称为手册或 man 页。一种特殊的分页程序 man 用于查看它们，如下所示：

```
man program
```

其中 program 是要查看的命令的名称。

Man 页在格式上略有不同，但通常包含标题、命令语法的概要、命令目的的描述，以及每个命令选项的列表和描述。然而，Man 页通常不包含示例，并且旨在作为参考，而不是教程。作为示例，让我们查看 ls 命令的手册页：

```
[me@linuxbox ~]$ man ls
```

在大多数 Linux 系统上，man 使用 less 来显示手册页，因此在显示页面时所有熟悉的 less 命令都可以使用。

man 显示的“手册”分为多个部分，不仅涵盖用户命令，还涵盖系统管理命令、编程接口、文件格式等。表 5-1 描述了手册的布局。

