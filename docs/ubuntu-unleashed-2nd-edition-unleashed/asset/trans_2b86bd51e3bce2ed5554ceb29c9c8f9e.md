

## until

until 与 while 语句恰好相反。它只要某个条件为假——或者说，直到该条件变为真——就会执行一段语句：

```
until (ValidPassword($user, $password)) {
    print "You've entered an invalid password. Please try again.\n";
    $password = GetPassword;
}
```

## last and next

你可以通过使用 last 语句强制 Perl 提前结束循环。last 类似于 C 语言的 break 命令——循环被退出。如果你决定需要在不结束循环本身的情况下跳过循环的剩余内容，可以使用 next，它类似于 C 语言的 continue 命令。不幸的是，这些语句不能与 do ... while 一起使用。

另一方面，你可以使用 redo 跳转到一个循环（由标签标记）或在调用处进入循环内部：

```
$a = 100;
while (1) {
    print "start\n";
    TEST: {
        if (($a = $a / 2) > 2) {
            print "$a\n";
            if (--$a < 2) {
                exit;
            }
            redo TEST;
        }
    }
}
```

在这个简单示例中，变量 $a 在一个无限循环中被反复操作和测试。单词 start 只会被打印一次。

## do ... while and do ... until

while 和 until 循环先评估条件。通过在条件之前应用 do 块，行为会发生变化。有了 do 块，条件最后才会被评估，这导致块的内容始终至少执行一次（即使条件为假）。这类似于 C 语言的 do ... while (conditional) 语句。

## Regular Expressions

Perl 最大的优势在于文本和文件处理，这通过使用正则表达式（regex）库来实现。正则表达式与 shell 的通配符处理和文件名展开功能（参见第 15 章）大不相同，它们允许以高效且简便的方式进行复杂的模式匹配和替换。

例如，下面的代码行会将文本行中出现的每个字符串 bob 或字符串 mary 替换为 fred：

```
$string =~ s/bob|mary/fred/gi;
```

不深入太多细节，表 27.7 解释了前一行代码的含义。

TABLE 27.7 Explanation of $string =~ s/bob|mary/fred/gi;

| Element | Explanation |
|---|---|
| $String =~ | 对名为 $String 的变量中的文本执行此模式匹配。 |
| s | 替换。 |
| / | 开始要匹配的文本。 |
| bob\|mary | 匹配文本 bob 或 mary。你应该记住它是在查找文本 mary，而不是单词 mary；也就是说，它也会匹配单词 maryland 中的文本 mary。 |
| / | 结束要匹配的文本；开始要替换它的文本。 |
| fred | 用文本 fred 替换任何匹配的内容。 |
| / | 结束替换文本。 |
| g | 全局执行此替换；也就是说，无论在字符串中匹配多少次，都替换匹配的文本。 |
| i | 搜索文本不区分大小写。它匹配 bob、Bob 或 b0B。 |
| ; | 表示代码行的结束。 |

如果你对细节感兴趣，可以使用手册中的 regex (7) 部分获取更多信息。

尽管将一个字符串替换为另一个字符串看起来可能是一项相当琐碎的任务，但在另一种语言（例如 C）中完成相同任务所需的代码如果没有外部库提供的额外子程序支持，则相当令人望而生畏。

## Access to the Shell

Perl 可以通过 `` 语法为你执行任何你通常通过向 shell 输入命令来执行的进程。例如，清单 27.4 中的代码会打印目录列表。

## LISTING 27.4 Using Backticks to Access the Shell

```
$curr_dir = `pwd`;
@listing = `ls -al`;
print "Listing for $curr_dir\n";
foreach $file (@listing) {
    print "$file";
}
```

### NOTE

`` 记法使用的是大多数键盘上 Tab 键上方的反引号，而不是单引号。

你也可以使用 Shell 模块来访问 shell。Shell 是随 Perl 一起提供的标准模块之一；它允许创建和使用类似 shell 的命令行。看下面的代码示例：

```
use Shell qw(cp);
cp ("/home/httpd/logs/access.log", "/tmp/httpd.log");
```

这段代码几乎看起来像是直接将命令行函数导入到 Perl 中。虽然实际上并非如此，但你可以假装代码类似于命令行，并在你的 Perl 程序中使用这种方法。

访问 shell 的第三种方法是通过 system 函数调用：

```
$rc = 0xffff & system('cp /home/httpd/logs/access.log /tmp/httpd.log');
if ($rc == 0) {
    print "system cp succeeded \n";
} else {
    print "system cp failed $rc\n";
}
```

该调用也可以与 or die 子句一起使用：

```
system('cp /home/httpd/logs/access.log /tmp/httpd.log') == 0
    or die 'system cp failed: $?';
```

然而，你无法捕获通过 system 函数执行的命令的输出。

## Modules and CPAN

Perl 社区（以及 Linux 社区）的一大优势是它是一个开源社区。这种社区支持通过以下方式在 Perl 中体现出来

