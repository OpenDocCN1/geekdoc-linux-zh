
## `$REAL_GROUP_ID` `$GID`

`$` 此进程的真实组 ID (real gid)。如果你在一台同时支持多个组的机器上，它会给出你所属的组的空格分隔列表。第一个数字是由 `getgid($)` 返回的，后续的由 `getgroups()` 返回，其中一个可能与第一个数字相同。

然而，赋值给 `($)` 的值应该是单个数字，以设置真实组 ID。`$` 提供的值在没有手动强制转换（例如通过添加 0）的情况下，不应直接赋值给 `($)`。请注意，这是针对有效组 ID `($)`，后者执行的是列表。

你可以通过 `POSIX::setgid($)` 同时更改真实组 ID 和有效组 ID。对 `($)` 的更改需要检查 `$!` 以检测在尝试更改时任何可能的错误。

助记法：括号用于对内容分组。真实组 ID 是你运行 `setgid` 之前离开的那个组。

## `$EFFECTIVE_GROUP_ID` `$GID`

`$` 此进程的有效组 ID (effective gid)。如果你在一台同时支持多个组的机器上，它会给出你所属的组的空格分隔列表。第一个数字是由 `getgid($)` 返回的，后续的由 `getgroups()` 返回，其中一个可能与第一个数字相同。

同样，赋值给 `($)` 的值也应该是空格分隔的数字列表。第一个数字设置有效组 ID，其余数字（如果有）将传递给 `setgroups()`。要获得 `setgroups()` 为空列表的效果，只需重复新的有效组 ID；若要强制有效组 ID 为 5 且 `setgroups()` 为空，请列出 `$= = "5 5"`。

你可以通过 `POSIX::setgid()`（仅使用单个数值参数）同时更改有效组 ID 和真实组 ID。对 `($)` 的更改需要检查 `$!` 以检测在尝试更改后任何可能的错误。

`$<`、`>`、`$` 和 `($)` 只能在支持对应 `set[re][ug]id()` 程序的机器上设置。`($)` 只能在支持 `setgid()` 的机器上交换。

助记法：参数用于对内容分组。有效组 ID 是正确的那个组，你正在运行 `setgid`。

## `$REAL_USER_ID` `$UID=$`

此进程的真实用户 ID (real uid)。你可以通过 `POSIX::setuid()` 同时更改真实用户 ID 和有效用户 ID。由于对 `($)` 的更改需要检查 `$!`，将尝试检测任何可能的错误。

助记法：如果你运行 `setuid`，它是你调用时所属的那个 uid。

## `$EFFECTIVE_USER_ID` `$EUID=$`

此进程的有效用户 ID (effective uid)。例如：`$<=$;` # 将真实 uid 设置为有效 uid `($,<$) = ($,<);` # 交换真实 uid 和有效 uid

你可以通过 `POSIX::setuid()` 同时更改有效用户 ID 和真实用户 ID。对 `($)` 的更改需要检查 `$!` 以检测在尝试更改后任何可能的错误。

`$` 和 `$` 只能在支持 `reuid()` 的机器上交换。

助记法：如果你运行 `setuid`，它是你进入的那个 uid。

## `$SUBSCRIPT_SEPARATOR` `$SUBSEP`

`$` 维度数组的下标分隔符，如果你需要引用哈希元素如：

```
$foo{x}, $y, $z}
它真的返回
$foo{join($, $x, $y, $z)}
但不要使用
@foo{x,$y,$z} # 一个切片-注意 @ 符号
它返回
($foo{x}, $foo{$y}, $foo{$z})
```

默认是“:”，与 awk 中的 `SUBSEP` 相同。如果你的键包含二进制数据，则 `$` 可能没有任何安全值。

考虑使用 perldoc 中描述的“真实”多维数组。

助记法：逗号（句法上的下标分隔符）是分号。

## `$b`

在使用 `sort()` 时的特殊包变量，见 perldoc 中的 “sort”。由于这种特殊性，这些 'vars' 不需要声明（即使在使用 `strict 'vars'` 伪令时也使用 `vars`）。不要用 `$a` 或 `$b` 将它们词法化。

## `$a`

特别是 `$b` 在使用 `sort()` 时的特殊包变量，见 perldoc 中的 “sort”。由于这种特殊性，这些 'vars' 不需要声明（即使在使用 `strict 'vars'` 伪令时也使用 `vars`）。不要用 `$a` 或 `$b` 将它们词法化。

