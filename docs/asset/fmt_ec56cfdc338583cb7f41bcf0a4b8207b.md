
```
    echo "ERROR: $REQ is not a directory." >&2

  fi

}
```

首先通过将 `REQ` 设置为 `$1` 的值来检查是否提供了参数。如果没有提供参数，则假设用户指的是当前目录。

然后检查请求的目录是否确实是一个目录。如果是，则进入该目录并用新目录的完整路径更新目录栈。你不能直接使用 `$REQ` 中的值，因为它可能是一个相对路径。

最后，通过调用 `dirs` 函数打印栈的内容。通过这种方式，该函数不需要知道如何打印栈。你只需要知道 `dirs` 会打印栈即可。

这使你能够更改函数（例如 `dirs`）的实现，而不影响其他函数。需要记住的一点是，如果你更改了某个函数（如 `dirs`）的实现，它不会影响其他函数。

# 24小时自学Shell脚本编程

第14小时：函数 目录 索引 上一节 下一节

本章章节：

- 创建和使用函数
- 结论
- 函数之间的数据共享（示例）
- 习

上一节 下一节

## 习

- 1. 编写一个函数，创建一个目录（及其所有父目录），切换到该目录，然后打印该目录的完整路径。请在所有级别包含错误检查。确保所有错误信息都由你的脚本生成，而不是由执行的命令生成。
- 2. 第13章“输入/输出”引入了在Shell 脚本中提示用户的概念。编写一个函数，可以用于提示用户响应并将用户的响应存放在变量 `RESPONSE` 中。请在所有级别包含错误检查。

# 24小时自学Shell脚本编程

第14小时：函数 目录 索引 上一节 下一节

本章章节：

- 创建和使用函数
- 结论
- 函数之间的数据共享（示例）
- 习

上一节 下一节

© Copyright Macmillan Computer Publishing. 版权所有。

24小时自学Shell脚本编程 目录 索引

第15小时：文本过滤器 < 上一节 下一节 >

本章章节：head 和 tail 命令。

总结 习

使用 grep 统计单词

< 上一节 下一节 >

# 第15小时

## 文本过滤器

Shell 脚本经常被调用来对其执行的命令的输出进行处理和重新格式化。有时这项任务只需要通过过滤某些行来仅显示输出的一部分。在大多数情况下，所需的处理要复杂得多。

在本章中，你将查看几个在 Shell 脚本中被大量用作文本过滤器的命令。这些命令包括

- `head`
- `tail`
- `grep`
- `sort`
- `uniq`
- `tr`

我还将向你展示如何结合这些命令，以极其强大的方式过滤文本。

### head 和 tail 命令

#### head 命令
`tail` 命令

在第3章“处理文件”中，你曾学习使用 `cat` 命令查看文件内容。该命令允许你查看整个文件，但通常你可能需要对显示的行进行更多控制。`head` 和 `tail` 命令提供了这种这种控制功能。

### head 命令

`head` 命令的基本语法为：

```bash
head [-n lines] files
```

`files` 是你希望 `head` 命令处理的文件列表。如果没有 `-n lines` 选项，`head` 命令将显示其标准输入的前10行。该选项则会显示指定的行数。

虽然这个命令对于查看大型 README 文件很有用，但它的真正的威力体日常应用中。考虑以下问题：我需要为我的公共 HTML 目录生成一个最近访问的文件列表。最简单的解决方案是什么？

通过拆解问题可以很容易生成解决方案。首先，我使用以下命令生成我的公共 HTML 文件列表：

```bash
$ ls -l /home/ranga/public_html
```

在我的情况下，这生成了以下文件和目录列表：

```
RCS
cgi-bin
downloads
humor
images
index.html
misc
projects
school
```

接下来，我需要按访问日期对列表进行排序。我可以通过为 `ls` 命令指定 `-ut`（按最后访问时间排序）选项来实现：

```bash
$ ls -lut /home/ranga/public_html
```

输出现在发生了变化：

