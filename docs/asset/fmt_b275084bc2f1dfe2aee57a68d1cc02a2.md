
### last 和 next

你可以使用 `last` 提前退出循环，类似于 `break` 命令。你可以使用 `next` 跳过循环的剩余部分，类似于 `continue` 命令。

## 正则表达式

Perl 最大的优势在于文本和文件处理，这是通过使用正则表达式（regex）库实现的。正则表达式与 Shell 的通配符扩展功能（见第 15 章）大不同，允许高效方便地完成复杂的模式匹配和替换。

例如，以下代码将文本中所有的字符串 bob 或 mary 替换为 `fred`：

```
$string = s/bob|mary/gi;
```

在不涉及过多细节的情况下，表 27.7 解释了上述行的含义。

### TABLE 27.7 $string ~ s/bob|mary/gi; 的解释

| 元素 | 解释 |
| --- | --- |
| `$string ~= ` | 对变量 `$string` 中的文本执行此模式匹配 |
| `s` | 替换。 |
| `/` | 开始要匹配的文本。 |
| `bob|mary` | 匹配 bob 或 mary。请记住它寻找的是文本 mary 而不是单词 mary；也就是说，它也会匹配 maryland 中的 mary。 |
| `/` | 结束要匹配文本；开始替换文本。 |
| `fred` | 将匹配到的内容替换为文本 fred。 |
| `/` | 结束替换文本。 |
| `g` | 此替换全局进行；也就是说，在字符串中匹配到的任何地方进行替换（任意多次）。 |
| `i` | 搜索不区分大小写。它可以匹配 bob、Bob 或 bob。 |
| `;` | 表示代码行的结束。 |

## 列表 27.4 使用反引号访问 Shell

```perl
$curr_dir = `pwd`;
@listing = `ls -al`;
print "Listing for $curr_dir\n";
foreach ($file (@listing) {
    print "$file";
}
```

> 注意
> 符号 `` ` `` 使用的是键盘上 Tab 键上方的反引号（在大多数键盘上都是如此），而不是单引号。

你也可以使用 `Shell` 模块来访问 shell。`Shell` 是 Perl 自带的标准模块之一；它允许创建和使用类似 shell 的命令行。查看下面的代码示例：

```perl
use Shell qw(cp);
cp ("/home/httpd/logs/access.log", "/tmp/httpd.log");
```

这段代码看起来几乎是直接将命令行函数导入了 Perl 中。虽然事实并非如此，但你可以假装这段代码类似于命令行，并在程序中使用这种方法。

访问 shell 的第三种方法是使用 `system` 函数调用：

```perl
$rc = 0xffff & system('cp /home/httpd/logs/access.log /tmp/httpd.log');
if ($rc == 0) {
    print "system cp succeeded \n";
} else {
    print "system cp failed $rc\n";
}
```

该调用还可以配合 `or die` 子句使用：
`system('cp /home/httpd/logs/access.log /tmp/httpd.log') == 0 or die "system cp failed: $?";`

然而，你无法捕通过 `system` 函数执行的命令输出。

## 模块与 CPAN

Perl 社区（以及 Linux 社区）的一个巨大优势是它是一个开源社区。这种社区支持通过全面 Perl 归档网络（CPAN）体现在 Perl，CPAN 是一个 Perl 代码仓库的镜像网络。

CPAN 的大部分内容由模块组成，这些是可重用的代码块，可以执行很有用的功能，类似于包含 C 程序员所需函数的软件库。这些模块有助于在构建 Perl 程序时加速开发，并让 Perl 极客在构建自行车时无需重复发明轮子。

Perl 安装时带有一系列标准模块。这些模块包含了你最初使用 Perl 时需要的大部分功能。如果你需要使用 Ubuntu 未安装的模块，请使用 `CPAN` 命令（它是标准模块之一）将其他模块下载并安装到你的系统中。在 http://www.perl.com/CPAN，你会找到 CPAN 多路分发器（Multiplex Dispatcher），它会尝试引导你访问距离最近的 CPAN 站点。

输入以下内容将进入一个交互式 shell，让你访问 CPAN。你可以在提示符处输入 `help` 获取有关如何使用 CPAN 程序的更多信息。

```bash
$ perl -MCPAN -e shell
```

从 CPAN 安装模块（或编写自己的模块）后，你可以通过以下函数将该模块加载到内存中并使用：

```perl
use Time::CTime;
```

在此示例中，`use` 会在变量 `$INC` 列出的目录中查找，`use` 查找名为 `Time` 的目录，其中包含一个 `CTime.pm` 文件，该文件反过来假设包含一个名为 `Time::CTime` 的包。每个模块的发行版都应该包含使用该模块的文档。

所有标准 Perl 模块（安装 Perl 时自带的模块）的列表请参见 Perl 文档中的 `permodlib`。你可以通过在命令行提示符输入 `perldoc permodlib` 来阅读此文档。

## 代码示例

接下来的章节包含你可能想用 Perl 执行的一些操作。

## 发送邮件

你可以通过多种方式让 Perl 执行 `sendmail` 命令。你常用的方法之一是打开到 `sendmail` 命令的管道并向其发送数据（如 27.5 所示）。另一种方法是使用 `Mail::Sendmail` 模块（通过 CPAN 获取），它使用 socket 连接发送邮件（如 27.6 所示）。后者更快，因为不需要启动外部进程。注意，为了让 27.5 中的 Perl 程序工作，你的系统上必须运行着 `sendmail`。

## 第 27 章 使用 Perl

### 列表 27.5 使用 Sendmail 发送邮件

```perl
#!/usr/bin/perl
open (MAIL, '/usr/sbin/sendmail -t'); # 使用 -t 防止用户干扰
print MAIL<<EndMail;
To: dpitts@mk.net
From: rbowen@mk.net
Subject: Email notification
David,
Sending email from Perl is easy!
Rich
EndMail
close MAIL;
```

> 注意，邮件地址中的 `@` 符号必须经过转义，否则 Perl 会尝试将其评估为名称数组。也就是说，`dpitts@mk.net` 会导致问题，你需要使用 `dpitts\@mk.net`。

用于打印邮件消息的语法被称为“在此处文档”（here document）。其语法如下：

```perl
print <<EndText;
...
EndText
```

`EndText` 的值必须与块的开头和结尾完全一致，包括任何空白字符。

### 列表 27.6 使用 Mail::Sendmail 模块发送邮件

```perl
#!/usr/bin/perl
use Mail::Sendmail;
%mail = (
    'To' => 'dpitts@mk.net',
    'From' => 'rbowen@mk.net',
    'Subject' => 'Email notification',
    'Message' => 'Sending email from Perl is easy!',
);
sendmail(%mail);
```

# 列表 27.8 延续

```perl
# import the NNTP module
use Net::NNTP;
SNTPost = 'news';
# 尝试连接到远程主机；
# 如果失败则打印错误信息
sntp = Net::NNTP->new($NNTPost)
or die "cannot connect $NNTPost: $!"
# sntp->debug(1);
sntp->post()
or die "could not post article: $@"
# 发送 post 的头部
sntp->datasend("Groups: news.announce\n")
sntp->datasend("Subject: FAQ Frequently Asked Questions\n")
sntp->datasend("From: ADMIN <root@rcbowen.com>\n")
sntp->datasend("\n")
# 对于 @post 数组中的每一行，发送它
for (@post)
{
    sntp->datasend($_);
}
# 结束循环
```
