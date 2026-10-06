
一个在支持 POSIX.2 风格本地化的系统上实际运行的示例

## POSIX Shell

POSIX.2 规定了 shell 的语义以及一组用户可以用于开发可移植 shell 的实用程序集合。其次要目的是促进用户的可移植性。

POSIX.2 独立于 POSIX.1，一个系统可以在不符合 POSIX.1 的情况下声称符合 POSIX.2。这对于大多数其他 POSIX 标准是不可能的，因为这些标准都是以 POSIX.1 为基础的。在实践中，你可以预期任何 UNIX 系统在几年内符合 POSIX.1 和 POSIX.2。许多非 UNIX 系统也会符合，使它们至少在表面上是“类 UNIX”的。尽管 Linux 没有经过正式认证，但它符合 POSIX.2 的要求。

## 可移植 shell 应用程序的实用程序

POSIX.2 规定了 72 个强制实用程序，称为执行环境实用程序。它们大部分来自 SVR3 或 Berkeley UNIX，或源自 UNIX 实用程序。几个如 `pathchk` 和 `printf` 是 POSIX.2 委员会的发明。这些创建是为了满足与可移植性特别相关的要求。其他工具采用了 UNIX 系统工具，但更改了语义，以解决 SVR3 和 Berkeley UNIX 之间的冲突，移除在国际化背景下不合理的行为，或修复不一致之处。

## 946 附录 D：POSIX 标准

执行环境如下所示。未在本文正文中描述的实用程序用星号（*）标记。与其传统的 UNIX 系统相比有显著差异的实用程序用剑号（†）标记。新的实用程序用双剑号（‡）标记。

| 执行环境的实用程序 | | | |
|---|---|---|---|
| awk | bc* | cat | |
| cd | chgrp | chmod | |
| csum*‡ | cmp* | comm | command*‡ |
| cp | cut* | date | dd* |
| diff | dirname* | ed | |
| env* | expr | false | find |
| fold* | getconf*‡ | getops | grept |
| head | id* | join* | kill* |
| ln | locale* | localef*‡ | logger*‡ |
| logname | lp* | ls | mailx* |
| mkdir | mkfifo*‡ | mv | nohup |
| od* | paste | pathck*‡ | pax* |
| pr | printf*‡ | pwd | read |
| rm | rmdir | sed | sh |
| sleep | sort | stty | tail |
| tee | test | touch | tr |
| true | tty | umask | uname* |
| uniq | wait | wc | xargs | |

以下是 POSIX.2 中新增实用程序的简要描述。

### cksum

`cksum` 实用程序用于为文件计算校验和。当你发送或接收文件时，使用它可以确保文件在传输过程中没有被损坏。`cksum` 实用程序替换了在 BSD 和 SVR4 中都存在的名为 `sum` 的命令。POSIX.2 委员会没有使用 `sum`，因为 BSD 和 System V 具有不同且不兼容的实现。`cksum` 使用的算法基于以太网标准 ISO 8802-3 的循环冗余校验。

语法为：

```
cksum [file...]
```

你可以在命令行上指定零或多个文件。如果你没有指定文件名，`cksum` 会对标准输入计算校验和。对于每个输入文件，`cksum` 会向标准输出写入文件的校验和、字节计数和名称。

### command

`command` 实用程序以一种设计好的方式执行任何命令行，以确保你执行的是你预期的命令版本。如果你输入：

```
command command_name [arguments...]
```

shell 将执行 `command_name`，而不会查找同名的 shell 函数。如果你使用 `-p` 选项，例如：

```
command -p command_name [arguments...]
```

shell 将使用特殊的 `PATH` 值来搜索 `command_name`，该值保证能够找到所有标准实用程序。

如果系统支持 POSIX.2 的用户可移植性实用程序选项，则 `command` 具有更多选项标志。使用 `-v` 选项，`command` 会报告 `command_name` 的绝对路径而不运行它，它会使用你的 `PATH` 变量进行搜索。如果 `command_name` 是内置实用程序、保留字或函数，则只写入其名称。如果 `command_name` 是别名，则会定义代表该别名的命令行。`-V` 选项类似，但它会区分函数、保留字和内置实用程序。

