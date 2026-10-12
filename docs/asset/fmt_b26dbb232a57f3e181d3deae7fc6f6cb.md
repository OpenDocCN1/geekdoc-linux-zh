
```
COMMAND(1)                Linux Programmer's Manual           COMMAND(1)

NAME
        command - summary of what command does

SYNOPSIS
        <complete syntax of command in the standard Linux form>

DESCRIPTION
        More verbose explanation of what "command" does.

OPTIONS
        Lists each available option with description of what it does

FILES
        lists files used by, or related to, command

SEE ALSO
        command_cousin(1), command_spouse(1), etc.

BUGS
        There are bugs in Linux commands??

AUTHOR
        J. S. Goobly (goobly@hurrdly-gurdly.boondocks)

Linux 1.0         22 June 1994                   1
```

`passwd` 的 man 手册页其实相当容易理解。不过请注意，man 手册页通常以一种非常正式且程式化的方式撰写，有时与常规英语相去甚远。这样做的目的不是为了让人困惑，而是为了在尽可能简短的描述中包含大量的信息。例如，尝试输入 `man ls`。你会发现 `ls` 有多少可用选项，以及解释它们需要多长时间。

虽然理解 man 手册页可能需要练习（以及仔细的阅读！），但一旦你习惯了它们，当你遇到一个不熟悉的命令时，你做的第一件事就会是调用该命令的 man 手册页。

### 在 Man 手册页中查找关键词

有时你知道自己想做什么，但不知道应该使用哪个命令。通过输入 `man -k <keyword>` 使用关键词选项，`man` 程序会返回所有其 `name` 条目（包含非常简短的描述）中包含该关键词的命令名称。

例如，你可以搜索 `manual`：

```
darkstar:~$ man -k manual
darkstar:~$ man 5 passwd
```

不过，你务必小心地指定关键词！例如，使用 `directory` 作为关键词问题不大，但使用 `file` 会返回比你想查看的更多的条目。

> **注意**

你可能注意到，命令后面似乎跟着括号中的数字，通常是 `(1)`。这指的是手册章节。在 UNIX 手册还是印刷装订卷的时候，普通命令在第 1 章，管理员使用的文件在第 5 章，编程例程在第 3 章，等等。因此，有些 man 手册页根本不是关于命令的，而是关于 Linux 中使用的文件或系统调用！如果某个条目出现在多个章节中，`man` 默认会显示编号最低的条目。你可以通过指定章节编号来查看编号较高的条目。例如，第 5 章有一个关于 `passwd` 文件的手册条目。要查看这个而不是 `passwd` 命令的手册条目，请输入 `man 5 passwd`。

通常，`man <n> <entry>` 会在第 `<n>` 章中找到 `<entry>` 的 man 手册页。

### Bash Shell 帮助设施

当你在提示符下输入命令时，shell 程序会读取你输入的内容，按需进行解释，并将结果传递给 Linux 操作系统。然后 Linux 执行请求的操作。许多 Linux 命令需要 Linux 查找并启动一个新程序。然而，shell 本身也能执行许多功能。

这些功能可以是简单且常用的命令，从而消除启动独立程序的开销；也可以是使 shell 环境更友好、更有用的设施。其中一个设施是 `help` 命令，它提供 `bash` shell 内置函数的信息。

在提示符下输入 `help`。你会看到至少以下部分内容：

```
GNU bash, version 1.14.15(1)
Shell commands that are defined internally. Type 'help' to see this list.
Type 'help name' to find out more about the function 'name'.
Use 'info bash' to find out more about the shell in general.
```

名称旁边的星号 (*) 表示该命令已被禁用。

```
%[DIGITS | WORD] [&] . [filename] : [arg...] alias [ name[=value] ... ] bg [job_spec] bind [-lvd] [-m keymap] [-r filena break [N] builtin [Shell-builtin [arg ...]] case WORD in [PATTERN [; PATTERN]. cd [dir] command [-pvV] [command [arg ...]] continue [n] declare [-frx] name[=value] ... dirs [-1] echo [-nE] [arg ...] enable [-n] [name ...] eval [arg ...] exec [-] file [redirection ...] exit [n] export [-n] [-f] [name ...] or exp fc [-e name] [-nlr] [first] [last fg [job_spec] for NAME [in WORDS ... ;] do COMMA function NAME { COMMANDS ; } or NA getopt optstring name [arg] hash [-r] [name ...] help [pattern ...] history [n] [ -awrn] [filename] if COMMANDS; then COMMANDS; [elif jobs [-lnp] [jobspec ...] | jobs - kill [-S sigspec | -sigspec] [pid let [arg ...] local name[=value] ... logout popd [+n ! -n] pushd [dir | +n ! -n] pwd read [-r] [name ...] readonly [-n] [-f] [name ...] or r return [n] select NAME [in WORDS ... ;] do CO set [--abefhknoutvXhDCP] [-o opti shift [n] source filename suspend [-f] test [expr] times trap [arg] [signal_spec] type [-all] [-type ! -path] [name typeset [-frxij] name[=value] ... ulimit [-SHacdmtfnpuv [limit]] umask [-S] [mode] unalias [-a] [name ...] unset [-f] [-v] [name ...] until COMMANDS; do COMMANDS; done variables - Some variable names an wait [N] while COMMANDS; do COMMANDS; done { COMMANDS }
```

你需要将 `help` 的输出管道传输到 `more`（`help | more`），以防止第一部分从屏幕上滚动过去。

### 通配符：* 和 ?

在许多深夜的纸牌游戏中，大小王会被混入牌堆。大小王是 `wild-cards`（通配牌），可以变成你选择的任何牌。这显然非常有用！Linux 也有通配符（wildcards）。它们比纸牌游戏中的大小王更有用。

Linux 有几个通配符。通配符在指定命令要操作的文件（或目录）时，是一种方便且强大的快捷方式。我们将简要介绍两个最常用的通配符：`*` 和 `?`。（Linux 支持相当多的其他通配符，但它们很少使用，在此处讨论只会使问题复杂化。）

最常用的是 `*`，它代表任何由一个或多个字符组成的组合。例如，`c*` 匹配所有以 c 开头的文件名。你可以通过输入 `ls /bin/c*` 来亲眼看到这一点。如果你在命令行输入 `ls /bin/c**t` 会发生什么？那在命令行输入 `ls /bin/*t` 呢？

`?` 通配符比 `*` 更具限制性。它只代表 *一个* 任意字符。你可以通过比较 `ls/bin/d*` 和 `ls/bin/d?` 来理解这一点。

> 注意
