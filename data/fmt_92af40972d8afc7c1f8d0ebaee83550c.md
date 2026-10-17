
| `x{n}` | 匹配字符 x 恰好出现 n 次。 |

| `x{n,}` | 匹配字符 x 出现 n 次或更多。 |

（续）

### 表 4-1（续）

| 表达式 | 含义 |

|---|---|

| `x{, m}` | 匹配字符 x 出现零次或最多 m 次。 |

| `x{n,m}` | 匹配字符 x 至少出现 n 次，但不超过 m 次。 |

| `$` | 匹配行的结尾。 |

| `\0` | 匹配空字符。 |

| `\b` | 匹配退格。 |

| `\B` | 匹配不在单词开头或结尾的任意字符。 |

| `\b` | 匹配单词的开头或结尾 — 当不在括号内时。 |

| `\cX` | 匹配 Ctrl-X（其中 X 为任意字母字符）。 |

| `\d` | 匹配单个数字。 |

| `\D` | 匹配非数字字符。 |

| `\f` | 匹配换页符。 |

| `\n` | 匹配换行（换行符）字符。 |

| `\ooo` | 匹配由数字 ooo 指定的八进制值（其中每个 o 为 0 到 7 之间的数字）。 |

| `\r` | 匹配回车。 |

| `\S` | 匹配非空白字符。 |

| `\s` | 匹配空白字符（空格、制表符或换行符）。 |

| `\t` | 匹配制表符。 |

| `\W` | 匹配非字母字符。 |

| `\w` | 匹配字母数字字符。 |

| `\xhh` | 匹配由数字 hh 指定的十六进制值（其中每个 h 为 0 到 f 之间的数字）。 |

| `^` | 匹配行的开头。 |

如果您想匹配字符 `$`、`|`、`*`、`^`、`[`、`]`、`\` 和 `/` 中的一个，您必须在要匹配的字符前加上反斜杠。因此，您应将这些字符输入为 `\$`, `\|`, `\*`, `\^`, `\[`, `\]`, `\\` 和 `\/`。由于奇怪的字符序列大量存在以及反斜杠的广泛使用，正则表达式看起来常常令人困惑。然而，就像其他任何事物一样，您可以从慢开始，起初只使用其中的几个特性。

到目前为止，我已经总结了正则表达式的语法。但我还没有展示如何在 Perl 中使用正则表达式。通常，您将正则表达式放在一对斜杠内，并使用匹配 (`=~`) 或不匹配

(`=~`) 和 (`!~`) 操作符用于测试字符串。你可以编写一个 Perl 脚本，其执行与本节前面使用 `grep` 完成的相同搜索。按照以下步骤完成此任务：

1. 使用文本编辑器输入并保存以下脚本到名为 `lookup` 的文件中：

```
#!/usr/bin/perl

