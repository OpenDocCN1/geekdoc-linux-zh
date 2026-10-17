
> `foreach` 常被简写为 `for`。

###### `while`

`while` 在特定条件为真时执行语句块：

```
while ($x<10) {

    print "$x\n";

    $x++;

}
```

请记住，条件可以是任何返回真或假值的表达式。例如，它可能是一个函数调用：

```
while (InvalidPassword($user, $password)) {

    print 'You've entered an invalid password. Please try again.\n';

    $password = GetPassword;

}
```

##### `until`

`until` 是 `while` 语句的完全相反。它在特定条件为假时执行语句块——或者更准确地说，直到条件变为真：

```
until (ValidPassword($user, $password)) {

    print 'You've entered an invalid password. Please try again.\n';

    $password = GetPassword;

}
```

##### `last` 和 `next`

你可以使用 `last` 语句强制 Perl 提前结束循环。`last` 类似于 C 语言中的 `break` 命令——循环退出。如果你决定跳过循环的剩余内容而不结束循环本身，可以使用 `next`，它类似于 C 语言中的 `continue` 命令。不幸的是，这些在 `do...while` 循环中不起作用。

##### `do...while` 和 `do...until`

`while` 和 `until` 循环首先评估条件。通过在条件前应用 `do` 块，可以改变这种行为。使用 `do` 块时，条件最后评估，导致块的内容至少执行一次（即使条件为假）。这类似于 C 语言中的 `do...while` (*条件*) 语句。

#### 正则表达式

Perl 最大的优势在于文本和文件操作，这是通过使用正则表达式（`regex`）库来实现的。正则表达式允许高效且轻松地完成复杂的模式匹配和替换。

例如，下面这行代码将文本行中每个出现的字符串 `bob` 或字符串 `mary` 替换为 `fred`：

```
$string =~ s/bob|mary/fred/gi;
```

不深入过多细节，表 32.7 解释了上面这行代码的含义。

| 元素 | 解释 |
| :--- | :--- |
| `$string =~` | 对变量 `$string` 中找到的文本执行此模式匹配。 |
| `s` | 替换。 |
| `/` | 开始要匹配的文本。 |
| `bob\|mary` | 匹配文本 `bob` 或 `mary`。你应该记得它查找的是文本 `mary`，而不是单词 `mary`；也就是说，它也会匹配单词 `maryland` 中的文本 `mary`。 |
| `/` | 结束要匹配的文本；开始要替换的文本。 |
| `fred` | 将匹配到的任何内容替换为文本 `fred`。 |
| `/` | 结束要替换的文本。 |
| `g` | 全局执行此替换；也就是说，在字符串中匹配到匹配文本的任何位置（任意次数）都进行替换。 |
| `i` | 搜索文本不区分大小写。它匹配 `Bob`、`bOb` 或 `bOB`。 |
| `;` | 指示代码行结束。 |

如果你对细节感兴趣，可以使用手册中的 `regex (5)` 章节获取更多信息。

虽然用一个字符串替换另一个字符串可能看起来是个相当琐碎的任务，但在另一种语言（例如 C）中实现相同功能所需的代码却相当令人望而生畏。

#### 访问 Shell

Perl 对管理功能很有用，因为它可以访问 `shell`。这意味着 Perl 可以执行你通常通过向 `shell` 输入命令来执行的任何进程。你使用 `\`\` 语法来实现这一点。例如，列表 32.4 中的以下代码打印目录列表。

##### 列表 32.4 使用反引号访问 Shell

```
$curr_dir = `pwd`;

@listing = `ls -la`;

print "Listing for $curr_dir\n";

foreach $file (@listing) {

    print "$file";

}
```

> **注意**
>
> 反引号 `` ` `` 表示法使用大多数键盘上位于 Tab 键上方的反引号，而不是单引号。

你还可以使用 `Shell` 模块来访问 `shell`。`Shell` 是随 Perl 提供的标准模块之一。它提供了一种对 `shell` 更透明的访问方式。查看以下代码示例：

