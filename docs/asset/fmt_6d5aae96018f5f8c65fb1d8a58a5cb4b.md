
`sub READ { $my\self = shift; $my\bufref = \$_[0]; my($undef, $len, $offset) = @_; print "READ called, \$buf=$bufref, \$len, \$offset=$offset"; # add to $$bufref, shift $len to number of characters $len; }`

## READLINE

当通过 `<HANDLE>` 或 `readline` 读取句柄时，将会调用此方法。
作为 `readline` 在标量上下文中，它应该返回下一行，如果没有更多数据则返回 `undef`。在列表上下文中，它应该返回所有剩余行，返回的字符串应包含输入记录分隔符 `$`（参见 perl），除非它是 `undef`（即 "slurp" 模式）。

```perl
sub READLINE { $my \$ = shift; if (wantarray) { return ("all remaining\n", "lines up\n", "to of\n"); } else { return ("READLINE called " .$$ . " tis\n"); } }
```

## GETC

当调用 `getc` 函数时，将会调用此方法。

```perl
sub GETC { print "Don't GETC, Perl"; return "a"; }
```

## EOF

当调用 `eof` 函数时，将会调用此方法。

从 Perl 5.12 开始，将传递一个额外的整数参数。在以下情况下：

如果未带参数调用 `eof`；为 0；
如果 `eof` 接收到一个文件句柄，例如 `eof (FH)`；为 1；
在非常特殊的情况下，如果绑定句柄是 `ARGV` 且带有空列表参数调用 `eof`，例如 `eof ()`；为 2。

```perl
sub EOF { not length $stringbuf }
```

## CLOSE

当通过 `close` 函数关闭句柄时，将调用此方法。

```perl
sub CLOSE { print "CLOSE called.\n" }
```

## UNTIE

与其他类型的绑定（ties）一样，当发生 `untie` 时，将调用此方法。在此发生时，可能 {“自动 CLOSE”。见下文的“Untie 陷阱（The untie Gotcha）”。

## DESTROY

与其他类型的绑定一样，当绑定句柄即将被销毁时，将调用此方法。这对于调试和清理有用。

```perl
sub DESTROY { print "</shout>\n" }
```

以下是使用我们示例的方法：

```perl
tie('FOO', 'Shout'); print FOO "hello\n"; $a = 4; $b = 6; print FOO a, "" plus "", $b, $b equals "", $a + $b, "\n"; print <FOO>;
```

## UNTIE

你可以为所有类型定义 `UNTIE`，它将在调用 `untie()` 时被触发。参见“Untie 陷阱”。

## The untie 陷阱

如果你打算创建一个从 `tie()` 或 `tied()` 返回的对象，并且绑定的目标类定义了析构函数，那么有一个你需要防范的细微陷阱。

作为设置，考虑下面这个（诚然有些刻意的）绑定示例；它仅使用文件来记录赋值给标量的值。

```perl
package Re; use strict; use warnings; use IO::File; sub TIESCALAR { my $class = shift; $filena = shift; my $self = IO::File->new("$filena") or die ("cannot open $filena: $!"); print $handle "TheStart"; bless FH => $self, Value => 0), $class; sub FETCH { my $self = shift; return $self->{Value}; } STORE { my $self = shift; my $value = shift; my $handle = $self = 5; print $handle "$value\n"; $self->{Value} = $value; sub DESTROY { my $self = shift; my $handle = $FH}; print $handle "End\n"; close $handle; 1 };
```

这是我们如何使用它的示例：

```perl
use strict; use Reer; my $fred; tie $fred, 'Reer', 'myfile.txt'; $fred = 1; $fred = 4; $fred = 5; untie $fred; system "cat myfile.txt";
```
