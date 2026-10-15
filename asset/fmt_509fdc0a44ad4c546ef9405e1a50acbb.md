
`tsh` 中 `case` 语句（`switch`）的格式如下：

```bash
switch (str)
  case str1|str2)
    Statements
    breaksw
  case str3|str4)
    Statements
    breaksw
  default)
    Statements
    breaksw
```

你可以为每个条件指定多个离散值——例如 `str1`、`str2` 等，也可以使用通配符指定一个值。最后一个条件应当是 `default`，如果未满足其他任何条件，则执行它。对于每个指定的条件，将执行直到 `breaksw` 为止的所有关联语句。

之前为 `pdksh` 和 `bash` 显示的给定数字输出月份的示例，在 `tsh` 中可以写如下：

```tcsh
#!/bin/tcsh

set month = 5
switch ($ month)
  case 1: echo "Month is January" ; breaksw
  case 2: echo "Month is February" ; breaksw
  case 3: echo "Month is March" ; breaksw
  case 4: echo "Month is April" ; breaksw
  case 5: echo "Month is May" ; breaksw
  case 6: echo "Month is June" ; breaksw
  case 7: echo "Month is July" ; breaksw
  case 8: echo "Month is August" ; breaksw
  case 9: echo "Month is September" ; breaksw
  case 10: echo "Month is October" ; breaksw
  case 11: echo "Month is November" ; breaksw
  case 12: echo "Month is December" ; breaksw
  default: echo "Oops! Month is October!" ; breaksw
endsw
```

你需要用 `breaksw` 结束每个条件下的语句。如果你这样做，下一个条件下的语句也会被执行。

## break 和 exit 语句

你应该注意另外两个语句：`break` 语句和 `exit` 语句。

`break` 语句可终止迭代循环，例如 `for`、`until` 或 `repeat` 命令。

`exit` 语句可用于退出 shell 程序。你可以可选地在 `exit` 后面使用一个数字。如果当前 shell 程序是由另一个 shell 程序调用的，调用程序可以检查代码（`$?` 或 `$status` 变量，取决于 shell）并据此做出决定。

## 在 Shell 脚本中使用函数

与其他编程语言一样，shell 程序也支持函数。函数是一个可以多次调用的代码块，这有助于避免代码重复。

`pdksh` 和 `bash` 中函数的格式如下：

```bash
func() {
    Statements
}
```

你可以像使用命令一样通过名称调用函数。调用函数时，你可以使用特殊变量 `$1`、`$2` 等为其传递参数。

输出月份的函数示例如下：

```bash
#!/bin/sh

month() {
  case $1 in
    01 |) echo "Month is January";
    02 |) echo "Month is February";
    03 |) echo "Month is March";
    04 |) echo "Month is April";
    05 |) echo "Month is May";
    06 |) echo "Month is June";
    07 |) echo "Month is July";
    08 |) echo "Month is August";
    09 |) echo "Month is September";
    10) echo "Month is October";
    11) echo "Month is November";
    12) echo "Month is December";
    *) echo "Invalid parameter";
  esac
}

month $1
```

`tsh` 中函数的格式如下：

```tcsh
month() {
  switch ($1)
    case 1: echo "Month is January" ; breaksw
    case 2: echo "Month is February" ; breaksw
    case 3: echo "Month is March" ; breaksw
    case 4: echo "Month is April" ; breaksw
    case 5: echo "Month is May" ; breaksw
    case 6: echo "Month is June" ; breaksw
    case 7: echo "Month is July" ; breaksw
    case 8: echo "Month is August" ; breaksw
    case 9: echo "Month is September" ; breaksw
    case 10: echo "Month is October" ; breaksw
    case 11: echo "Month is November" ; breaksw
    case 12: echo "Month is December" ; breaksw
    default: echo "Oops! Month is October!" ; breaksw
  endsw
}

month $1
```

# 第 23 章

## 使用 Perl

Perl（Practical Extraction and Report Language）是一种强大的脚本工具，你可以用它来管理文件、创建报告、编辑文本并执行许多其他任务。Perl 包含在 Fedora 中，并被认为是该发行版的不可缺的一部分，因为 Fedora 依赖 Perl 处理许多软件服务、日志记录和工具。如果你从本书的 CD 盘进行完整安装，你会发现有 150 个用 Perl 编写的软件工具安装在 `/usr/bin` 和 `/usr/sbin` 目录下。

### Linux 下的 Perl

如果你熟悉其他一些编程语言，那么你很可能已经能够编写功能性的 Perl 代码。Perl 包含了 C、BASIC 以及其他多种编程语言的优秀特性——其中还融入了大量的 `awk`、`sed` 和 shell 脚本功能。Perl 是由 Larry Wall 在 20 世纪 80 年代为了为了克服 `awk` 命令在文件处理方面的局限性而创建的。Wall 已经负责了许多重要的 UNIX 工具的开发，例如 `patch` 命令（用于轻松地更新和将更改插入程序的源代码中），他声称 Perl 的意思是“病态折衷性主义的橡胶胶列表者（Pathologically Eclectic Rubber Lister）”。尽管 Perl 被设计为一种数据提取和报告生成语言，但它对许多 UNIX 和 Linux 系统管理员非常有吸引力；它可以用于创建新的软件工具，填补 shell 脚本能力与编译后的 C 程序之间的空白。Perl 相比其他 UNIX 工具的另一个优势是，它可以从二进制文件中处理并提取数据（即那些没有终止符或 `sed` 和 `awk` 无法处理的文件）。

> 在 Perl 中，“实现某功能有多种方法”。这是 Perl 的非官方格言，由于出现的频率之高，它被广泛缩写为 TIMTOWTDI。

Perl 将文本文件中的语言解释为 Perl 程序（尽管某些 Linux 用户可能称这些为脚本）。虽然有些人认为 Perl 是一个解释器，但这些程序实际上是在内存中编译的，然后由 Perl 内部解释器运行。你可以在 shell 命令行中使用 Perl 来执行单行 Perl 程序，但大多数情况下，你是将程序（通常以 `.pl` 结尾）作为命令来运行的。这些程序通常可以在任何计算机平台上运行，因为 Perl 已经移植到几乎每一个操作系统。你会在本书随附的 CD-ROM 中找到 RPM 文件。

Perl 程序用于支持许多 Fedora 服务，例如系统日志。例如，`logwatch.pl` 程序每天早上 4:20 由系统上的 `cron`（计划）守护进程运行。这个包含 690 行的 Perl 程序物理上位于 `/etc/log/scripts/` 目录下，但作为 `/etc/cron.daily` 目录下的名为 `00-logwatch` 的符号链接启动。该程序（可以通过编辑配置文件 `logwatch.conf` 进行配置）在分析日志后生成并通过电子邮件发送一份简短报告。
