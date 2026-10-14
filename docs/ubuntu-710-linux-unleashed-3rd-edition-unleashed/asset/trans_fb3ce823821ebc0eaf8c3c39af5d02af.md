

## until

until 与 while 语句截然相反。只要特定条件为假，它就会执行一个语句块——或者说，直到该条件变为真为止：

```
until (ValidPassword($user, $password)) {
    print "You've entered an invalid password. Please try again.\n";
    $password = GetPassword;
}
```

## last 和 next

你可以使用 last 语句强制 Perl 提前结束循环。last 类似于 C 语言的 break 命令——循环被退出。如果你决定需要跳过循环的剩余内容但不结束循环本身，可以使用 next，它类似于 C 语言的 continue 命令。遗憾的是，这些语句不适用于 do ... while。

另一方面，你可以使用 redo 跳转到某个循环（由标签标记）或跳转到循环内部被调用的位置：

```
$a = 100;
while (1) {
    print "start\n";
    TEST: {
        if (($a = $a / 2) > 2) {
            print "$a\n";
            if (-$a < 2) {
                exit;
            }
            redo TEST;
        }
    }
}
```

在这个简单的示例中，变量 $a 在一个无限循环中被反复操作和测试。单词 start 只会被打印一次。

## do ... while 和 do ... until

while 和 until 循环会先对条件进行求值。通过在条件前加上 do 块，可以改变这一行为。使用 do 块时，条件在最后才被求值，这导致块中的内容至少总会执行一次（即使条件为假）。这与 C 语言的 do ... while (conditional) 语句类似。

## 正则表达式

Perl 最大的优势在于文本和文件处理，这通过使用正则表达式（regex）库来实现。正则表达式与 shell 的通配符处理和文件名展开功能（参见第 15 章）截然不同，它能够高效且轻松地完成复杂的模式匹配和替换。

例如，下面这行代码会将一行文本中所有出现的字符串 bob 或 mary 替换为 fred：

```
$string =~ s/bob|mary/fred/gi;
```

在不深入过多细节的情况下，表 23.7 解释了上述代码行的含义。

表 23.7 对 `$string =~ s/bob|mary/fred/gi;` 的说明

| 元素 | 说明 |
|---|---|
| $String =~ | 对名为 $string 的变量中的文本执行此模式匹配。 |
| s | 替换。 |
| / | 开始要匹配的文本。 |
| bob\|mary | 匹配文本 bob 或 mary。你应该记住，它寻找的是文本 mary，而不是单词 mary；也就是说，它也会匹配 maryland 这个词中的 mary 文本。 |
| / | 结束要匹配的文本；开始用于替换的文本。 |
| fred | 将所有匹配到的内容替换为文本 fred。 |
| / | 结束替换文本。 |
| g | 全局执行此替换；也就是说，无论该匹配文本在字符串中出现在哪里，都将其替换（并可替换任意多次）。 |
| i | 搜索文本不区分大小写。它能匹配 bob、Bob 或 bOb。 |
| ; | 表示这行代码的结束。 |

如果你对这些细节感兴趣，可以通过手册中的 regex（7）部分获取更多信息。

虽然将一个字符串替换为另一个字符串看起来可能是一项相当琐碎的任务，但在其他语言（例如 C）中，除非有来自外部库的额外子例程支持，否则完成同样事情所需的代码相当令人望而生畏。

## 访问 Shell

Perl 可以为你执行任何你通常通过反引号（``）语法向 shell 键入命令来执行的过程。例如，清单 23.4 中的代码会打印一个目录列表。

## 清单 23.4 使用反引号访问 Shell

```
$curr_dir = `pwd`;
@listing = `ls -al`;
print "Listing for $curr_dir\n";
foreach $file (@listing) {
    print "$file";
}
```

### 注意

`` ` `` 符号使用的是 Tab 键上方（在大多数键盘上）的反引号，而不是单引号。

你还可以使用 Shell 模块来访问 shell。Shell 是 Perl 附带的标准模块之一；它允许创建和使用类似 shell 的命令行。请看下面的代码示例：

```
use Shell qw(cp);
cp ("/home/httpd/logs/access.log", "/tmp/httpd.log");
```

这段代码看起来几乎像是直接把命令行函数导入到了 Perl 中。虽然实际上并非如此，但你可以把这段代码当作类似命令行来处理，并在你的 Perl 程序中使用这种方法。

访问 shell 的第三种方法是通过 system 函数调用：

```
$rc = 0xffff & system('cp /home/httpd/logs/access.log /tmp/httpd.log');
if ($rc == 0) {
    print "system cp succeeded \n";
} else {
    print 'system cp failed $rc\n';
}
```

该调用也可以与 or die 子句一起使用：

```
system('cp /home/httpd/logs/access.log /tmp/httpd.log') == 0
or die 'system cp failed: $?';
```

但是，你无法捕获通过 system 函数执行的命令的输出。

## 模块与 CPAN

Perl 社区（以及 Linux 社区）的一个巨大优势在于它是一个开源社区。这种社区支持通过

