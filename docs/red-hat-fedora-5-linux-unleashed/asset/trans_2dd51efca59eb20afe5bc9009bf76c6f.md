
## 模块和 CPAN

Perl 社区（以及 Linux 社区）的一个巨大优势在于它是一个*开源*社区。这种社区支持通过 CPAN 体现出来，CPAN 是一个 Perl 代码库的镜像网络。

CPAN 的大部分内容由*模块*组成，这些模块是可重用的代码片段，能够执行有用的操作，类似于包含 C 程序员函数的软件库。这些模块在构建 Perl 程序时有助于加快开发速度，并让 Perl 开发者（hackers）避免在“骑自行车”时反复重新发明轮子。

Perl 附带了一套已安装的标准模块。这些模块应包含你最初使用 Perl 所需的大多数功能。如果你需要使用未随 Fedora 安装的模块，请使用 CPAN 模块（它是标准模块之一）在你的系统上下载并安装其他模块。在 `http://www.perl.com/CPAN`，你会找到 CPAN 多路复用调度器，它会尝试引导你访问离你最近的 CPAN 站点。

输入以下命令将进入一个交互 shell，让你可以访问 CPAN。你可以在提示符处输入 **help** 以获取有关如何使用 CPAN 程序的更多信息。

```sh
$ perl -MCPAN -e shell
```

安装从 CPAN 安装的模块（或编写自己的模块）后，你可以使用 `use` 函数将该模块加载到内存中并使用它：

```perl
use Time::CTime;
```

`use` 会在变量 `@INC` 中列出的目录中查找该模块。在此示例中，`use` 查找一个名为 `Time` 的目录，该目录包含一个名为 `CTime.pm` 的文件，该文件被认为包含一个名为 `Time::CTime` 的包。每个模块的分发版都应包含关于使用该模块的文档。

要查看所有标准 Perl 模块（即安装 Perl 时附带的模块）的列表，请参阅 Perl 文档中的 **perlmodlib**。你可以通过在命令提示符处输入 **perldoc perlmodlib** 来阅读此文档。

## 代码示例

以下部分包含了一些你可能想使用 Perl 做的事情的示例。

## 发送邮件

让 Perl 发送邮件有几种方法。你经常看到的一种方法是打开到 sendmail 命令的管道并向其发送数据（如清单 30.5 所示）。另一种方法是使用 Mail::Sendmail 模块（可通过 CPAN 获取），该模块直接使用套接字连接发送邮件（如清单 30.6 所示）。后一种方法更快，因为它不需要启动外部进程。请注意，为了使清单 30.5 中的 Perl 程序能够正常工作，sendmail 必须在你的系统上运行。

### 清单 30.5 使用 Sendmail 发送邮件

```perl
#!/usr/bin/perl
open (MAIL, "| /usr/sbin/sendmail -t"); # Use -t to protect from users
print MAIL <EndMail;
To: dpitts\@mk.net
From: rbsowen\@mk.net

Subject: Email notification

David,
   Sending email from Perl is easy!
Rich
.
EndMail
close MAIL;
```

> **注意**
> 注意，电子邮件地址中的 @ 符号必须转义，以便 Perl 不尝试评估该名称的数组。也就是说，`dpitts@mk.net` 会导致问题，因此你需要使用 `dpitts\@mk.net`。
> 用于打印邮件消息的语法称为 here document（here-document）。语法如下：
>
> ```perl
> print <EndText;
> ...
> EndText
> ```
>
> EndText 的值在块的开始和结束处必须完全相同，包括任何空白字符。

### 清单 30.6 使用 `Mail::Sendmail` 模块发送邮件

```perl
#!/usr/bin/perl
use Mail::Sendmail;
%mail = ( 'To' => 'dpitts@mkm.net',
    'From' => 'rhansen@mkm.net',
    'Subject' => 'Email notification',
    'Message' => 'Sending email from Perl is easy!',
);
sendmail(%mail);
```

Perl 会忽略哈希中最后一个元素后面的逗号。保留它很方便；如果你想向哈希添加项目，就不需要添加逗号。这纯粹是一种风格选择。

## 使用 Perl 安装 CPAN 模块

你可以使用 `-M` 和 `-e` 命令，通过 Perl 交互地从 CPAN 存档下载并安装 Perl 模块。按以下方式使用 Perl 启动该过程：

```sh
# perl -MCPAN -e shell
```

