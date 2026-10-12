
131.107.3.19 registered 2 hits

152.163.207.36 registered 56 hits

### 分析第一个访问计数器

`hitcnt.pl` 的第一个版本输出很粗陋，大多数命令行应用程序都是如此。然而，你为更庞大的功能奠定了基础。

#### 提示

Apache 服务器用户只需要进行两个微小的更改，即可让 `hitcnt.pl` 与其日志文件协同工作。首先，当然要更改程序顶部定义的日志文件位置。然后，将调用 Perl 的 `split` 函数的行改为与 `logs1.pl` 中相同的调用（即你在上一节中编写的脚本）。

`hitcnt.pl` 中介绍了两个新的 Perl 结构：最后语句和哈希（hashes）。哈希是一种特殊的数组；它的元素不是像 `$array[4]` 那样通过数字索引，而是通过字符串索引，例如 `$color('banana') = 'yellow'`。哈希简化了某些任务，在本例中是统计某些——IP 地址的出现次数。哈希用特殊符号 `%` 标记。

让我们来看代码。从日志文件中提取客户端 IP 地址的方法与你在上一节中执行的方法相同。注意你没有更改对 `split` 的调用：

```perl
while (<LOG>) {
  ($ClientIP, $Dummy, $Date, $Time, $SvcName,
    $SrvrName, $SrvrIP, $CPUTime, $BytesRecv,
    $BytesSent, $SvcStatus, $NStatus,
    $Operation, $Target, $Dummy) =
  split (/, /);
```

但这里有一个例外。并不是将输入行存储在本地变量中，而是让 `split` 直接从标准输入（在 Perl 中定义为 `$_`）获取数据。这就是为什么 `split` 只有一个搜索模式作为参数。

#### 注意

没有理由在 `split` 中传入完整的日志文件条目列表，因为 `hitcnt.pl` 只使用了第一个变量。然而，在脚本的未来版本中你可能需要比 IP 地址更多的信息，所以你应该保留其余变量。

然后你将 IP 地址存储在哈希中。哈希条目的索引是 IP 地址，哈希条目的的值是你看到某个特定 IP 地址的次数：

```perl
$NumHits{$ClientIP}++;
```

`++` 运算符用于增加其操作对象的值。当你第一次给出某个 IP 地址时，`$IPHash{$ClientIP}` 是未定义的，并且

```perl
$BytesSent, $SvcStatus, $NTStatus,
$Operation, $Target, $Dummy) = split (/,/);
```

```perl
# Store the client IP address, increment counter.
```

```perl
$NumHits($ClientIP)++;
```

```perl
}
# end while (<LOG>)
```

```perl
close (LOG); # Close the log file.
```

```perl
# Print out the results after formatting date from
# file name.
```

```perl
if ($LogFile ~ /(..)(\d\d)(\d\d)(\d\d))/
  $year = $2;
  $month = $3;
  $day = $4;
```

```perl
print "On $month/$day/$year:\n\n";
```

```perl
foreach $ip ( keys %NumHits )
  print "$ip registered $NumHits{$ip} hits\n";
```

```perl
print "\n"; # Extra line.
```

```perl
} # end foreach $LogFile...
```

```perl
# Close the directory.
```

```perl
closedir (LOGDIR);
```

```perl
# Endcntl1.pl
```

将此脚本保存为 `hitcnt1.pl`，并再次从命令行运行它。

不时使用 `Ctrl+S` 定期停止输出；你应该能看到与图 15.7 所示类似的界面。

## 分析整个目录的访问计数器

尽管看起来是一个令人生生畏的新程序，但你只为原始的 `hitcnt.pl` 增加了了两个新功能。你使用了 Perl 的目录函数来获取日志文件目录的句柄，并将处理 IP 地址和计数次数的代码放入了一个 `foreach` 循环中。

程序顶部的更改是非常细微的：

```perl
$LogDir = "c:\winnt/system32/logfiles";
opendir(LOGD, $LogDir) or die "Can't open LogDir: $!";
@LogFiles = readdir(LOGD)
```

注意，你现在只需要定义的字符串常量是日志目录的路径。字符串 `$LogDir` 是 `opendir` 的参数，它返回 `LOGD` 句柄。该句柄被 `readdir` 用于将目录中的所有文件放入 `@LogFiles` 中。

在 `foreach` 循环的开头有两个特别关注的项目。第一个测试是每个 Windows 和 Unix 目录中都存在的两个特殊文件：

```perl
foreach $LogFile (@LogFiles)
{
    if ($LogFile eq ".") || ($LogFile eq "..")
        next;
}
```

文件名指的是当前目录，而 `..` 是父目录；在这个例子中你不需要它们，所以它们被忽略了。

是如何实现的呢？通过使用 Perl 的 `next` 语句，它本质上与你在上一节中学习的最后一个语句相反。这里

![](img/6e99147f217994f89499215b2cff677f_448_0.png)

# 第五章

`last` 会跳出循环，而 `next` 会让循环重新开始，而不执行后续的任何代码。在这个例子中，如果 `$LogFile` 的值是其中一个特殊文件名，你不希望执行任何操作，而是直接获取下一个文件名。

接下来的代码部分防止了在处理目录句柄时的一种常见错误：

```perl
$LogPath = $LogDir."".$LogFile;
open (LOG, $LogPath) || die "Can't open $LogPath:\n";
```

注意，通过组合目录名和文件名，`$LogFile` 中已经构建了完整的文件路径，这是因为只有当你将日志目录也设置为你的当前目录时，`$LogFile` 才能独立工作打开文件。在每当你运行 `hitcnt1.pl` 时，这种情况发生的概率微乎其微——指定文件路径是最明智之举。

`hitcnt1.pl` 中的最后一个新功能是根据 IIS 日志文件名生成日期：

```perl
if ($LogFile ~ /(..)(\d)(\d)(\d)(\d)/)
{
  $year = $2;
  $month = $3;
  $day = $4;
}

print "On $month/$day/$year:\n";
```

还记得每日 IIS 日志文件名的格式吗？前两个字符是 `in`，后面跟着两位位数的年份、月份和日期。换句话说，1997 年 8 月 24 日的日志文件名为 `in970824.log`。正则表达式 `/(..)(..)(..)(..)/` 按照顺序匹配文件名中的前四对字符。因此，你可以从 `$2` 提取年份，从 `$3` 提取月份，从 `$4` 提取日期，而忽略 `$1`。

## 将访问计数器推向网络端

你现在已经知道如何遍历整个 IIS 日志文件目录，并计算和显示连接到你网站的每个 IP 地址在每天的访问次数。最后一步——将整套内容放在网页上——是最简单的。

你已经通过读取日志文件和处理数据完成了所有最艰出的工作。你只需要做的更改是 `hitcnt1.pl` 底部的 `print` 语句。它们现在需要输出 HTML 格式的代码。

## 监控网站活动

HTML 转换需要几行额外的代码。首先，在顶部附近调用你的 HTML 头部和尾代码：

```perl
# 引入 HTML 头和尾。
require "header.pl";
```

```perl
# 定义日志路径。
$LogDir = "c:\winnt/system32/logfiles";
$Title = "Hit Counter";
```

然后，设置 HTML：

```perl
# 获取文件列表。
@LogFiles = readdir(LOGD);
```

```perl
# 打印表格。
print "<html><head><title>$Title</title></head><body><table>";
```
