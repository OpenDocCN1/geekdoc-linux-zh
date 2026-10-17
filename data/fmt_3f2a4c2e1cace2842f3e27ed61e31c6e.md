
假设你编写了一篇关于物质世界财务周期的电子周刊，并通过电子邮件分发。为了简化涉及金融市场的法律后果，你特意选择在周五下午 5:00 发送。现在是周三，你已完成分析，并且几乎已经收拾好今晚开始的度假行装。你如何对得起你的订阅者？只需要三行 `at` 脚本：

```
# at 17:00 Friday << COMMAND
mail -s "This week's CYCLES report." mailing_list
 < analysis.already_written
COMMAND
```

这会将 `mail` 命令调度以供稍后处理。你可以注销你的会话，你的 `Linux` 主机仍会在周五 17:00 发送邮件，正如你指示的那样。事实上，你甚至可以在执行 `at` 命令时关闭机器，只要它在时间内重新启动，你调度的任务仍会按你规定的计划启动。

## 其他机制：Expect、Perl 等

你准备好超越 UNIX 外壳的限制了吗？几种替代技术是免费的、易于安装、易于学习，并且比 shell 更强大——即具有更丰富的功能及更结构化的语法——。一些例子将暗示它们所能提供的东西。

### Expect

`Expect` 由 Don Libes 开发，是一种与许多不同程序配合工作的脚本语言，可用作自动化的强大软件工具。为什么？`Expect` 自动化交互，特别是那些涉及终端控制和时间延迟的交互，这是其他工具未尝试过的。许多命令行应用程序因其涉及密码输入且拒绝为此目的接受标准输入重定向而闻名，因此被认为不可脚本化。然而，这对 `expect` 命令来说不是问题。在 Red Hat Linux 下，`expect` 安装在 `/usr/bin` 目录下，你可以在其手册页中找到文档。

创建一个名为 `hold` 的脚本，其内容如清单 26.4 所示。

**清单 26.4** `hold` —— 用 `Expect` 编写的“保持连接”

```expect
#!/usr/bin/expect
# Usage: "hold HOST USER PASS".
# Action: login to node HOST as USER. Offer a shell prompt for
# normal usage, and also print to the screen the word HELD
# every five seconds, to exercise the connection periodically.
# This is useful for testing and using WANS with short time-outs.
# You can walk away from the keyboard, and never lose your
# connection through a time-out.
# WARNING: the security hazard of passing a password through the
# command line makes this example only illustrative. Modify to
# a particular security situation as appropriate.
set hostname [lindex $argv 0]
set username [lindex $argv 1]
set password [lindex $argv 2]
# There's a trouble if Susername's prompt is not set to "..." .
# A more sophisticated manager knows how to look for different
# prompts on different hosts.
set prompt_sequence ") "
spawn telnet $hostname
expect "login: "
send "$username\r"
expect "Password:"
send "$password\r"
# Some hosts don't inquire about TERM. That's another
# complication to consider before widespread use
# of this application is practical.
# Note use of global [gl] pattern matching to parse "*"
# as a wildcard.
expect -gl "TERM = (*))"
send "\r"
expect $prompt_sequence
send "sh -c 'while true; do echo HELD; sleep 5; done'\r"
interact
```

此脚本启动一个 `telnet` 会话，然后每五秒发送字符串 `"HELD"` 来保持连接打开。我使用几条带有短超时的电话线，以检查自付费用。我每天都会使用清单 26.4 中脚本的一个变体，因为我经常需要保持其中一条连接打开。

`Expect` 是 `Tcl` 的扩展，因此它完全可以通过 `Tcl` 功能进行编程。关于 `Tcl` 和 `Tk` 的更多信息，请访问其作者 John Ousterhout 博士的页面：[http://www.sun.com/960710/cover/ousterhout.html](http://www.sun.com/960710/cover/ousterhout.html)。关于 `Expect` 的更多信息，请访问 [http://expect.nist.gov](http://expect.nist.gov)。

> **提示**
>
> 你还会发现 Red Hat Linux 附带了 `autoexpect` 命令。该命令监视控制台的交互式会话，然后创建一个可执行程序来执行控制台会话。关于如何使用 `autoexpect` 来自动化 FTP 会话的示例，请参阅第 11 章。

### Perl

许多人认为 `Perl` 是 Red Hat Linux 中最流行的脚本语言，仅次于 shell。其强大功能和简洁性在自动化场景中尤为有价值。

> **注意**
>
> 如需了解更多关于 `Perl` 的信息或获取最新版本，请访问 [http://www.perl.com](http://www.perl.com) 或 [http://www.perl.org](http://www.perl.org)。

例如，假设 `/usr/local/bin/modified_directories.pl` 包含以下代码：

```perl
#!/usr/bin/perl
# Usage: modified_directories.pl DIR1 DIR2 ... DIRn
# Output: a list of all directories in the file systems under
#    DIR1 ... DIRn, collectively. They appear, sorted by the
#    interval since their last activity, that is, since a file
#    within them was last created, deleted, or renamed.
# Randal Schwartz wrote a related program from which this is
# descended.
use File::Find;
$directory_list = @ARGV;
# "-M" abbreviates "time since last modification", while
#    "-d" "... is a directory." 

find ( sub { 
   $modification_lapse{$File::Find::name} = -M if -d $File::Find::name, 
   @directory_list );

for ( sort { 
   $modification_lapse{$a} <=> $modification_lapse{$b} } keys
$modification_lapse) {
    # Tabulate the results in nice columns.
    printf "%5d: %s\n", $modification_lapse[$_], $_;
}
```

还假设你在 `crontab` 中添加了如下条目：

```
20 2 * * * /usr/local/bin/modified_directories.pl /
```

在这种情况下，每天早上你都会收到一封电子邮件报告，说明主机上每个目录上次修改的日期。这既有助于发现安全问题（当只读目录被修改时，它们会意外地出现在列表顶部），也有助于识别文件系统中休眠的域（位于列表底部），这些域可以被释放出来用于更好的用途。

## 其他工具

许多其他通用脚本语言都能有效地实现操作自动化。除了 `Perl` 和 `Tcl` 之外，`Python` 由于其可移植性和可扩展性等原因，值得最受关注。