```
use Shell qw(cp);

cp ('/home/httpd/logs/access.log', "/tmp/httpd.log");
```

这几乎看起来像是直接将命令行函数导入到 Perl 中。虽然实际上并非如此，但你可以假装是这样，并相应地使用它。

访问 `shell` 的第三种方法是通过 `system` 函数调用：

```
$rc = 0xfff & system('cp /home/httpd/logs/access.log /tmp/httpd.log');

if ($rc == 0) {

    print "system cp succeeded \n";

}

else {

    print "system cp failed $rc";

}
```

`system` 函数也可以与 `or` `die` 子句一起使用：

```
system('cp /home/httpd/logs/access.log /tmp/httpd.log') == 0

    or die "system cp failed: $?"
```

然而，你无法捕获通过 `system` 函数执行的命令的输出。

在 `shell` 脚本语言中，访问命令行相当常见，但在更高级的编程语言中则不太常见。

#### 开关（Switches）

Perl 拥有多种命令行选项（*开关*），它们会微妙地改变 Perl 的行为。这些开关可以出现在命令行上，也可以放在 Perl 程序开头的 `#!` 行中。

以下是所有可用的命令行开关。

> **注意**
>
> 多个命令行开关可以堆叠在一起，因此 `-pie` 等同于 `-p -i -e`。

- `-0[octnum]` 将输入记录分隔符（`$/`）指定为八进制数。`$/` 通常是换行符，因此每条记录对应一行。例如，如果你将一个文件读入数组，这将使每个数组元素对应一行。值 `00` 是一个特殊情况，它会导致 Perl 每次读取一段作为一条记录。如果省略 `octnum`，则空字符作为分隔符。
- `-a` 当与 `-n` 或 `-p` 一起使用时，开启自动拆分模式。这意味着输入的每一行都会自动拆分到 `@F` 数组中。
- `-c` 告诉 Perl 对指定的 Perl 程序执行语法检查，但不执行它。这非常有价值，而且给出的错误信息很有用、易读，并告诉你从何处开始查找问题，这在错误信息中是罕见的。
- `-d` 在 Perl 调试器下运行脚本。更多信息请参阅 `perldebug`。

> **注意**
>
> 本章节中多处引用了 Perl 文档。例如，`perldebug`、`perlrun`、`perlmod` 和 `perlmodlib` 都是 Perl 文档中的文档。要查看这些文档，只需在 Shell 提示符下输入 `perldoc perlmodlib`。你还可以在 `http://www.cpan.org/doc/index.html` 或任何 CPAN 网站上在线查看所有 Perl 文档。（CPAN 是 Perl 综合归档网络。详见本章后面的“模块和 CPAN”。）
>
> Perl 文档以 POD（纯普通文档）格式编写，可以使用随 Perl 提供的 `pod2*` 工具将其转换为任何其他格式，如 `tex`、`ASCII` 或 `HTML`。例如，要生成 `Fubar` 模块的 HTML 文档，你会输入 `pod2html Fubar.pm > Fubar.html`。

- `-d:foo` 在安装为 `Devel::foo` 的调试或跟踪模块的控制下运行脚本。例如，`-d:DProf` 使用 `Devel::DProf` 分析器执行脚本。有关 Perl 调试器的更多信息，请参阅 `perldebug`。
- `-Dflags` 设置调试标志。更多细节请参阅 `perlrun`。
- `-e commandline` 指示跟随的内容是 Perl 代码。这允许你直接在命令行输入 Perl 代码，而不是运行文件中的代码。

```
perl -e 'print join " ", keys %ENV;'
```

