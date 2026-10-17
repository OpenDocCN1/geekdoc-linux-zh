
就这样。Shell，`bash` 执行该文件中的三个命令并退出。可以想象的最简单的 Shell 脚本就是命令本身。例如，在写这本书时，我偶尔想捕捉某个特定窗口的快照。我是通过 `import` 命令做到的（该命令在第 9 章讨论过）。通常，我会从另一个桌面捕捉图像，即一台放在我写作工作站旁边的笔记本电脑。之所以做这两件事，是因为我可以这样做。

## 关于变量的更多

这里有很多内容。脚本会检查是否有任何参数。如果参数计数（这就是变量 `$#` 的含义）为 0，它会打印一条错误消息并退出。如果我记得传递一个文件名，我就会得到一个漂亮得多、类似“干得好”的消息。

```
$ grabwin etern.tif
etern.tif 捕获完成。
```

当你谈论 shell 编程时，你会在不同层级处理变量。你有之前看到的内置变量，也可以赋值变量。例如，在不编写脚本的情况下，在你的 shell（命令行）提示符处输入这一行：

```
hours=24
```

然后输入：

```
echo "There are $hours hours in a typical day"
```

系统的响应如下：

```
There are 24 hours in a typical day.
```

你通过在变量前加一个美元符号 (`$`) 来访问该变量。如果你只是在 shell 脚本中输入一行（不是 `hours=24` 这一行），让该脚本执行并运行，你会得到：

```
There are in a typical day.
```

shell 脚本没有获取到 `$hours` 变量。为了让 shell 脚本知道 `hours` 变量，你需要导出它（`export`）。有两种方法。其中一种是像你之前那样赋值变量，然后输入命令 `export hours`。你也可以把整个内容写在一行，以节省击键次数。

```
export hours="24"
```

现在运行脚本会显示一条更智能的消息，说明一天中到底有多少小时。除了用户分配的变量外，脚本还可以利用环境变量。这些变量是系统在你登录时为你设置的。其中一些变量有时会被用户主目录下的 `.bash_profile` 文件或全局的 `/etc/profile` 覆盖。一个常见的修改变量是 `PATH` 变量，它列出了可执行文件的可能搜索路径。检查你自己的 `HOME/.bash_profile` 文件中对以下内容的引用：

```
PATH=$PATH:$HOME/bin:/usr/local/bin
export USER BASH_ENV PATH
```

如你所见，你可以通过在赋值中引用它来修改环境变量。第二行导出了 `PATH` 和许多其他变量，以便你在任何可能工作的 shell 和任何环境中都能使用它们。要查看你的环境变量，请输入此命令：

```
env
```

## 特殊字符

某些字符对 shell 来说有特定的含义。以下是你将遇到的示例。

| 字符 | 描述 |
| --- | --- |
| `$` | 突出显示变量名的开头 |
| `#` | 注释字符 |
| `\` | 匹配字符 |
| `?` | 匹配任意单个字符 |
| `*` | 匹配任意数量的字符 |
| `'` | 定义字符串 |
| `` ` `` | 执行反引号内的内容 |
| `\` | 转义随后的字符 |
| `[]` | 列出括号内的字符范围 |

美元符号 (`$`) 是你已经见过的一个。它表示变量名的开始。你还见过注释字符 (`#`)，在接下来的章节中，我将讨论它的某些特殊属性。在很早的第 5 章中，我谈到了问号 (`?`) 和星号 (`*`)。

