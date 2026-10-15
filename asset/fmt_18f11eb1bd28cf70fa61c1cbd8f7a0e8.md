
`vars`（参见 perl 手页中的 vars 章节）可以在此类情况下作为替代方案，用于显式用包命名空间限定所有全局变量。用此类局部变量声明的变量对任何自动加载的程序可见（但遗憾的是，在包外部不可见）。

# AutoLoader 对比 SelfLoader

AutoLoader 的目的与 SelfLoader 相似：它们都推迟子程序的加载。SelfLoader 使用 `__DATA__` 标记而不是 `__END__`。虽然这意味着你不需要使用磁盘文件层次以及为每个加载的程序进行相关的打开和关闭，但 SelfLoader 在解析 `__DATA__` 之后的行时较慢。一旦在启动时解析了行，程序会被缓存。SelfLoader 还可以处理文件中的多个包。

AutoLoader 仅在请求时读取代码。在许多情况下，这应该使其比 SelfLoader 快；然而，AutoLoader 要求使用类似 AutoSplit 的机制来创建单独的文件。`ExtUtils::Maker` 手页在使用 AutoLoader 时会自动调用 AutoSplit。

# 注意事项 (Caveats)

在 Perl 5.02 之前，AutoLoader 的接口略有不同。

# 参见

`SelfLoader` 手页。

# 基准测试 (Benchmark)

Benchmark 提供了一组程序，用于确定执行代码所需的时间。

# 概要

Benchmark 封装了一组程序来确定执行代码所需的时间。

# 概要

Benchmark 模块用法。

```
timethis(count, "code");

# 或者使用引用。
timethise(count,
  'Name1' => sub { ...code1... },
  'Name2' => sub { ...code2... },
);

$st = timeit(count, '...code...')
print "$count loops of other took";
```

# 方法

以下方法配置 Benchmark。

new 返回当前时间。例如：

```
use Benchmark;
$t0 = new;
# ... your code ...
$t1 = new;
$td = timediff($t1, $t0);
print "the code took:",timestr($td),"\n";
```

debug 通过设置标志启用或禁用调试：

```
debug Benchmark 1;
$t = timeit(10, ' ');
debug Benchmark 0;
```

# 标准导出

如果你使用 Benchmark 模块，可以使用以下程序。

`timeit` (`COUNT`, `CODE`) `COUNT` 参数是循环次数，`CODE` 是要执行的代码。`CODE` 可以是代码引用或要评估的字符串；任何一种方式都在调用者的包中运行。该程序返回一个 Benchmark 对象。

`timethis` (`COUNT`, `CODE`, [`TITLE`, [`STYLE`]]) `COUNT` 参数是循环次数，`CODE` 是要执行的代码。`CODE` 可以是要评估的字符串或代码引用；任何一种方式都在调用者的包中运行。结果打印到 STDOUT，格式为 TITLE 后接时间。如果省略了 TITLE 参数，默认值为 "timethis COUNT"。

如果 `COUNT` 为负数，则被解释为运行的最小 CPU 秒数。零表示默认的三秒。

此示例运行至少 10 秒：

```
timethis(-10, $code)
```

此程序运行两个代码测试，至少三秒：

```
timethise(0, test1 => '...', test2 => '...')
```

CPU 秒在 Unix 术语中，是指进程本身的用户时间和内核系统时间之和，与此对应的是真实时间（墙钟时间）以及子进程花费的时间。小于 0.1 秒是不允许的（例如，count 为 -0.01 将导致致命运行时异常）。

# 标准 Perl 模块 671

CPU 秒是最小时间。CPU 调度和其他操作系统的因素可能会增加复杂性，导致花费多一点时间。然而，基准测试输出还将列出每秒运行 `$code` 次数，这个数字比实际秒数更有意义。此例返回一个 Benchmark 对象。

`timethese` (`COUNT`, `CODEHASHREF`, [`STYLE`]) `CODEHASHREF` 是一个哈希表的引用，其键为名称，值则是要评估的字符串或代码引用。对于 `CODEHASHREF` 中的每个 (`KEY`, `VALUE`) 对，此例会调用 `timethis(COUNT, VALUE, KEY, VALUE)`。这些例程按 KEY 的字符串比较顺序调用。`COUNT` 可以为 0 或负数。详见 `timethis()`。

