
`$rec = join(':', $login, $passwd, $uid, $gid, $gcos, $home, $shell);`

注意，与 `split` 不同，`join` 不接受模式作为其第一个参数。

## keys HASH

## keys ARRAY

## keys EXPR

在列表上下文中调用时，返回一个包含指定哈希所有键（keys）的列表；或者在 Perl 5.12 或更高版本中，仅返回数组的索引。5.12 之前的 Perl 版本如果尝试使用数组参数，将产生语法错误。在标量上下文中，返回键或索引的数量。

哈希条目的返回顺序看起来是随机的。实际随机顺序特定于给定的哈希；对哈希进行的一系列精确操作可能会每个哈希产生不同的顺序。对哈希的任何插入都可能改变顺序，任何删除也是如此，但每个 `keys` 返回的最近一个键可以被删除而不改变顺序。只要给定的哈希未被修改，你就可以依赖键、值，并且每次重复返回彼此相同的顺序。详情请参阅 perl 中的“Algorithmic Complexity Attacks”，Perl 的哈希算法和哈希遍历在任何 Perl 版本中都可能变化。绑定哈希（Tied hashes）在插入或删除项时的顺序变化方面可能与 Perl 原生哈希的行为不同。

作为副作用，调用 `keys()` 会返回 HASH 或 ARRAY 的内部迭代器（"each"）。特别是，在空上下文中调用 `keys()` 会重置迭代器且没有其他输出。

这里是打印环境的另一种方法：

```perl
@keys = %ENV; @values = values %ENV; while (@keys) { 
    print shift(@keys), '=', pop(@values), "\n"; 
}
```

或者按键排序：

```perl
foreach $key (sort(%ENV)) { print $key, '=', $ENV{$key}, "\n"; }
```

返回的值是哈希中原始键的副本，修改它们不会影响原始哈希。比较 "values"。

要对哈希进行排序，你需要使用 `sort` 函数。这里按以下值对哈希进行降序数值排序：

```perl
foreach $key (sort { $hash{$b} <=> $hash{$a } keys %hash) { 
    printf "%4d s\n", $hash{$key}, $key; 
}
```

作为 Ivalue（内部值）使用，`keys` 允许你增加为给定哈希分配的哈桶数量。如果你知道哈希将变得很大，这可以提高一定的效率（这类似于通过给 `@array` 分配更大的数字来预扩展数组）。如果你说

`keys %hash = 200;`

那么 `%hash` 将为其分配 200 个桶——实际上是 256 个，因为它们会向上取到 2 的幂。即使执行了 `%hash = ()`，这些桶也会保留；如果你想释放存储，请使用 `undef %hash`；`%hash` 仍然在作用范围内。你不能通过这种方式使用 `keys` 缩小为哈希分配的桶的数量（但你不必担心，尝试没有效果）。在 Ivalue 上下文中 `keys @array` 是语法错误。

从 Perl 5.14 开始，`keys` 可以接受一个标量 EPR，该 EPR 必须包含指向无偏哈希或数组的引用。参数将自动解引用。这一特性被认为是高度实验性的。精确行为在未来的 Perl 版本中可能会更改。

```perl
for keys ($hashref) { ... } for keys ($obj->get_arrayref) { ... }
```

为了避免让运行早期版本 Perl 的代码用户因神秘的语法错误而困惑，请在文件顶部放置此类内容，以指示你的代码仅运行在较版本的 Perl 上：

```perl
use 5.012; # 让 keys/values/each 作用于数组
use 5.014; # 让 keys/values/each 作用于标量（实验性）
```

另请参见 each，values 和 sort。

## kill SIGNAL, LIST

## kill SIGNAL

向进程列表发送信号。返回成功用于发送信号的参数数量（这与实际杀掉的进程数量并不相同，例如当进程被杀掉的情况下）。

```perl
$cnt = 'HUP', $child1, $child2; kill 'KILL', @goners;
```