首先，我想谈谈反斜杠 (`\`)。当在特殊字符前面加一个反斜杠时，它会阻止 shell 解释该特殊字符。这是一个简单且我认为有效的演示。尝试输入此命令：

```
$ echo *
```

你是否得到了目录中每个文件并用空格分隔的列表？我所想的如此。再试一次，这次在星号前面加一个反斜杠。

```
$ echo \*
```

注意，shell 现在输出一个单个星号。每当你想要使用像 shell 中的那些特殊字符，但你不希望它们被以任何特殊方式处理时，在它们前面加一个反斜杠（我猜这是一种特殊处理）。

## 关于这一点我可以完全赞同

啊，引号。我有许多喜欢的引用。其中之一是“我想要永生，除非战斗到死”，这是 Spider Robinson 说过的一句话，但我希望我曾那样过。抱歉，这是不同风格的引言。

当然，我应该谈谈引号对 shell 意味着什么。双引号 (`"`) 告诉 shell 将内部内容解释为字符串。这是定义变量或将文本回显终端的方式。

```
my_variable="This is a double quote \" inside my double quotes."
```

你会注意到我在双引号内部又放了一个双引号，但用反斜杠转义了该字符。如果我输入 `echo $my_variable`，得到的是：

```
This is a double quote " inside my double quotes.
```

单引号 (`''`) 从表面上看似乎与双引号的作用相同，但它们确实有另一个重要功能。让我们设置几个变量并编写一个小的 shell 脚本。

```
$ os_name="Linux"
$ os_desc="way cool"
$ echo "$os_name is $os_desc"
Linux is way cool.
```

这大体是你在这里预期的结果。现在，我们在那个 `echo` 命令周围加上单引号，看看区别。

```
$ echo '$os_name is $os_desc.'
$os_name is $os_desc.
```

嗯……似乎单引号阻止了 shell 将美元符号解释为变量名。现在，那些反引号（`` ` ``）呢？反引号（或反引号）的特殊之处在于它们会执行内部的内容。例如，如果你有一个 shell 脚本回显 "The current date and time information is .."，而你想填充其他内容，你会想要 `date` 命令的输出。这是此此的一种方法：

```
the_date=`date`
echo "The current date and time information is $the_date."
```

另一种简单的方法是把反引号包裹的 `date` 命令放在 `echo` 行本身中。

```
echo "The current date and time information is `date`."
```

## 真正编写 shell

我提到的内容之一是 shell 是一种真正的编程语言。这完全正确。你可以使用如 `if...then...else`、`while` 和 `for` 循环、`case` 语句等结构。为了给你一个概念，这里有一个在意大利数学家 Leonardo Pisano 之后运行的小脚本。

```
# 运行斐波那契数列
fib_iterations=0
last_number=1
echo "The sequence starts with 1"
until [ $fib_iterations -ge 10 ]
do
    fib_iterations=$(expr $fib_iterations + 1)
    echo "number is $last_number"
done
```

## 指定 Shell

如果你查看 `/etc/rc.d/init.d` 目录下的某些启动脚本，或者可能是 `/etc/init.d` 目录，你会注意到它们以一个非常有趣的小结构开头。以下是我的 `inet` 启动脚本的前五行：

```
[root@testsys /root]# head -5 /etc/rc.d/init.d/inet
#!/bin/sh
# inet Start TCP/IP networking services. This script
# starts the Internet Network Daemon.
```

看到开头那行 `#!/bin/sh` 了吗？这种被称为 hash-bang（释字节符）的 `#!/path_to_shell` 结构是强制使用特定类型的 shell 来执行脚本的一种。假设你创建了一个使用 C shell 特有结构来工作的 shell 脚本。如果让 bash 来执行它，显然无法得到你想要的结果。此外，还有一些系统函数，例如 `at` 命令（将在下一章介绍），它们将使用 `/bin/sh` 执行所有命令。如果你创建的脚本使用了某些基础 `sh` 无法理解的 bash 命令怎么办？

解决方案很简单。只需在你的 shell 脚本顶部加上这一行：

```
#!/bin/bash
```

现在，即使运行脚本的 shell 是 `/bin/sh`，它也会切换到 `/bin/bash` 来执行该脚本。这也被用于定义其他的脚本环境。Perl 脚本开头会有这一行：

```
#!/usr/local/bin/perl
```

请记住，Perl 解释器的路径可能随系统而异。

## Perl

让我们直接进入 Perl 程序世界吧。将以下代码输入到一个简单的文本文件中（随你怎么喜欢命名），使该文件具有可执行权限，然后运行它。

```
#!/usr/bin/perl
# print "Perl, the Practical Extraction and Report Language, \n"
print "was was written by Larry Wall back in the eighties. \n";
```

Perl 被称为编程语言的“瑞士军刀”、互联网的“胶带”，以及其他同样有趣的称呼。对于你这个管理员来说，Perl 是一种编写强大应用程序的方法，而无需改变职业并成为一名专业程序员。

该语言本身汲借了 shell 脚本、C 语言、BASIC 以及其他语言。Perl 有几条格言。也许其中最著名的是“条条路都通”（There's more than one way to do it）。显然，这是该语言创建期间的一条格言。

Perl 的强大之处之一在于其庞大的用户群。它是全球 Web 上最流行的编程语言之一，用于大量的 CGI（通用网关接口，一组用于 Web 编程应用程序的钩子）。正如此，很容易被误导而仅从这个角度来看它。Perl 是一个很棒的小工具箱，你应该更好地了解它。

还记得我在第 11 章中提到的 CPAN 存档吗？那里有大量的预制模块，可以帮助你完成无数任务。

## Perl 实战：一个监控磁盘空间的脚本

有几本和这本书一样厚的书涵盖了 Perl 这个主题，所以我并不会假装能在几页内告诉你需要知道的一切。相反，我将为你提供一个实用的 Perl 脚本示例，用于你的日常系统维护工作。在这种情况下，你将创建一个 Perl 脚本，并将其设置为定期运行（下一章介绍自动化），以通知你关键的磁盘空间问题。如果磁盘空间低于总量的 10%，就会有人收到通知。让我们来看看它，然后我会告诉你发生了什么。

```
#!/usr/bin/perl
# checkusage.pl checks the usage of the disk space in percentage
# and e-mails it to sysadmin if greater than 90 percent

$admin_addr = 'marcel@my_domain.com';
&check_dfusage;
exit();
```

### 子程序

```
sub check_dfusage {
  @diskinfo = `df`;
  $message_text = '';
  foreach (@diskinfo) {
    ($dirname, $arg1, $arg2, $arg3, $arg4, $arg5, $arg6) = \
      split(' ', $_, 7);
    ($arg4num, $therest) = split('%', $arg4, 2);
    if ($arg4num > 90) {
      $message_text .= "Directory $dirname is now at\n$arg4num\n";
    }
  }
  print $arg4 . "\n";
  if ($message_text ne '') {
    &message;
  }
}

sub message {
  open(SF, "| mail -s 'Important system info' $admin_addr");
  print SF "$message_text";
  close(SF);
}
```

你要做的第一件事是设置管理员的邮箱地址。这可以是你的邮箱，也可以是一个应该被通知的用户列表。注意，电子邮件地址中的商业符号 (`@`) 已经用反斜杠字符进行了转义。

有两个子程序，每个子程序都通过行首保留字 `sub` 来标识。根据第一个子程序（称为 `check_dfusage`）的结果，你可能调用或不调用第二个程序（称为 `message`）来执行工作。

变量 `@diskinfo` 是 Perl 中所谓的数组变量。`df` 命令的结果被解析成数组中的每一行。我感兴趣的是第四列（文件系统名称），在脚本中由 `$arg4` 表示。如果 `$arg4`（减去百分号）大于 90，就会准备消息并通知你的管理员。90 是我设置的一个任意界值。如果你想在 75% 时收到警告，请将界值改为 75。

### 资源

使该脚本具有可执行权限并运行它：

```
chmod +x path_to/script
./path_to/script
```

输出示例：

```
Directory /dev/hda1 现在占用率为 95%
```

## 值得考虑的其他语言

Python 和 Tcl/Tk 都有大量的支持，且各有优势。你应该考虑的两个是 Python 和 Tcl/Tk。

### 资源

**书籍**

* *Programming Perl*, Larry Wall (Cambridge, MA: O'Reilly and Associates, 2000)

**网站**

* BASH Programming HOWTO: `http://www.linuxdoc.org/HOWTO/Bash-Prog-HOWTO`
* CPAN (Comprehensive Perl Archive Network): `http://www.cpan.org/`
* Perl 主页（至少一个）: `http://www.perl.com/`
* Tcl SourceForge 项目: `http://tcl.sourceforge.net/`

# 第 15 章 通过自动化简化管理

## 建设性的懒惰

多年来一直开玩笑说系统管理员是出名的懒人。他们会加班工作到深夜，唯一的目的是为了将某个过程自动化，以便以后再也不用做。这正是我一直以来的系统管理员风格（这意味着我通过不断寻找不用工作的方法为我的懒惰买单）。我并不是这么想的。Perl 大师 Larry Wall 声称懒惰是程序员的三大美德之一。他说“程序员”。

为了支持这一关于懒惰美德的说法，我最近在一个流行的互联网搜索引擎上搜索了“laziness”、“system”和“administrator”这些词，得到了超过 3500 条结果。罗伯特·A·海因莱因写过一个关于懒到不会失败的故事。事实上，他的一位角色拉扎拉斯·隆（出自《时间足够》）声称：“进步是由懒惰的人寻找更简单的方法来实现的。”

## cron: 掌控 Linux 时钟

运行在你系统上的基本进程之一是一个名为 `cron` 的实用程序。实际程序被称为 `crond`（cron 守护进程）。`cron` 是一个执行大量任务的小程序。每个 UNIX 系统都有某种形式的 `cron` 作为系统调度器的一部分。在你的 Red Hat Linux 系统（以及其他发行版）上，`cron` 实际上是由 Paul Vixie 编写的 "Vixie cron"。Slack 的 cron 则有些不同——它安装了 Matthew Dillon 的 cron 包。

那么，你问，它将如何改变你的生活？它能为你做什么？`cron` 允许你在名为 `crontab` 的文件中指定的时间和日期运行重复性任务。以用户 ID 和权限运行的 crontab 条目以用户名存储（这是它们来自 `/etc/passwd` 文件的名称）。例如，root 的 crontab 称为 "root"。每分钟，`cron` 都会唤醒并检查是否有任何任务需要运行。这些任务可以是关于任何你可以放入脚本文件中的内容：执行备份、清理日志文件、删除核心文件、通过 `fortune` 程序向你发送每日 Linux 格言等。此版本的 `cron` 还会检查它监控的任何目录和文件是否发生了变化。如果是，它将重新读取这些文件并将其加入待办列表。

crontab 的位置因系统而略有不同。系统中还存在 cron 任务，或多或少仅供系统使用的。查看你的 `/var/spool/cron` 目录。在你的 Red Hat 系统上，各种用户的 crontab 都在这里。在 Debian 系统上，有一个进一步子目录 `crontabs`，用户的 crontab 位于其中。

`/etc/crontab` 文件中 `cron.daily`、`cron.weekly` 等其他命令的执行时间。我的看起来像是：

```bash
SHELL=/bin/bash
PATH=/bin:/bin:/usr/bin
MAILTO=root
HOME=
# run-parts
01 * * * * root run-parts /etc/cron.hourly
02 4 * * * root run-parts /etc/cron.daily
22 4 * * 0 root run-parts /etc/cron.weekly
42 4 1 * * root run-parts /etc/cron.monthly
```
