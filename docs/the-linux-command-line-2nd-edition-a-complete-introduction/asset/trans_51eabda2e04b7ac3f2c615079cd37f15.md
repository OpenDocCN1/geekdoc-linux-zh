

## 所有手册页中最残酷的一页

如我们所见，Linux 和其他类 Unix 系统附带的手册页是作为参考文档而非教程使用的。许多手册页难以阅读，但我认为难度大奖非 bash 的手册页莫属。在我为本书做研究时，我仔细审阅了它，以确保覆盖了其大部分主题。打印出来有 80 多页，内容极其密集，而且其结构对新用户来说完全没有意义。

另一方面，它又非常准确且简洁，同时极其完整。所以，如果你有胆量，就去看看吧，并期待有一天你能读懂它，然后一切都变得有意义。

## info - 显示程序的 info 条目

GNU 项目为其程序提供了一种替代手册页的方式，称为 “info”。Info 页面由一个名为 info 的阅读器程序显示，这个名字起得很恰当。Info 页面跟网页一样带有超链接。下面是一个示例：

```
File: coreutils.info,  Node: ls invocation,  Next: dir invocation,
Up: Directory listing

10.1 `ls': List directory contents
===================================

The `ls' program lists information about files (of any type,
including directories).  Options and file arguments can be intermixed
arbitrarily, as usual.

    For non-option command-line arguments that are directories, by
default `ls' lists the contents of directories, not recursively, and
omitting files with names beginning with '.'.  For other non-option
arguments, by default `ls' lists just the filename.  If no non-option
argument is specified, `ls' operates on the current directory, acting
as if it had been invoked with a single argument of '.'

By default, the output is sorted alphabetically, according to the
locale.
-- Info: (coreutils.info.gz)ls invocation, 63 lines --Top--------
```

info 程序读取 info 文件，这些文件按树状结构组织成单个节点，每个节点包含一个主题。Info 文件包含超链接，可以让你从一个节点移动到另一个节点。超链接可以通过其前导星号识别，将光标放在其上并按回车键即可激活。

要调用 info，键入 “info”，后面可选地跟一个程序名。下面是一个在显示 info 页面时用来控制阅读器的命令表：

**表 5-2：info 命令**

| 命令 | 动作 |
|---|---|
| ? | 显示命令帮助 |
| PgUp 或 Backspace | 显示上一页 |
| PgDn 或 Space | 显示下一页 |
| n | 下一个 - 显示下一个节点 |
| p | 上一个 - 显示上一个节点 |
| u | 向上 - 显示当前节点的父节点，通常是一个菜单。 |
| Enter | 跟随光标处的超链接 |
| q | 退出 |

到目前为止，我们讨论过的大多数命令行程序都属于 GNU 项目的 “coreutils” 软件包，因此键入：

```shell
[me@linuxbox ~]$ info coreutils
```

将显示一个菜单页面，其中包含指向 coreutils 软件包中每个程序的超链接。

## README 和其他程序文档文件

系统中安装的许多软件包都有文档文件存放在 /usr/share/doc 目录中。其中大多数以纯文本格式存储，可以用 less 查看。有些文件是 HTML 格式，可以用网页浏览器查看。我们可能会遇到一些以 “.gz” 扩展名结尾的文件。这表示它们已经用 gzip 压缩程序压缩过。gzip 软件包包含一个名为 zless 的特殊版本的 less，它可以显示 gzip 压缩的文本文件的内容。

## 使用 `alias` 创建你自己的命令

现在让我们迎来第一次编程体验！我们将使用 `alias` 命令创建自己的命令。但在开始之前，我们需要揭秘一个小命令行技巧。每条命令之间用分号分隔，就可以在一行中输入多条命令。它像这样工作：

```
command1; command2; command3...
```

下面是我们将要使用的示例：

```shell
[me@linuxbox ~]$ cd /usr; ls; cd -
bin  games  kerberos  lib64  local  share  tmp
etc  include  lib  libexec  sbin  src
/home/me
[me@linuxbox ~]$
```

正如我们所见，我们在一行中组合了三个命令。首先切换到 `/usr` 目录，然后列出目录内容，最后使用 `cd -` 返回原始目录，于是我们回到起始位置。现在，让我们用别名把这个序列变成一个新命令。我们要做的第一件事是为新命令想出一个名字。让我们试试 “test”。在此之前，最好先确认 “test” 这个名称是否已被使用。为了查明，我们可以再次使用 `type` 命令：

```shell
[me@linuxbox ~]$ type test
test is a shell builtin
```

糟糕！名称 “test” 已被占用。让我们试试 “foo”：

```shell
[me@linuxbox ~]$ type foo
bash: type: foo: not found
```