while (<STDIN>)
{
    if ( $_ =~ /[bB]laster/ ) { print $_; }
}
```

2. 使用以下命令使 `lookup` 文件可执行：

```
chmod +x lookup
```

3. 使用以下命令尝试该脚本：

```
cat /usr/src/linux*/drivers/cdrom/sbpcd.c | ./lookup
```

在此情况下，`cat` 命令将特定文件的内容（正如你从 `grep` 示例中知道的，该文件包含一些带有正则表达式的行）馈送给 `lookup` 脚本。脚本 simply 应用 Perl 的正则表达式匹配操作符 (`=~`) 并打印任何匹配的行。输出应与使用以下命令显示的 `grep` 命令类似：

```
grep "[bB]laster" /usr/src/linux*/drivers/cdrom/sbpcd.c
```

`lookup` 脚本中的 `$_` 变量需要一些解释。 `<STDIN>` 表达式从标准输入获取一行，默认情况下将该行存储在 `$_` 变量中。在 `while` 循环内部，正则表达式与 `$_` 字符串进行匹配。以下单个 Perl 语句完成了 `lookup` 脚本的工作：

```
if ( $_ =~ /[bB]laster/ ) { print $_; }
```

```
while (<STDIN>)
{
    if ( $_ =~ /\\n/ && $_ =~ /^ {7}\S/ ) { print $_; }
}
```

## 流程控制语句

到目前为止，你看到的 Perl 语句旨在按串行方式执行，一个接一个。Perl 还包括能够控制语句执行流程的语句。你已经看到过 `if` 语句和 `while` 循环。Perl 包含一套完整的流程控制语句，就像 C 中的一样，但有一些额外的特性。

在 Perl 中，所有条件语句采用以下形式：

```
conditional-statement
{ Perl code to execute if conditional is true }
```

请注意，你必须用大括号 (`{...}`) 括起条件语句后面的代码。条件语句检查表达式的值以确定是否执行大括号内的代码。在 Perl 中，与 C 相同，任何非零值都被视为逻辑真，而零值则为假。

接下来我简要描述 Perl 中主要条件语句的语法。

### if 和 unless

Perl 的 `if` 语句类似于 C 的 `if` 语句。例如，`if` 语句可以检查计数是否超过阈值，如下所示：

```
if ( $count > 25 ) { print "Too many errors!\n"; }
```

你可以向 `if` 语句添加 `else` 子句，如下所示：

```
if ($user eq "root")
{
    print "Starting simulation...\n";
}
else
{
    print "Sorry $user, you must be \"root\" to run this program.\n";
    exit;
}
```

如果你熟悉 C，你可以看到 Perl 的语法与 C 非常相似。`if` 语句的条件可以有零个或多个 `elsif` 子句以处理更多备选情况，如下所示：

```
print "Enter version number:"; # prompt user for version number

$os_version = <STDIN>;   # read from standard input
chop $os_version; # get rid of the newline at the end of the line
# Check version number
if ($os_version > 10 ) { print "No upgrade necessary\n";}
elsif ($os_version > 6 && $os_version < 9)
{ print "Standard upgrade\n";}
elsif ($os_version > 3 && $os_version < 6 ) { print "Reinstall\n";}
else { print "Sorry, cannot upgrade\n";}
```

![](img/a7eec43a54473e95dc5ea333fecf1bd7_822_0.png)

`unless` 语句是 Perl 独有的。该语句的形式与 `if` 相同，包括使用 `elsif` 和 `else` 子句。不同之处在于 `unless` 仅在条件为假时执行其语句块。例如，你可以在以下代码中使用 `unless`：

```
unless ($user eq "root")
{
    print "You must be \"root\" to run this program.\n";
    exit;
}
```

在这种情况下，除非字符串 `user` 是 `"root"`，否则脚本会退出。

### while

使用 Perl 的 `while` 语句进行循环——在现有条件变为逻辑假之前重复某些处理。要逐行从标准输入读取并处理该行，可以使用以下 `while` 循环：

```
while ($in = <STDIN>)
{
# Code to process the line
    print $in;
}
```

![](img/a7eec43a54473e95dc5ea333fecf1bd7_822_1.png)

如果你在不带任何参数的情况下从标准输入读取，Perl 会将标准输入的当前行分配给 `$_` 变量。因此，你可以按如下方式编写前面的 `while` 循环：

```
while (<STDIN>)
{
# Code to process the line
    print $_;
}
```

Perl 的 `while` 语句比 C 的更灵活，因为你可以用几乎任何东西作为要测试的条件。例如，如果你使用数组作为条件，`while` 循环会一直执行直到数组没有元素剩余，如以下示例所示：

```
# Assume @cmd_arg has the current set of command arguments
while (@cmd_arg)
{
$arg = shift @cmd_arg; # this extracts one argument
# Code to process the current argument
print $arg;
}
```

`shift` 函数移除数组的第一个元素并返回该元素。

你可以使用 `next` 关键字跳到循环的末尾；`last` 关键字退出循环。例如，以下 `while` 循环将 1 到 10 的数字相加，跳过 5：