### getconf

`getconf` 实用程序让你能够确定各种选项和依赖于配置参数的值，例如系统是否支持用户可移植性实用程序选项，或系统支持的最大文件名长度。

你通过以下两种方式之一调用 `getconf`：

```
getconf system_var
```

```
getconf path_var pathname
```

第一种语法用于系统变量。例如，你可以通过以下调用确定任何用户 ID 可以打开的最大并发进程数：

```
getconf CHILD_MAX
40
```

第二种语法用于确定在文件层次结构中可能随位置变化的变量值。例如，你可以通过命令确定 `/tmp` 目录中文件的最大允许长度：

```
$ getconf NAME_MAX /tmp
255
```

你可以查询的符号集由于太长而无法在此列出，你可以在 POSIX.2 标准中找到。下表列出了一些更有用的符号：

| 符号 | 含义 |
| --- | --- |
| `getconf PATH` | 输出能够找到所有标准实用程序的 `PATH` 变量值。 |
| `getconf LINE_MAX` | 输出你可以可靠传递给处理文本文件的标准实用程序的输入行最大长度。它必须至少为 2048。 |
| `getconf POSIX2_UPE` | 如果系统支持用户可移植性实用程序选项，则显示值 1。 |
| `getconf POSIX2_LOCALEDEF` | 如果系统支持用户可移植性实用程序选项，则显示值 1。 |
| `getconf PATH_MAX` | 报告此文件系统的路径最大长度。 |
| `getconf NAME_MAX` | 报告此文件系统中文件名的最大长度。 |

### locale

`locale` 实用程序提供了国际化的手段。`locale` 的设计目的是让非交互式脚本遇到错误时将其记录在系统管理员可以检查的地方。

### localedef

`localef` 实用程序允许用户定义自己的 `locale`，如果实现支持此项。定义 `locale` 所需的信息量巨大，超本书的范围。

### logger

`logger` 实用程序提供了写入日志文件的手段。

### mkfifo

POSIX.1 包含 `fifo()` 函数，允许程序创建 `fifo` 特殊文件。此实用程序在 shell 层提供了相同的功能。语法为：

```
mkfifo [-m mode] file ...
```

默认情况下，创建的 `fifo` 模式为 660，由调用者的 `umask` 修改。如果使用 `-m`，则使用模式参数。

### pathchk

`pathchk` 实用程序允许可移植 shell 脚本确定路径在给定系统上有效。语法为：

```
pathchk [-p] pathname ...
```

对于每个路径参数，`pathchk` 将检查其长度是否超过 `PATH_MAX`，每个组件的长度是否超过 `NAME_MAX`，路径中的每个现有目录是否可搜索。如果你使用 `-p` 选项，则 `pathchk` 将执行严格的可移植性检查：路径将检查最大 255 字节，文件名检查最大长度 14 字节。

# 950 附录 D：POSIX 标准

## pax

`pax` 的名字表面上是 tar 和 cpio 格式支持者的缩写。`pax` 工具可以读取和写入多种格式的归档。这些格式特别但不限于 POSIX.1 的 tar 和 cpio 格式。POSIX.2 委员会的既定意图是在未来的标准修订中定义一种新的归档格式。该格式将成为 `pax` 的默认格式。

`pax` 命令的语法过于复杂，无法在此描述。如果它存在于你的系统中，请查阅手册页。

## printf

`printf` 工具的发明主要是为了处理 BSD 和 System V 版本的 `echo` 之间的不兼容性。POSIX.2 规定，任何 `echo` 命令行中的 `-n` 作为第一个参数或任何以 `\` 开头的参数，其行为由实现定义。要直接打印任何最简单的字符串，你应该使用 `printf`。

`printf` 代表“格式化”，`printf` 工具允许你在格式化参数的控制下打印字符串。其语法定义为：

```
printf format [ string ... ]
```