- `-Fpattern` 指定如果在 `-a` 也生效时的拆分模式。默认情况下是“ ”，`-F` 允许你将它设置为你需要的任何值，如 ‘,’ 或 ‘;’。模式可以用 `//`、`""` 或 `''` 包围。
- `-h` 输入 `perl -h` 会列出所有可用的命令行开关。
- `-i[extension]` 指示文件将被就地编辑。如果提供了扩展名，原始文件将使用该扩展名备份。否则，原始文件将被覆盖。
- `-Idirectory` 由 `-I` 指定的目录会被添加到模块（`@INC`）的搜索路径的前面。
- `-l[octnum]` 启用自动行尾处理，这意味着行尾字符会自动从输入中移除并加回到输出中。如果省略 `octnum`，这只是换行符。
- `-m|-module` 或 `-M|-module` 在运行你的脚本之前执行 `use module`。`-m` 和 `-M` 之间有细微的差别。更多细节请参阅 `perlrun`。
- `-n` 使 Perl 对命令行提供的每个文件循环执行你的脚本。不会打印输出。以下示例来自 `perlrun`，删除所有超过一周的文件：

```
find . -mtime +7 -print | perl -nle 'unlink;'
```

- `-p` 这与 `-n` 类似，只是每一行都会打印出来。
- `-P` 导致脚本在由 Perl 编译之前先通过 C 预处理器运行。
- `-s` 执行一些命令行开关解析，并将开关放入 Perl 脚本中对应的变量中。例如，如果使用 `-fubar` 开关运行以下脚本，它将打印 ‘1’。你的 Perl 代码可能如下：

```
#!/usr/bin/perl -s
print $fubar;
```

当你执行它时，你会输入：

```
myperl -fubar
```

- `-S` 使用 `PATH` 环境变量搜索脚本。
- `-T` 启用*污染*检查。在这种模式下，Perl 假设所有用户输入都是污染的或不安全的，直到程序员告知其不然。这有助于保护你免受试图利用你代码中安全漏洞的人的影响，在编写 CGI 程序时尤为重要。
- `-u` 告诉 Perl 在编译此脚本后转储核心。假设你有大量的时间和耐心，你可以用这个来创建一个可执行文件。
- `-U` 允许你在 Perl 程序中做不安全的事情，例如以超级用户身份运行时注销目录。
- `-v` 打印你的 Perl 可执行文件的版本和补丁级别。

```
$ perl -v
This is perl, version 5.005_03 built for i586-linux
```

版权所有 1987-1999, Larry Wall

Perl 只能根据艺术许可证或 GNU 通用公共许可证的条款进行复制，

这些许可证可以在 Perl 5.0 源代码包中找到。

Perl 的完整文档，包括常见问题列表，

应该在这个系统上使用 ‘man perl’ 或

‘perldoc perl’ 找到。如果你可以访问互联网，

将你的浏览器指向 `http://www.perl.com/`，即 Perl

主页。

- `-V` 打印主要 Perl 配置值的摘要以及 `@INC` 的当前值。

```
-V:names
```

此参数将 `names` 配置变量的值打印到 `STDOUT`。

- `-w` 告诉 Perl 显示关于程序中潜在问题的警告信息，例如仅使用一次的变量（可能是拼写错误），在比较中使用 `*` 而不是 `==`，等等。这通常与 `-c` 标志一起使用，以进行彻底的程序检查。

```
perl -cw finalassignment.pl
```

- `-x directory` 告诉 Perl 脚本嵌入在更大的东西中，如电子邮件消息。Perl 丢弃 `#!` 开始且包含字符串 `perl` 的行之前的所有内容，以及 `__END__` 之后的所有内容。如果指定了目录，Perl 会在执行脚本前更改到该目录。

#### 模块和 CPAN

Perl 社区（以及 Linux 社区）的一个巨大优势在于它是一个开源社区。Perl 通过 CPAN（Perl 综合归档网络）表达了这一点，它是一组代码仓库的镜像网络——更准确地说，是 Perl 代码。