按下*Enter*键后，你将看到一些介绍性信息，并被要求选择初始的自动或手动配置，这是在进行任何下载或安装之前所必需的。输入 *no* 并按下 *Enter*，让 Perl 自动配置下载和安装过程；或者，如果愿意，只需按下 *Enter* 以手动配置下载和安装。如果使用手动配置，你将被询问一系列关于路径、缓存、终端设置、程序位置等问题。设置将保存在当前目录下名为 `.cpan` 的目录中。

完成后，你将看到 CPAN 提示符：

```
cpan>
```

要让 Perl 检查你的系统，然后下载并安装大量模块，请使用 *install* 关键字，在提示符处指定 *Bundle*，然后像这样按下 *Enter*：

```
cpan> install Bundle::CPAN
```

要下载所需的模块（使用清单 30.6 中的示例），请使用 *get* 关键字，如下所示：

```
cpan> get Mail::Sendmail
```

该模块的源代码将下载到 `.cpan` 目录中。然后你可以使用 *install* 关键字来*build*（构建）并安装该模块，如下所示：

```
cpan> install Mail::Sendmail
```

获取、构建和安装模块的整个过程也可以通过使用 Perl 的 `-e` 选项在命令行上完成，如下所示：

```sh
# perl -MCPAN -e "install Mail::Sendmail"
```

也要注意，在单引号（''）内部，@ 符号不需要转义。Perl 不会在单引号内部*interpolate*（插值/评估变量），但在双引号和 here strings（类似于 shell 操作中的 `<<`）内部会这样做。

### 清除日志

许多程序维护各种各样的日志。日志中的许多信息通常是冗余的或无用的。清单 30.7 中显示的程序从文件中删除包含特定单词或短语的所有行，因此你可以清除你知道不重要的行。例如，你可能希望删除 Apache 错误日志中源自你的测试客户端机器的所有行，因为你知道这些错误消息是在测试期间产生的。

#### 清单 30.7 清除日志文件

```perl
#!/usr/bin/perl
# Be careful using this program!
# This will remove all lines that contain a given word
# Usage: remove <word> <file>
$word=@ARGV[0];
$file=@ARGV[1];
if ($file) {
    # Open file for reading
    open (FILE, "$file") or die "Could not open file: $!";
    @lines=<FILE>;
    close FILE;
    # Open file for writing
    open (FILE, ">$file") or die "Could not open file for writing: $!";
    for (@lines) {
        print FILE unless /$word/;
    } # End for
    close FILE;
} else {
    print "Usage: remove <word> <file>\n";
} # End if...else
```

该代码使用了一些惯用的 Perl 表达式以保持简洁。它使用 `<FILE>` 符号将文件读取到数组中；然后，除非行匹配命令行上给出的模式，否则将行写回文件。

*die* 函数在 open 语句失败时终止程序操作并显示错误消息。如特殊变量部分所述，错误消息中的 `$!` 是操作系统返回的错误消息。它可能是类似 `file not found`（文件未找到）或 `permission denied`（权限被拒绝）之类的信息。

## 发布到 Usenet

如果你的工作部分要求定期向 Usenet 发布内容——例如 FAQ 列表——那么以下 Perl 程序可以为你自动化该过程。在示例代码中，发布的文本是从文本文件中读取的，但你的输入可以来自任何地方。

清单 30.8 中显示的程序使用 Net::NNTP 模块，这是 Perl 分发版的标准部分。你可以在命令行输入 `perldoc Net::NNTP` 来查找有关 Net::NNTP 模块的更多文档。

### 清单 30.8 向 Usenet 发布文章

```perl
#!/usr/bin/perl

# load the post data into @post
open (POST, 'post.file');
@post = <POST>;
close POST;
# import the NNTP module
use Net::NNTP;
$NNTPhost = 'news';
# attempt to connect to the remote host;
# print an error message on failure
$nntp = Net::NNTP->new($NNTPhost)
  or die "Cannot contact $NNTPhost: $!";
# $nntp->debug(1);

$nntp->post()
    or die 'Could not post article: $!';
# send the header of the post
$nntp->datasend('Newsgroups: news.announce\n');
$nntp->datasend('Subject: FAQ - Frequently Asked Questions\n');
$nntp->datasend('From: ADMIN <root@arcbowen.com>\n');
$nntp->datasend('\n\n');
# for each line in the post array, send it
for (@post)
{
    $nntp->datasend($_);
} # End for
$nntp->quit;
```

## 单行脚本

Perl 擅长的其中一种形式是单行脚本（one-liner）。人们会花很大的功夫将任务减少到一行 Perl 代码。Perl 有一种不太公平的声誉，即难以阅读。事实是，你可以在任何语言中编写难以阅读的代码。Perl 允许用多种方法完成某事，这自然而然地导致人们试图寻找最晦涩的方式来完成事情。

