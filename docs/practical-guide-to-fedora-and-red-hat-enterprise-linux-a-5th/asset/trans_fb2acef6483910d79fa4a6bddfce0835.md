

![](img/f28adb66a7398a382f0505e0ba74a872_1056_0.png)

第三条语句初始化了数组 `@list`。虽然该语句并非必需，但包含它是良好的编程实践，有助于提高代码的可读性。下一条语句打开 `$fh` 词法句柄。在该 open 语句的文件引用部分（见第 1000 页）中，末尾的管道符号 (|) 指示 Perl 将管道符号之前的命令行传递给 shell 执行，并在程序从文件句柄读取时接受该命令的标准输出。在这种情况下，该命令使用 `grep` 过滤 `/etc/group` 文件（见第 472 页）中包含 `$user` 中用户名的那一行。如果 Perl 无法打开句柄，`die` 语句将显示错误消息。

```perl
$ cat groupfind.pl
$user = shift || $ENV{"USER"};
say "User $user belongs to these groups:";
@list = ();
open (my $fh, "grep $user /etc/group |") or die "Error: $!\n";
while ($group = <$fh>) {
  chomp $group;
  $group =~ s/(.*?):.*/$1/;
  push @list, $group;
}
close $fh;
@list = sort @list;
say "@list";
```

```text
$ perl groupfind.pl
User sam belongs to these groups:
adm admin audio cdr crond dialout dip floppy kvm lpadmin ...
```

`groupfind.pl` 中的 `while` 结构从 `grep` 的标准输出中读取行，并在 `grep` 执行完毕后终止。在 `/etc/group` 的每一行中，组名最先出现，随后是一个冒号和其他信息，包括属于该组的用户名称。下面是该文件中的一行：

sam:x:1000:max,zach,helen

这一行：

```perl
$group =~ s/(.*?):.*/$1/;
```

使用正则表达式和替换功能，从每一行中去除组名以外的所有字符。正则表达式 `.*?` 会对零个或多个字符进行贪婪匹配，后跟一个冒号；在星号后加上问号可使该表达式执行非贪婪匹配（见第 1010 页）。将表达式中需要程序显示的那部分字符串用括号括起来，使得 Perl 能够在替换字符串中使用正则表达式匹配的字符串。最后的 `.*` 匹配行的其余部分。Perl 将替换字符串中的 `$1` 替换为正则表达式括号部分（即括号内的部分）匹配的字符串，并将该值（组名）赋值给 `$group`。

`chomp` 语句去除行尾的 NEWLINE（正则表达式未匹配该字符）。`push` 语句将 `$group` 的值添加到 `@list` 数组的末尾。如果没有 `chomp`，输出的每一组将各自独占一行。在 `while` 结构处理完来自 `grep` 的输入后，`sort` 对 `@list` 进行排序，并将结果赋值给 `@list`。最后一条语句显示用户所属组的排序列表。

## opendir 和 readdir

下一个示例介绍了 `opendir` 和 `readdir` 函数。`opendir` 函数以类似于 `open` 打开普通文件的方式打开目录。它接受两个参数：目录句柄的名称和要打开的目录名称。`readdir` 函数从打开的目录中读取文件名。

在该示例中，`opendir` 使用 `$dir` 词法目录句柄打开工作目录（由 . 指定）。如果 `opendir` 失败，Perl 将执行 `or` 运算符后的语句；`die` 向标准错误发送错误消息并终止程序。打开目录后，`while` 循环遍历目录中的文件，将 `readdir` 返回的文件名赋值给词法变量 `$entry`。`if` 语句仅针对是目录的文件（-d）执行 `print`。`print` 函数显示目录名称，除非目录名为 `.` 或 `..`。当 `readdir` 读取完工作目录中的所有文件时，它返回 `false`，控制权传递给 `while` 块之后的语句。`closedir` 函数关闭打开的目录，`print` 在程序显示的目录列表后显示一个 NEWLINE。

```perl
$ cat dirs2a.pl
#!/usr/bin/perl
print "The working directory contains these directories:\n";
opendir(my $dir, '.') or die "Could not open directory: $!\n";
while (my $entry = readdir $dir) {
    if (-d $entry) {
        print $entry, ' ' unless ($entry eq '.' || $entry eq '..');
    }
}
closedir $dir;
print "\n";
$ ./dirs2a.pl
The working directory contains these directories:
two one
```

