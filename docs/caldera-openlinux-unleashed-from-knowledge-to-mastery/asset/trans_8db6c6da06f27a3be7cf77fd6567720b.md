
# 代码示例

在过去几年里，许多人形成了一种观念，认为 Perl 是一种 CGI 语言，好像它除了 CGI 之外毫无用处。事实恰恰相反。你可以将 Perl 用于系统管理的方方面面，并作为你计划在新 Linux 系统上运行的任何应用程序的基础构件。

以下章节提供了一些你可能想用 Perl 完成的任务示例。Perl 足够通用，你可以让它完成几乎任何事情。

## 发送邮件

让 Perl 发送邮件有几种方法。一种常见的方法是打开一个通往 *sendmail* 的管道并向其发送数据（如列表 32.5 所示）。另一种方法使用 Mail::Sendmail 模块，它直接使用套接字连接来发送邮件（如列表 32.6 所示）。后一种方法更快，因为它不需要启动外部进程。

**列表 32.5 使用 sendmail 发送邮件**

```perl
open (MAIL, "| /usr/sbin/sendmail -t"); # 使用 -t 以防止用户滥用
print MAIL
To: dpitts@mkm.net
From: rbowen@mkm.net
Subject: Email notification

David,
  Sending email from Perl is easy!
Rich
.
EndMail
close MAIL;
```

**注意**

注意电子邮件地址中的 @ 符号需要转义，以便 Perl 不会尝试评估该名称的数组。

用于打印邮件消息的语法被称为 *heredoc*。语法如下：

```perl
print <<EndText;
.....
EndText
```

EndText 值在块的开头和结尾必须完全相同，包括任何空白字符。

**列表 32.6 使用 Mail::Sendmail 模块发送邮件**

```perl
use Mail::Sendmail;
%mail = ('To' => 'dpitts@mik.net',
         'From' => 'rbowen@mik.net',
         'Subject' => 'Email notification',
         'Message' => 'Sending email from Perl is easy!');
sendmail(%mail);
```

Perl 会忽略哈希中最后一个元素后的逗号。保留它很方便；如果你想向哈希添加项目，不需要添加逗号。这纯粹是一种风格选择。

另外注意，在单引号 (' ') 内的 @ 符号不需要转义。Perl 在单引号内不 *插值*（评估变量），但在双引号和 heredoc 内会。

## 清除日志

许多程序维护各种日志。通常，日志中的许多信息是冗余的或无用的。列表 32.7 中显示的程序删除文件中包含特定单词或短语的所有行，这样你就可以清除那些已知不重要的行。例如，你可能希望删除 Apache 错误日志中源自你的测试客户端机器的所有行，因为你知道这些错误消息是在测试过程中产生的。

**列表 32.7 清除日志文件**

```perl
#!/usr/bin/perl
#    小心使用此程序！！
#       这将删除包含给定单词的所有行
#       用法： remove <word> <file>
$word=$ARGV[0];
$file=$ARGV[1];
if ($file) {
    # 打开文件以读取
    open (FILE, "$file") or die "Could not open file: $!";    
    @lines=<FILE>;
    close FILE;
    # 打开文件以写入
    open (FILE, ">$file") or die "Could not open file for writing: $!";
    for (@lines) {
        print FILE unless /$word/;
    } # End for
    close FILE;
} else {
    print "Usage:  remove <word> <file>\n";
} # End if...else
```

该代码使用了一些惯用的 Perl 表达式使代码简洁。它使用 `<FILE>` 符号将文件读取到数组中；然后除非行匹配命令行给定的模式，否则它将行写回文件。

**die** 函数在 open 语句失败时终止程序操作并显示错误消息。错误消息中的 `$!`，如特殊变量部分所述，是操作系统返回的错误消息。它可能是类似于“文件未找到”或“权限被拒绝”的内容。

## 发布到 Usenet

如果你的工作要求定期向 Usenet 发布内容——例如 FAQ 列表——列表 32.8 中显示的程序可以为你自动化这个过程。在示例代码中，发布的文本是从文本文件读取的，但你的输入可以来自任何地方。

列表 32.8 中显示的程序使用 **Net::NNTP** 模块，它是 Perl 发行版的标准组成部分。你可以通过在命令行键入 **perldoc Net::NNTP** 找到关于 **Net::NNTP** 模块的更多文档。

**列表 32.8** 向 Usenet 发布文章