`timediff` (`T1`, `T2`) Timiff 返回 Benchmark 时间之间的差，作为一个 Benchmark 对象，适用于传递给 `timestr()`。

`timesum` (`T1`, `T2`) 该命令返回两个 Benchmark 时间之和，作为一个 Benchmark 对象，适用于传递给 `timestr()`。

`timestr` (`TIMEDIFF`, [`STYLE`, [`FORMAT`]]) 此例返回一个字符串，按照要求的 STYLE 格式化 TIMEDIFF 对象中的时间。`TIMEDIFF` 预期为与 `timediff()` 返回的类似的 Benchmark 对象。

`STYLE` 可以是 `all`, `noc`, `nop` 或 `auto`。`all` 命令显示五种可用时间的每一种（墙钟时间、用户时间、系统时间、子进程时间和子进程系统时间）。`noc` 命令显示除两个子进程时间以外的所有可用时间。`nop` 命令仅显示墙钟时间和两个子进程时间。`auto` 命令（默认值）的作用等于 `all`，除非两个子进程时间均为零，在这种情况下作用等于 `noc`。

`FORMAT` 是 print-f 风格的选择符（不带前导的 %），用于打印时间。默认为 `5.2f`。

# 注意事项

将已评估的字符串与代码引用进行比较将得到不准确的结果。代码引用的执行时间比等效字符串慢。

实时计时是使用 `time(2)` 执行的，因此粒度仅为一秒。

# 672 附录 C

短测试可能会产生负数，因为 Perl 执行短测试所需的空循环似乎比比执行实际代码更长时间。例如，尝试：

```
timethis(100, '1');
```

空循环的系统时间可能略大于带有实际代码循环的系统时间；因此，差异最终可能小于 0。

# bytes

此 pragma 强制 Perl 将字符串视为字节而非字符。这在处理 Unicode 数据时非常重要，其中 `chr(400)` 是一个字符但占用两个字节：

```
my $x = chr(400);
print length($x); # 1,因为它是一个字符
{
  use bytes;
  print length($x); # 2,因为它是两个字节
}
```

# 参见

第 13 章，“Perl 与 Unicode”。

# Carp

此模块写入错误或诊断信息，但提供了比 `warn()` 或 `die()` 更多的丰富的上下文信息。

# 概要

```
use Carp;
croak "We're outta here!";
```

```
use Carp qw(cluck);
cluck "This is how we get here!";
```

# 描述

Carp 例在你自己的模块非常有用，因为它们的作用类似于 `die()` 或 `warn()`；然而，它们会报告错误在代码中的位置。如果例 `Foo()` 中包含一个 `carp()`，`carp()` 会报告错误发生在调用 `Foo()` 的地方，而不是调用 `carp()` 的地方。

# 强制堆栈跟踪

作为调试辅助，你可以强制 Carp 在所有模块中将 `croak` 视为 `confess`，将 `carp` 视为 `cluck`。换句话说，你可以强制执行详细的堆栈跟踪。当你试图追溯为什么或从哪里生成了警告或错误时，这可能非常有帮助。

此功能通过以下方式启用：

```
perl -Marparp=verbose script.pl
```

或者通过在环境变量 `PERLOPT` 中包含字符串 `MCarp=verbose`。

# 缺陷

目前，Carp 例程不处理异常对象。如果调用的第一个参数是引用，它们将简单地根据情况调用 `die()` 或 `warn()`。

# GI::Carp

此模块提供了将错误和诊断消息写入 HTTPD Web 服务器日志的例，而不是标准错误设备。

# 概要

```
use CGI::Carp;

die "dying because of fatal error.\n";

use CGI::Carp qw(cluck);
cluck "I wouldn't do that if I were you";

use CGI::Carp qw(fatalsToBrowser);
die "Fatal error messages are now sent to browser";
```

# 描述
