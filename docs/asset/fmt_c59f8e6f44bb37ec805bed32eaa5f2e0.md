
```
$ cat re8.pl
$stg = "What is 123 and 456";
$stg =~ s/\D+(\d+).*/$1;
print "$stg\n";
```

```
$ perl re8.pl
123
```

# CPAN 模块 1097

最后，以 root 权限运行安装模块：

```
# make install
Installing /usr/local/share/perl/5.10.0/Timestamp/Simple.pm
Installing /usr/local/man/man3/Timestamp::simple.3pm
Writing /usr/local/lib/perl/5.10.0/auto/Timestamp/Simple/.packlist
Appending installation info to /usr/local/lib/perl/5.10.0/perl.pod
```

安装模块后，你可以使用 `perdoc` 显示文档，从而了解如何使用该模块。示例请参见第 1059 页。

某些模块包含 SYNOPSIS 摘要部分。如果你安装的模块包含此类部分，可以通过将 SYNOPSIS 部分中的代码放入文件中并作为 Perl 程序运行来测试该模块：

```
$ cat times.pl
use Timestamp::Simple qw(stamp);
print stamp, "\n";
```

```
$ perl times.pl
2010090418627
```

你可以在 Perl 程序中该模块。下面的示例使用了时间戳模块来生成唯一文件名：

```
$ cat fn.pl
use Timestamp::Simple qw(stamp);
```

```
# 将时间戳存储在变量中
$ts = stamp, "\n";
```

```
# 去掉年份
$ts =~ s/^\d*\.//;
```

```
# 创建唯一文件名
$fn = "myfile." . $ts;
```

```
# 打开、写入并关闭文件
open(OUTFILE, '>', "$fn");
print OUTFILE "Hi there.\n";
close(OUTFILE);
```

```
$ perl fn.pl
$ls myfile
myfile.2010905183010
```

你可以使用 `substr` 函数代替正则表达式去掉年份。要做到这一点，请将以 `$ts` 开头的行替换为以下行。在这里，`substr` 取的是字符串 `$ts` 从位置 4 开始并持续到字符串末尾的值：

```
$ts = substr($ts, 4);
```

## 1098 第 28 章 PERL 脚本语言

### 示例

本节提供了一些示例 Perl 程序。首先尝试原样运行这些程序，然后修改它们以学习更多关于 Perl 编程的知识。

第一个示例在 Linux 下运行，显示作为参数提供的用户所属的组列表。如果没有提供参数，它将显示运行程序的用户所属的组列表。在 Perl 程序中，`%ENV` 哈希存储了来自调用 Perl 的 shell 的环境变量。该哈希中的键 `key` 是环境变量的名称，值 `value` 是对应变量的值。第一行代码为 `Suser` 分配了一个名称。`shift` 函数 第 1071 页 获取第一个命令行参数的值，并移动剩余的参数 如果有。如果用户带参数运行程序，则该参数被赋值给 `Suser`。如果命令行上没有出现参数，`shift` 将失败，Perl 将执行逻辑或 `||` 之后的语句。该语句提取与 `%ENV` 中 `user` 键关联联的值，即运行程序的用户的用户名。

第三条语句初始化了数组 `@list`。虽然该语句不是必须的，但包含它是一个良好的习惯，可以使代码更易读。下一条语句打开了词域变量 `$fh`。此 `open` 语句文件句柄 第 1082 页 末尾的管道符号 `|` 告诉 Perl 将管道符号之前的命令行传递给 shell 执行，并在程序从文件读取内容时接受该命令的标准输出。在这种情况下，命令使用 `grep` 过滤 `/etc/group` 文件 第 506 页，筛选包含 `Suser` 中存储的用户名的行。如果 Perl 无法打开句柄，`die` 语句将显示错误消息。

#### 接受来自进程的输出

```
$ cat groupfind.pl
$user = shift || $ENV{"USER"};
say "User $user belongs to these groups:";
@list = ();
open (my $fh, "grep $user /etc/group |") or die "Error: $!\n";
while ($group = <$fh>) {
  chomp $group;
  $group =~ s/.*://;
  push @list, $group;
}
close($fh);
print join(", ", @list);
```

```
$ perl groupfind.pl
User root belongs to these groups:
admin, sudo, dialout
```

`split` 函数根据指定的分隔符将字符串划分为多个子字符串。调用 `split` 的语法为：

```
split (re, string);
```

其中 `re` 是分隔符，它是一个正则表达式 通常是单个字符，而 `string` 是要划分的字符串。正如下一个示例所示，你可以将列表分配数组变量。

下一个程序在 Linux 下运行，列出 `/etc/passwd` 中 UID 大于或等于 100 的用户名。它使用 `while` 循环从 `passwd` 读取行到 `User`，并使用 `split` 将行按逗号分割成子字符串。以 `@row` 开头的行将这些子字符串赋值赋值给 `@row` 数组的元素。`if` 语句表达式当第三个子字符串 UID 大于或等于 100 时为真。由于比较的是两个数字，该表达式使用了 `>=` 数字比较符；字母比较则使用 `ge` 字符串比较符。

`print` 语句将 UID 数字和关联的用户名显示到 sortout 文件。该句柄的 `open` 语句建立了一个管道，将其输出传递给 `sort -n`。`sort` 工具 第 154 页 在读取完所有输入之前不会显示任何输出，`split3.pl` 在关闭 sortout 文件之前不会显示任何内容，而该文件在读取完 `passwd` 文件后关闭。

```
$ cat split3.pl
!/usr/bin/perl -w

open($pass, "/etc/passwd");
open($sortout, "| sort -n");
while ($user = <pass>) {
    @row = split (/:/, $user);
    if ($row[2] >= 100) {
        print $sortout "$row[2] $row[0]\n";
    }
}
close($pass);
close($sortout);
```

```
$ perl split3.pl
100 bin
101 daemon
102 games
```

```
$ ./split3.pl
100 libuuid
101 syslog
102 klog
103 avahi-autoipd
104 pulse
```

下一个示例使用 `@ARGV` 第 108 页 计数并显示调用它时传入的参数。`foreach` 结构循环遍历 `@ARGV` 数组中的元素，该数组存储了命令行参数。`++` 自增操作符在显示之前进行计数。

```perl
$ cat 10.pl
!/usr/bin/perl -w
```

```perl
$count = 0;
$num = @ARGV;
print "You entered $num arguments on the command line:\n";
foreach $arg (@ARGV) {
    print ++$count, ". $arg\n"
}
```

```perl
$ 10.pl apple pear banana watermelon
```

你在命令行上输入了 4 个参数：

- 1. apple

2. pear

3. banana

4. watermelon

### 章节总结

Perl 是由 Larry Wall 在 1987 年编写的。自那时起，Perl 的规模和功能不断增长，现在已成为一种非常流行的语言，用于文本处理、系统管理、软件开发和通用编程。Perl 最大的资产之一是它对数千第三方模块的支持，其中许多模块存储在 CPAN 仓库中。

`perdoc` 工具用于查找和显示本地 Perl 文档。它允许你通过显示程序中包含的 pod 普通旧文档 行来为 Perl 程序编写文档。
