
Perl 社区（以及 Linux 社区）的一个巨大优势是它是开源的。Perl 附带一组标准模块。这些模块包含了你最初需要的许多功能。大部分 CPAN 由模块组成，这些模块是可重用的代码块，类似于软件库。这些模块帮助程序员避免重复造轮子。

如果你需要使用未安装的模块，使用 CPAN（它是标准模块之一）来下载并安装其他模块到你的系统。在 http://cpan.org，你可以找到 CPAN。输入以下命令会进入一个交互式 shell，你可以在提示符处输入 help 获取关于 CPAN 的信息：

```bash
matthew@seymour~$ perl -MCPAN -e
```

从 CPAN 安装模块（或编写自己的模块）后，你可以使用 `use` 函数将该模块加载到内存中：

```perl
use Time;
```

`use` 在名为 `Time` 的目录中查找。关于所有标准模块（安装它时 Perl 附带的模块），请参 Perl 文档中的 `perlmod`。你可以通过在提示符输入 `perldoc perlmod` 来阅读此文档。

# 代码示例

以下章节包含了一些你可能用 Perl 执行的操作示例。

## 发送邮件

你可以通过几种方式让 Perl 发送电子邮件。你经常看到的方法是打开到 `sendmail` 命令的管道并向其发送数据（如列表 46.5 所示）。另一种方法是使用 `Mail::Sendmail` 模块（通过 CPAN 获取），它使用 socket 连接发送邮件（如列表 46.6 所示）。后者更快，因为它不需要启动外部进程。注意，为了让列表 46.5 中的程序工作，系统中必须运行 sendmail。

### 列表 46.5 使用 Sendmail 发送邮件

```perl
#!/usr/bin/perl
open (MAIL, "|usr/sbin/sendmail -t"); # 使用 -t 保护用户
print MAIL <<EndMail;
To: you
From: me
Subject: A Sample Email
Sending email from Perl is easy!
EndMail
close MAIL;
```

**注意**

电子邮件地址中的 `@` 符号必须转义，否则 Perl 会尝试评估该数组。也就是说，`user@mk.net` 会导致问题，你需要使用：

```perl
user@@mk.net
```

用于打印邮件消息的语法被称为此处文档（here document）。语法如下：

```perl
print <<EndText;
....
EndText
```

`EndText` 的值在块的开头和结尾必须相同，包括任何空格。

## 列表 46.6 使用 Mail::Sendmail 模块发送邮件

```perl
#!/usr/bin/perl
use Mail::Sendmail;

%mail = ( To => "you@there.com",
    From => "me@here.com",
    Subject => "A Sample Email",
    Message => "This is a very short message"
);

sendmail(%mail) or die $Mail::Sendmail::error;

print "OK. Log says:\n", $Mail::Sendmail::log;

use Mail::Sendmail;
```

Perl 忽略表中最后一个元素后的逗号。把它留在那里很方便；这样如果你想向哈表中添加项，就不需要添加逗号。这纯粹是一个风格决定。

# 使用 PERL 安装 CPAN 模块

你可以使用 `-M` 和 `-e` 命令通过 Perl 交互式地从 CPAN 存档下载并安装 Perl 模块。使用如下 Perl 命令启动过程：

```bash
perl -MCPAN -e
```

当你按下回车时，你会看到一些信息，并被要求选择初始的自动或手动配置，这在任何下载或安装发生之前都是必须的。输入 no 并按回车让 Perl 自动配置下载和安装过程；或者如果你愿意，只需按回车手动配置下载和安装。如果你使用手动配置，你必须回答关于路径、缓存、终端设置、程序位置等的问题。设置保存在当前目录下的名为 `.cpan` 的目录中。

完成后，你会看到 CPAN 提示符：

```bash
cpan>
```

要让 Perl 检查你的系统然后下载并安装大量模块，使用 `install` 关键字，在提示符处指定 `Bundle`，然后按回车，如下：

```bash
cpan> install Bundle::CPAN
```

下载所需的模块（使用列表 46.6 中的示例），使用 `get` 关键字，如下：

```bash
cpan> get Mail::Sendmail
```

模块的源代码被下载到 `.cpan` 目录中。然后你可以使用 `install` 关键字来构建并安装该模块，如下：

```perl
cpan> install Mail::Sendmail
```

获取、构建和安装模块的整个过程也可以通过 Perl 的 `-e` 选项在命令行中完成，如下：

```bash
# perl -MCPAN -e "install Mail::Sendmail"
```

请注意，列表 46.6 中的 `@` 符号在单引号（' ' '）内不需要转义。Perl 不会在单引号内进行字符串插值（评估变量），但在双引号和“在此处的字符串”（here strings，类似于 shell 的 `<<` 操作）中会进行插值。

## 清理日志

许多程序维护着各种类型的日志。通常，日志中的许多信息是冗余的或毫无用的。列表 46.7 所示的程序会删除文件中包含特定单词或短语的所有行，这样就可以清除掉你认为不重要的行。例如，你可能想要删除 Apache 错误日志中所有源自你测试客户端机器的行，因为你清楚这些错误信息是在测试期间产生的。

### 列表 46.7 清理日志文件

```perl
#!/usr/bin/perl
# 使用此程序要小心！
# 这将删除所有包含给定单词的行
# Usage: remove <word> <file>
$word=@ARGV[0];
$file=@ARGV[1];
if ($file) {
  # 打开文件读取
  open (FILE, "$file") or die "Could not open file: $!";      @lines=<FILE>;
  close FILE;
  # 打开文件写入
  open (FILE, ">$file") or die "Could not open file for writing: $!";
  for (@lines) {
    print FILE unless /$word/;
  } # End for
  close FILE;
} else {
  print "Usage: remove <word> <file>\n";
} # End if...else
```

列表 46.7 中的代码包含了一些惯用的 Perl 表达式以保持其简洁。它通过使用 `<FILE>` 符号将文件读到数组中；然后，除非行匹配命令行上指定的模式，否则将它们重新写回文件。

`die` 函数会在 `open` 语句失败时终止程序操作并显示错误消息。正如本章前面提到的，错误消息中的 `$!` 是操作系统返回的错误消息。它可能是类似于“找不到文件”（file not found）或“权限被拒绝”（permission denied）。

## 发布到 Usenet

如果你工作的部分内容需要定期发布到 Usenet——例如一个 FAQ 列表——下面的 Perl 程序可以为你自动完成这一过程。在列表 46.8 中，发布的文本从文本文件中读取，但你的输入可以来自任何地方。

列表 46.8 所示的程序使用了 `Net::NNTP` 模块，它是 Perl 分发版的标准部分。你可以通过在命令行输入 `perldoc Net::NNTP` 来找到关于 `Net::NNTP` 模块的更多文档。

### 列表 46.8 向 Usenet 发布文章
