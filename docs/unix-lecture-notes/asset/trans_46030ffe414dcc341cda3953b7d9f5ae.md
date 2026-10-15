

# NAME

本节给出条目的名称或名称，并简要说明其用途。

# SYNOPSIS

本节总结所描述条目的使用方法。

# DESCRIPTION

本节描述头文件的功能。

# APPLICATION USAGE

本节为信息性内容。本节对应用程序开发人员关于该条目提出警告和建议。在本节的警告和建议与 POSIX.1-2008 本卷的规范部分发生冲突时，应以规范材料为准。

# RATIONALE

本节为信息性内容。本节包含有关 POSIX.1-2008 本卷内容的历史信息，以及标准制定者为何包含或舍弃某些特性。

# FUTURE DIRECTIONS

本节为信息性内容。本节提供应作为当前思路指南的评论；不一定会采纳这些未来方向。

# SEE ALSO

本节为信息性内容。本节给出相关信息的参考。

重要的部分是 NAME、SYNOPSIS、DESCRIPTION 和 SEE ALSO。

例如

```
$ man stdlib.h
```

将显示头文件 <stdlib.h> 的手册页。这是一个有用的功能。但如果你不知道你需要的命令的名称，也不知道可能有用或相关的任何文件名称，那么你就不知道要阅读哪本手册页。UNIX 系统提供了各种克服此问题的方法。

## 2.4.2 Man Page Searching

最基本且保证在所有系统上都能工作的解决方案是使用 man 命令的搜索功能。要搜索 NAME 部分的单行摘要中包含特定关键字的所有手册页，你可以输入

```
$ man -k keyword
```

这仅在安装手册页时已构建 whatis 数据库的情况下才有效，因此你受制于系统管理员。例如，输入

## 2.5 Digging Deeper into the who Command

对 utmp 文件的手册搜索输出看起来会像这样：

```
endutent [getutent] (3) - access utmp file entries
getutent          (3) - access utmp file entries
getutid [getutent] (3) - access utmp file entries
getutline [getutent] (3) - access utmp file entries
login              (3) - write utmp and wtmp entries
logout [login]     (3) - write utmp and wtmp entries
pututline [getutent] (3) - access utmp file entries
sessreg            (1x) - manage utmp/wtmp entries for non-init clients
setutent [getutent] (3) - access utmp file entries
utmp               (5) - login records
utmpname [getutent] (3) - access utmp file entries
utmpx.h [utmpx]    (0p) - user accounting database definitions
wtmp [utmp]        (5) - login records
```

第一个词是手册页的主题，第二个是手册页标题，第三个是手册的章节号，最后是主题的简要描述。

每个 UNIX 系统都有一个手册卷，专门处理命令使用的文件。编号可能不同。从上面的输出来看，utmp 文件似乎在手册页的第 5 节中描述：

```
utmp [utmp] (5) - login records
```

此外，行

```
wtmp [utmp] (5) - login records
```

表明描述 wtmp 文件的手册页与描述 utmp 的手册页相同。显然，utmp 在手册的第 5 节中有一个手册页。要指定要显示的具体章节，你需要将其指定为选项。语法各不相同；在 RedHat Linux 中以下任一方式都有效：

```
$ man 5 utmp
$ man -S5 utmp
```

输出中还有一行

```
utmpx.h [utmpx] (0p) - user accounting database definitions
```

`<utmpx.h>` 头文件描述了对 utmp 文件的 POSIX 兼容接口。此接口与 `<utmp.h>` 文件的接口不同。我们将使用过时的 `<utmp.h>` 接口进行初步尝试，更深入地探索 utmp 文件，从我们键入上述任一 man 命令时系统提供的手册页开始。之后我们将考虑使用另外两个接口，即 POSIX utmpx 接口和一个 GNU 扩展，即线程安全的函数 `getutent_r()` 及其同类函数。

下面显示了来自 RedHat Enterprise Linux Release 4 的 utmp 手册页的开头。

```
NAME
    utmp, wtmp - login records

SYNOPSIS
        #include <utmp.h>

DESCRIPTION
        The utmp file allows one to discover information about who is currently
        using the system. There may be more users currently using the system,
        because not all programs use utmp logging.

        Warning: utmp must not be writable, because many system programs
        (foolishly) depend on its integrity. You risk faked system logfiles and
        modifications of system files if you leave utmp writable to any user.
        The file is a sequence of entries with the following structure declared
        in the include file (note that this is only one of several definitions
        around; details depend on the version of libc):

        (lines omitted here)
```

首先请注意，它告诉我们相关头文件是：`<utmp.h>` 这是编译器在你的程序中包含指令 `#include <utmp.h>` 时将使用的头文件⁶。接下来，它向系统管理员发出警告，不要让任何人除了其所有者超级用户之外都可以写入该文件。然后在向我们展示包含文件的内容之前，它警告我们其余的人，内容可能因安装而异。

由于 UNIX 是一个免费的、社区支持的操作系统，它一直在不断发展。你可能会发现书中或这些笔记中描述的内容与你在系统上观察到的不同。并非有什么是正确或错误的，而是 UNIX 是一个不断变化的目标，系统在细节上可能有所不同。例如，旧版本 Linux 中 utmp 的手册页将与此处显示的非常不同。甚至 utmp 文件本身的位置也不同。UNIX 的后期版本增加了系统函数以提供数据抽象层，以便程序员无需了解文件的实际结构。问题在于不同版本的 UNIX 对 utmp 结构有不同的定义，直接访问该结构的程序在不同系统上会失败。

⁶文件系统中可能有许多名为 `utmp.h` 的文件。每个编译器都有自己的方法来决定使用哪一个。GNU 编译器集合 gcc 在特定位置安装自己的头文件，并默认使用这些文件。gcc 使用的默认搜索路径通常为

`/usr/local/include`
`target-install-dir/include`
`/usr/include`

其中 `target-install-dir` 是 gcc 在机器上安装的目录。这将在稍后更详细地解释。