`SIGNAL` 可以是信号名称（字符串），也可以是信号数字。信号可以带有 SIG 标志，SIGUSR 和 SIG0 都指向同一个信号。推荐使用信号的字符串形式以便于移植性，因为同一个信号在不同的操作系统中有不同的数字。

当前平台支持的信号名称列表可以在 `$Config{sig_name}` 中找到，它由 `Config` 模块提供。详情请参见 `Config`。

负信号与负信号名称相同，它杀死的是进程组而不是进程。例如，`kill '-KILL', $pgrp` 和 `kill -9, $pggrp` 将向指定的整个进程组发送 SIGKILL。这意味着你想使用正负号的负信号。

如果 `SIGNAL` 是数字 0 或字符串 ZERO (`SIGZERO`)，则不会向进程发送信号，但 `kill` 会检查是否可能向其发送信号（也就是说，简而言之，进程由同一用户所有，或者我们是超级用户）。

`length(Encode::encode_utf8(EXPR))` （你必须先使用 Encode。请参考 Encode 和 perlucotide。）

`__LINE__` 一个特殊的标记，可编译为当前行号。

`link OLDFILE,NEWFILE` 创建一个与旧文件名链接的新文件名。成功时返回 true，否则返回 false。

可移植性问题：perlport 中的 “link”。

`listen SOCKET_QUESIZE` 作用与 (2) 系统调用相同。如果执行成功，则返回 true，否则返回 false。请参考 perlic 中“Sockets: Client/Server Communication”的示例。

`local EXPR` 你可能真的更想使用另一个操作符，因为 `local` 并不是大多数人们认为的那个“局部（local）”。详细信息请参考 perlsub 中的“Private Variables by my()”。

一个 `local` 语句将列出的变量修改为该编码块、文件或 `if` 语句的局部变量。如果列出了多个值，则列表必须放在括号内。详细信息请参考 perlsub 中的“Temporary Values via local()”，包括关于绑定数组和哈希的问题。

`delete local EXPR` 结构也可用于将数组/哈希元素的删除操作限制在当前块。请参考 perlsub 中的“Localized deletion of elements of composite types”。

`localtime` `localtime` 将时间函数返回的时间转换为包含 9 个元素的列表，其中包含针对本地时间的分析结果。通常用法如下：

```
# 0 1 2 3 4 5 6 7 8 ($sec,$min,$hour, $mday, $mon,$year, $wday, $yday,$isdst) = localtime(time);
```

所有列表元素均为数值型，且直接源自 C 语言的 `struct tm`。`$sec`、`$min` 和 `$hour` 分别是指定时间的秒、分、小时。

`$mday` 是月份中的几几，`$mon` 是年份 0..11 中的月份，其中 0 表示 1 月，11 表示 12 月。这使得我们很容易地从列表中获取名称：

`$year` 包含自 1900 年以来的年份。要获取 4 位年份，请写：

```
$year += 1900;
```

要获取年份的最后两位（例如 2001 年的“01”），请执行：

```
$year = sprintf("%02d", $year % 100);
```

`$wday` 是星期几，0 表示星期日，3 表示星期三。`$yday` 是一年中的第几天，范围为 0..364（闰年为 0..365）。

如果省略 `EXPR`，`localtime()` 返回当前时间（如 (3) 返回的结果）。

在标量上下文中，`localtime()` 返回 (3) 的值：

```
$now_string = localtime(); # 例如 "Thu Oct 13 04:54:34 1994"
```

该标量值的格式**不是**依赖于本地化（locale），而是内置在 Perl 中的。如果需要使用 GMT 而不是本地时间，请使用内置的 `:gmtime`。另参考 Time:: 模块（用于转换秒）。

要获取某种格式化但依赖于本地化的日期字符串，请适当设置你的本地环境变量（请参阅 perlocale），例如：

```perl
use POSIX qw(strftime);
$now_string = strftime "%Y %a %b %H:%M:%S", localtime); # 根据你的本地化环境格式化的 GMT：
```