```
RCS
humor
misc
downloads
images
resume
projects
school
cgi-bin
index.html
```

为了获取五个最近访问的文件列表，我可以将 `ls` 命令的输出管道到：

```bash
ls -lut /home/ranga/public_html | head -5
```

这产生了以下列表：

```
index.html
RCS
humor
misc
downloads
```

### tail 命令

`tail` 命令的基本语法与 `head` 命令相似：

```bash
tail [-n lines] files
```

这里 `files` 是 `tail` 命令应该处理的文件列表。如果没有 `-n lines`，`tail` 命令将显示其标准输入的最后10行。有了这个选项，它将改为显示指定的行数。

为了说明 `tail` 命令的用法，考虑为我的系统生成一个五个最旧邮件的列表的问题。

我可以再次从 `ls -1` 命令开始，但这次将使用 `-t`（按最后修改时间排序）选项代替之前的选项：

```bash
$ ls -lt /var/spool/mail
```

为了获取最后五个，我将使用 `tail` 而不是 `head`：

```bash
$ ls -lt /var/spool/mail | tail -5
```

在我的系统上生成了以下列表：

```
anna
root
amma
vathsa
ranga
```

在这个列表中，文件按从新到旧的顺序排列。要反转顺序，我也可以为 `ls` 命令指定 `-r` 选项：

```bash
$ ls -lrt /var/spool/mail | tail -5
```

在我的系统中，我得到了这个列表：

```
ranga
vathsa
amma
root
anna
```

### follow 选项

`tail` 命令极其实用的功能是 `-f`（f 代表 follow）选项：

```bash
tail -f file
```

指定 `-f` 选项允许你在程序向文件写入的同时检查该文件。我经常必须查看日志，但不想等待程序结束，所以我使用 `tail -f` 来监控日志。例如：

```bash
$ tail -f /var/log/syslog
```

unix 关联了一些额外信息。与 unix 对应项不同，它实现了一些很好的选项，使其成为 unix 文件名，但它们确实是，而且正确处理它们是必要的。

### 从标准输入 (STDIN) 读取

当未指定行时，`grep` 在 STDIN 输入的行上查找匹配项。这使得它连接管道非常有用。

例如，以下命令用于在 `who` 命令的输出查找名为 rango 的用户：

```
$ who | grep rango
ranga tty1 Aug 26 14:12
ranga ttyp2 Nov 23 14:15 (rishi.bosland.u)
```

### -v 选项

大多数时候，你使用 `grep` 在文件中搜索查找特定单词，但有时你想获取所有不匹配特定内容的行列表。

使用 `grep`，这可以通过 `-v` 选项来指定。例如，以下命令产生 `/etc/passwd` 中所有不包含 `home` 单词的列表：

```
$ grep -v home /etc/passwd
```

在我的系统上，输出如下：

```
root*:0:0:::/sbin/sh
daemon:*:1:5:::/sbin/sh
bin*:2:2:/usr/bin:/bin/sh
sys*:3:3:::
adm*:0:4:/var/adm:/bin/sh
uucp*:5:3:::/var/spool/uucpublic:/usr/bin/uucp/uucico
lp*:9:7:::/var/spool/lp:/bin/sh
nobody*:2-2::
```

`-v` 选项的一个常见用途是解析 `ps` 命令的输出。例如，如果我正在寻找系统中运行的所有 `bash` 实例，我可以使用以下命令：

```
/bin/ps -ef | grep bash
```

有时输出看起来所示：

```
rango 3277 3276 2 13:41:45 pts/0 0:02 -bash
rango 3463 3277 4 18:38:26 0:00 grep bash
```

列表中的第二个进程是我刚刚运行的 `grep`。因为它并不是真正的 `bash` 实例，我可以通过以下方式将其移除：

```
/bin/ps -ef | grep bash | grep -v grep
```

这移除了多余的输出：

```
ranga 3277 3276 0 13:41:45 pts/t0 0:02 -bash
```