```perl
#!/usr/bin/perl
open (POST, "post.file");
@post = <POST>;
close POST;
use Net::NNTP;
$NNTPHost = 'news';
$nntp = Net::NNTP->new($NNTPHost)
       or die "Can't contact $NNTPHost: $!";
# $nntp->debug(1);
$nntp->post()
       or die "Could not post article: $!";
$nntp->datasend("Newsgroups: news.announce\n");
$nntp->datasend("Subject: FAQ - Frequently Asked Questions\n");
$nntp->datasend("From: ADMIN <root@rcbowen.com>\n");
$nntp->datasend("\n\n");
for (@post) {
    $nntp->datasend($_);
} # End for
$nntp->quit;
```

## 单行程序

Perl 有一个不太好的名声，认为它难以阅读。事实是，你可以在任何语言中编写难以阅读的代码。Perl 允许用多种方法做某事，这自然而然地导致人们试图寻找最晦涩的方法来做事情。

Perl 擅长的一个领域是单行程序。人们费尽心思将任务简化为一行 Perl 代码。以下是一些可能使你的生活更轻松的单行程序示例。

**提示**

仅仅因为你做某事并不是做某事的特别好的理由。我会经常写稍微长一点的代码，即使某件事可以只用一行代码完成，只是为了可读性——既是为了我自己，也是为了以后阅读代码的人。回头去看一段为了效率或仅仅因为能做到而将某事简化为一行的代码，并花费 30 分钟试图弄清楚它做什么，是非常令人恼火的。

## 施瓦茨变换

以 Randal Schwartz 命名，*施瓦茨变换* 是一种按不明显的方式排序数组的方法。`sort` 函数按字母顺序排序数组；这很清楚。如果你想按第三个单词对字符串数组按字母顺序排序怎么办？也许你想要一些更有用的东西，比如按文件大小对文件列表进行排序？施瓦茨变换创建一个新列表，该列表包含你要用于排序的信息，并引用原始列表。然后你排序新列表并使用它来确定原始列表应有的顺序。这是一个简单的示例，按长度对字符串列表进行排序：

```perl
sorted_by_length =
    map { $_->[0] }                # 提取原始列表
    sort { $a->[1] <=> $b->[1] }    # 按转换后的值排序
    map { [$_, length($_)] }
    @list;
```

由于每个运算符都立即作用于其右侧的输入，从右到左阅读（或按照此处写的从上到下）会很有帮助。

首先作用于列表的是 map 运算符。它将列表转换为哈希，其中键是列表元素，值是每个元素的长度。这就是你放置代码以进行你想要的排序转换的地方。

下一个运算符是 *sort* 函数，它按值对列表进行排序。

最后，通过提取键，哈希被转换回数组。数组现在处于所需顺序。

## 命令行处理

Perl 在解析各种程序的输出方面非常出色。这是许多人使用 **awk** 和 **sed** 等工具完成的任务。Perl 为你提供了更大的词汇量来执行这些任务。以下示例非常简单，但它说明了你可能如何使用 Perl 切割某些输出并对其进行处理。在示例中，Perl 用于仅列出大于 10 KB 的文件。

```perl
ls -la | perl -nae 'print "$F[8] $F[4]\n" if $F[4] > 10000;'
```

**-n** 开关表示我希望 Perl 代码对输出的每一行运行一次。**-a** 开关自动将输出拆分到 `@F` 数组中。**-e** 开关表示 Perl 代码将跟随在命令行中。（见本章前面提到的“开关”。）

# Perl 相关工具

许多工具与 Perl 相关或包含在 Perl 发行版中。其中最常见的是：

- **perldoc**：显示 Perl 文档
- **pod2html**：将 Perl 文档转换为 HTML 格式
- **pod2man**：将 Perl 文档转换为 man (`nroff`/`troff`) 格式
- **a2p**：将 **awk** 脚本转换为 Perl
- **s2p**：将 **sed** 命令转换为 Perl

# 更多信息

查找更多信息的第一个地方是 Perl 文档和 Linux man 页面。

Perl、其所有文档以及数百万行 Perl 程序都可以在互联网上免费获取。还有许多专门针对 Perl 的 Usenet 新闻组，以及一摞书和一本季刊。

## 书籍

尽管你当地的书店可能有许多 Perl 书籍，但以下书籍被强烈推荐。你还可以查看 *Camel Critiques*（Tom Christiansen；**http://language.perl.com/critiques/index.html**）阅读关于其他可用 Perl 书籍的评论。