此变量是在 Perl 5.003 中引入的。

## `%SIG`

该哈希包含信号的处理程序。例如：

```perl
sub handler { #1 argument is signal by my($sig) = @_; print Caught a SIG{shutting down}; close(0); }
$SIG{INT} = \&handler;
$SIG{QUIT} = \&handler;
$SIG{INT} = 'DEFAULT'; # 恢复默认动作
$SIG{QUIT} = 'IGNORE'; # 忽略 SIGQUIT
```

使用值 "PIPE" 通常忽略忽略信号，CHLD信号除外。此类特殊情况请参见 perl。

以下是其他示例：

```perl
$SIG{PIPE} = "Pluer"; # 分配 main::Pluer (不建议)
$SIG{PIPE} = \&Pluer; # 没有问题；分配当前的 $Pluer
$SIG{PIPE} = "Pluer; # 语法错误
$SIG{PIPE} = Pluer(); # 噢，Pluer() 返回了什么？？
```

务必使用裸字（bareword）作为信号处理程序的名称，以免无意中调用它。

如果你的系统拥有 `sigaction()` 函数，则使用该函数安装信号处理程序，并获得可靠的信号处理。

某些内部钩子也可以通过 `%SIG` 哈希进行设置。当准备打印警告阶段时，由 `$SIG{WARN}` 指示的运行时会被调用。警告消息作为第一个参数传递。存在 `__WARN__` 钩子可以抑制向 STDERR 打印普通警告的行为。你可以在变量中设置警告，或将警告转换为致命错误，例如：

```perl
local $SIG{WARN} = sub { $_[0] }; eval proggie;
```

由于 `__WARN__` 不支持 IGNORE 钩子，你可以使用子程序禁用警告：

```perl
local $SIG{WARN} = sub {};
```

当准备抛出致命异常时，调用 `$SIG{DIE__}` 对应的例。错误消息作为第一个参数传递。当存在 `__DIE__` 钩子程序时，异常处理将像没有钩子的情况下一样继续，除非钩子程序通过 `goto &sub`、循环退出或 `die()` 退出。`__DIE__` 句柄在调用期间会被显式调用，因此你可以在 `__DIE__` 处触发 `die`。同样适用于 `__WARN__`。

由于实现上的缺陷，`$SIG{DIE__}` 钩子甚至在 `eval()` 内部也会调用。不要用它来重写 `$@` 中待处理的异常，或将其作为覆盖 `Core::die()` 的奇特替代品。这种奇怪的行为在未来可能会得到修复，使得 `$SIG{DIE__}` 仅在程序即将退出时调用，正如原始意图所示。其他用途均已弃用。

`__DIE__/__WARN__` 句处理器在一个方面非常特殊：它们可能被调用以报告解析器发现（可能的）错误。在这种情况下，解析器可能处于不一致状态，从此类句柄中尝试评估 Perl 代码可能会导致段错误（segfault）。解析 Perl 时产生的这些警告或错误应极谨慎地使用，如下：

```perl
require Carp if defined $S; Carp::confess("Something wrong") if defined &Carp::confess; die("Something wrong, but could not load Carp to give \backtrack\n" . "To see backtrack try starting Perl -MCarp switch");
```

在这里，除非调用处理器的解析器，否则第一行将加载 Carp。如果 Carp 可用，第二行将打印回溯并退出。第三行仅在 Carp 不可用时执行。

在异常处理程序中甚至必须考虑 `$^` 变量简直是错误的。目前的 `$SIG{DIE__}` 会带来麻烦，并且难以追踪错误。避免使用它，改用 `END()` 或 `CORE::GLOBAL::die` 覆盖。

另见 perflunk 中的 "die, "warn"、"eval in perflunk" 以及 warnings 以获取更多信息。

## `$BASELINE`

程序开始的时间，自 Unix纪元以来（1970 年初）的秒为单位的时间。-M、-A 和 -C 字段返回的值基于此值。

## `$PERL_VERSION`

Perl 解释器的修订版本和子版本，以版本对象的形式表示。

此变量在 perl v5.10.0 中首次出现；早期版本的 perl 将具有未定义的值。在 v5.10.0 之前，`$V` 被表示为 v-字符串（v-string）而不是版本对象。

## `$V`

可判断执行脚本的 Perl 解释器是否在正确的版本范围内。
