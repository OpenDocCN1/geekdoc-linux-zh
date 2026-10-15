

## 表 23.7 $string =~ s/bob|mary/fred/gi; 的说明

| 元素 | 说明 |
|---|---|
| fred | 用文本 fred 替换匹配到的内容。 |
| / | 结束替换文本。 |
| g | 全局执行此替换；也就是说，在字符串中 wherever 你匹配到它（以及任意次数）都替换匹配文本。 |
| i | 搜索文本不区分大小写。它匹配 bob、Bob 或 bOB。 |
| ; | 表示代码行的结束。 |

如果你对细节感兴趣，可以使用手册中的 regex (?) 部分获取更多信息。

虽然用一个字符串替换另一个字符串看起来可能是一项相当琐碎的任务，但在另一种语言（例如 C）中执行相同操作所需的代码相当令人生畏，除非得到外部库中额外子程序的支持。

## 访问 Shell

Perl 可以通过 `` 语法为你执行任何你通常通过向 shell 输入命令来执行的进程。例如，清单 23.4 中的代码打印目录列表。

### 清单 23.4 使用反引号访问 Shell

```
$curr_dir = `pwd`;
@listing = `ls -al`;
print "Listing for $curr_dir\n";
foreach $file (@listing) {
    print "$file";
}
```

> 注意
> `` 记法使用的是 Tab 键上方（大多数键盘上）的反引号，而不是单引号。

你也可以使用 Shell 模块来访问 shell。Shell 是随 Perl 提供的标准模块之一；它允许创建和使用类似 shell 的命令行。看下面的代码示例：

```
use Shell qw(cp);
```

```
cp ("/home/httpd/logs/access.log", "/tmp/httpd.log");
```

这段代码几乎看起来像是直接将命令行函数导入到 Perl 中。虽然实际上并非如此，但你可以假装代码与命令行相似，并在你的 Perl 程序中使用这种方法。

访问 shell 的第三种方法是通过 system 函数调用：

```
$rc = 0xffff & system('cp /home/httpd/logs/access.log /tmp/httpd.log');
if ($rc == 0) {
    print "system cp succeeded \n";
} else {
    print "system cp failed $rc\n";
}
```

调用也可以与 or die 子句一起使用：

```
system('cp /home/httpd/logs/access.log /tmp/httpd.log') == 0
    or die "system cp failed: $?"
```

然而，你无法捕获通过 system 函数执行的命令的输出。

## 模块和 CPAN

Perl 社区（以及 Linux 社区）的一大优势是它是一个开源社区。这种社区支持通过 Comprehensive Perl Archive Network（CPAN）表达，CPAN 是一个 Perl 代码存储库的镜像网络。

CPAN 的大部分内容由模块组成，模块是可以重复使用的代码块，做着有用的事情，类似于包含 C 程序函数的软件库。这些模块有助于在构建 Perl 程序时加快开发速度，并使 Perl 黑客在构建自行车时不必反复重新发明轮子。

Perl 附带了一套已安装的标准模块。这些模块应该包含你最初使用 Perl 时所需的大部分功能。如果你需要使用 Ubuntu 未安装的模块，请使用 CPAN 模块（它是标准模块之一）将其他模块下载并安装到你的系统上。在 http://www.perl.com/CPAN，你会找到 CPAN Multiplex Dispatcher，它会尝试将你引导到离你最近的 CPAN 站点。

输入以下命令将使你进入一个交互式 shell，可通过该 shell 访问 CPAN。你可以在提示符下输入 help 以获取有关如何使用 CPAN 程序的更多信息：

```
$ perl -MCPAN -e shell
```

从 CPAN 安装模块后（或编写自己的模块），你可以将该模块加载到内存中以用作函数：

`use Time::CTime;`

use 会在变量 @INC 列出的目录中查找模块。在此示例中，use 查找名为 Time 的目录，其中包含名为 CTime.pm 的文件，该文件又假定包含名为 Time::CTime 的包。每个模块的发行版都应包含有关如何使用该模块的文档。

要列出所有标准 Perl 模块（即随 Perl 安装时附带的模块），请参阅 Perl 文档中的 perldoc。你可以通过在命令提示符下输入 `perldoc perldoc` 来阅读此文档。

## 代码示例

以下各节包含一些你可能想用 Perl 完成的事项的示例。

## 发送邮件

你可以通过几种方式让 Perl 发送电子邮件。一种常见的方法是打开到 sendmail 命令的管道并向其发送数据（见清单 23.5）。另一种方法是使用 Mail::Sendmail 模块（可通过 CPAN 获得），它使用套接字连接直接发送邮件（见清单 23.6）。后一种方法更快，因为它不必启动外部进程。请注意，sendmail 必须在你的系统上运行，清单 23.5 中的 Perl 程序才能工作。

```
```perl
#!/usr/bin/perl
open MAIL, '| /usr/sbin/sendmail -t'; # Use -t to protect from users
print MAIL <<EndMail;
To: dpatts
From: rbowen
Subject: Email notification

David,
Sending email from Perl is easy!
Rich
.
EndMail
close MAIL;
```
```