## split

`split` 函数根据指定的分隔符将字符串分割为子字符串。调用 `split` 的语法是：

```perl
split (/re/, string);
```

其中 `re` 是分隔符，是一个正则表达式（通常是单个正则字符），`string` 是要分割的字符串。如下一个示例所示，你可以将 `split` 返回的列表赋值给数组变量。

下一个程序在 Linux 下运行，并列出 UID 大于或等于 100 的 `/etc/passwd`（见第 475 页）文件中列出的用户的用户名。它使用 **while** 结构从 **passwd** 中读取行到 **$user**，并使用 **split** 将行拆分为以冒号分隔的子字符串。以 **@row** 开头的行将这些子字符串中的每一个赋值给 **@row** 数组的一个元素。**if** 语句评估的表达式在第三个子字符串（即 UID）大于或等于 100 时为 *true*。由于该表达式比较的是两个数字，因此使用 **>=** 数值比较运算符；如果是字母比较，则使用 **ge** 字符串比较运算符。

**print** 语句将 UID 编号及相关的用户名发送到 **$Sortout** 文件句柄。该句柄的 **open** 语句建立了一个管道，将输出发送给 **sort** **-n**。由于 **sort** 工具（见第 155 页）在接收完所有输入之前不会显示任何输出，因此 **split3.pl** 在关闭 **$Sortout** 句柄之前不会显示任何内容，而该句柄在读取完 **passwd** 文件后才被关闭。

```perl
$ cat split3.pl
#!/usr/bin/perl -w

open ($pass, "/etc/passwd");
open ($Sortout, "| sort -n");
while ($user = <$pass>) {
	@row = split (/:/, $user);
	if ($row[2] >= 100) {
		print $Sortout "$row[2] $row[0]\n";
	}
}

close ($pass);
close ($Sortout);
```

```text
$ ./split3.pl
100 libuuid
101 syslog
102 klog
103 avahi-autoipd
104 pulse
...
```

下一个示例统计并显示调用时传入的参数，使用 **@ARGV**（见第 1002 页）。**foreach** 结构遍历 **@ARGV** 数组中的元素，该数组保存命令行参数。**++** 前置自增运算符在显示 **$count** 之前对其进行递增。

```perl
$ cat 10.pl
#!/usr/bin/perl -w

$count = 0;
$num = @ARGV;
print "You entered $num arguments on the command line:\n";
foreach $arg (@ARGV) {
print ++$count, ". $arg\n";
}
```

```text
$ ./10.pl apple pear banana watermelon
You entered 4 arguments on the command line:
1. apple
2. pear
3. banana
4. watermelon
```

## 章节摘要

Perl 由 Larry Wall 于 1987 年编写。自那时起，Perl 在规模和功能上不断壮大，现已成为一种非常流行的语言，用于文本处理、系统管理、软件开发和通用编程。Perl 最大的优势之一是其对数千个第三方模块的支持，其中许多模块存储在 CPAN 仓库中。

`perldoc` 实用程序用于查找并显示本地 Perl 文档。它还允许你通过在程序中包含 pod（plain old documentation）行来为 Perl 程序编写文档。

Perl 提供三种类型的变量：标量（以 `$` 开头的单数变量）、数组（以 `@` 开头的复数变量）以及哈希（也称为关联数组；以 `%` 开头的复数变量）。数组和哈希变量都保存列表，但数组是有序的，而哈希是无序的。标准控制流语句允许你改变 Perl 程序内语句的执行顺序。此外，Perl 程序可以利用子例程，其中可以包含局部的变量（词法变量）。

正则表达式是 Perl 的强项之一。除了许多 Linux 实用程序中可用的相同功能外，Perl 还提供了允许执行更复杂字符串处理的正则表达式功能。

## 练习题

- 1. 在 Perl 中关闭警告的两种不同方法是什么？
- 2. 数组和哈希之间有什么区别？
- 3. 在每个示例中，何时使用哈希，何时使用数组？
  - a. 统计日志文件中某个 IP 地址出现的次数。
  - b. 生成一个超过磁盘配额的用戶列表，用于报告。
- 4. 编写一个正则表达式来匹配带引号的字符串，例如：
  He said, "Go get me the wrench," but I didn't hear him.