CPAN 的大部分由*模块*组成，模块是可用的代码块，执行有用的操作，这样你每次试图构建自行车时就不必重新发明轮子。有数千个 Perl 模块，从发送电子邮件到维护你的 Cisco 路由器访问列表，到告诉你名字是男性还是女性，到以某种花哨格式打印时间，无所不包。有用于 CGI 编程的模块，访问套接字库的模块，以及为你发布到 Usenet 的模块。如果你能想到做某事，很有可能有一个模块可以帮助你。如果没有有帮助的模块，鼓励你编写一个并与社区的其他人分享。

在 `http://www.perl.com/CPAN/` 你会找到 CPAN 多路复用器，它试图引导你到离你最近的 CPAN 站点。

Perl 随附一组已安装的标准模块。这些模块包含你想要的许多功能。你可以使用 CPAN 模块（它是标准模块之一）在我的系统上下载和安装其他模块。输入以下命令会让你进入一个交互式 Shell，让你访问 CPAN。你可以在提示符处输入 *help* 获取关于如何使用 CPAN 程序的更多信息。

```
perl -MPAN -e shell
```

安装来自 CPAN 的模块（或编写你自己的模块）后，你可以使用 `use` 函数将该模块加载到内存中，以便你可以使用它。

```
use Time::CTime;
```

`use` 在变量 `@INC` 列出的目录中查找模块。在这个例子中，`use` 查找一个名为 `Time` 的目录，该目录包含一个名为 `CTime.pm` 的文件，进而假设该文件包含一个名为 `Time::CTime` 的软件包。每个模块的分发版本都应包含关于使用该模块的文档。

有关所有标准 Perl 模块（安装 Perl 时随附的那些）的列表，请参阅 Perl 文档中的 *perlm5lib*。你可以在命令提示符下输入 *perldoc perlm5lib* 来阅读此文档。

### 代码示例

在过去几年里，许多人形成了一种观念，认为 Perl 是一种 CGI 语言，好像它除了 CGI 之外毫无用处。事实恰恰相反。你可以将 Perl 用于系统管理的方方面面，并作为你计划在新 Linux 系统上运行的任何应用程序的基础构件。

以下章节提供了一些你可能想用 Perl 完成的任务示例。Perl 足够通用，你可以让它完成几乎任何事情。

#### 发送邮件

让 Perl 发送邮件有几种方法。一种常见的方法是打开一个通往 *sendmail* 的管道并向其发送数据（如列表 32.5 所示）。另一种方法使用 `Mail::Sendmail` 模块，它直接使用套接字连接来发送邮件（如列表 32.6 所示）。后一种方法更快，因为它不需要启动外部进程。

**列表 32.5 使用 `sendmail` 发送邮件**

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

注意电子邮件地址中的 `@` 符号需要转义，以便 Perl 不会尝试评估该名称的数组。

用于打印邮件消息的语法被称为 *heredoc*。语法如下：

```perl
print <<EndText;
.....
EndText
```

`EndText` 值在块的开头和结尾必须完全相同，包括任何空白字符。

**列表 32.6 使用 `Mail::Sendmail` 模块发送邮件**

```perl
use Mail::Sendmail;
%mail = ('To' => 'dpitts@mik.net',
         'From' => 'rbowen@mik.net',
         'Subject' => 'Email notification',
         'Message' => 'Sending email from Perl is easy!');
sendmail(%mail);
```

Perl 会忽略哈希中最后一个元素后的逗号。保留它很方便；如果你想向哈希添加项目，不需要添加逗号。这纯粹是一种风格选择。

另外注意，在单引号 (' ') 内的 `@` 符号不需要转义。Perl 在单引号内不 *插值*（评估变量），但在双引号和 `heredoc` 内会。

##### 清除日志

许多程序维护各种日志。通常，日志中的许多信息是冗余的或无用的。列表 32.7 中显示的程序删除文件中包含特定单词或短语的所有行，这样你就可以清除那些已知不重要的行。例如，你可能希望删除 Apache 错误日志中源自你的测试客户端机器的所有行，因为你知道这些错误消息是在测试过程中产生的。

**列表 32.7 清除日志文件**
