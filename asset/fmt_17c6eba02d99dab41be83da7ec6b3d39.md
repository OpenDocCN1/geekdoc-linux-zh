
```
Command Prompt - perl -d figure12.5code.pl
D:\book\-d figure12.5code.pl
Default die rest.

Loading routines db.pl version 1.07
Editor available.

Enter h or 'h h' for help, or 'perldebug' for more help.
main(figure12.5code.pl:2):  $a = 15;
2=>    $a = 15;
3>    while ($a < 25){
4:        $a++
5:        last if ($a = 20);
6:        print "$a is still less than 25 \n";
7:    }
8:    print "exiting";
9>DB<1> -
```

### 图 12-6 使用 l 命令

正如你在图 12-6 中看到的，整个程序都列出来了，而且由于我们还没有在程序中执行第一行之后的内容，占位符 `=>` 显示我们位于程序的第二行。如果你知道想显示的确切行号，可以按照如下方式输入：

```
DB(1) 5
```

### 注意

我们将以与之前相同的方式显示几个选项，以避免本节有过多的截图。我们建议你在程序上打开调试器，并在我们涵盖这些命令时发布它们。

# 406 Perl：学者指南

此选项会列出调试器当前正在使用的程序的第五行。你也可以使用此程序来重置 `l` 命令。请记住，`l` 命令按顺序每次列出程序的十行。如果你列出了第1到第10行以及11到到20行，你可以通过先发布 `l 1` 从头开始，然后使用 `l` 列出其余行。除了可以显示单行外，你还可以使用以下命令指定一次要显示的行号范围：

```
DB(2) 1 5-8
```

此命令列出你程序的第5到第8行。你也可以使用以下命令列出第5到8行：

```
DB(3) 1 5+3
```

此命令告诉调试器从第5行开始，并显示该行及其接下来的三行。

如果你的程序中有子程序，你可以使用 `l` 命令加上子程序的名称来跳转并显示它。如果你想显示之前已经显示的行或多行，可以使用以下命令：

```
DB(4) –
```

图 12-7 显示了 `-` 命令的使用。如从图 12-7 所示，`-` 命令并没有显示之前显示的确切行数，但这些行将包含在显示的十行之中。

`w` 命令可以用于显示程序的十行，其中一行是指定的行号。你也可以用 `l` 命令实现此，但使用 `w` 会让你操作更方便。以下是发布 `w` 命令的示例：

```
DB(5) w
```

# 第12 节：错误消息与调试 | 407

```
Command Prompt - perl figure12.5code.pl
D:\Perl>perl -d figure12.5code.pl
Default de handler restored.

Loading DB routines from perl5db.pl version 1.07
Editor trace enabled.

Enter h h h for help, or perldoc perldebug for more help.
main::(figure12.5code.pl:2) -> sa = 15;
DB2(1) i = -6
2: -> sa = 15;
3:     while (sa < 25) {
4:         sa++;
5:         last if (sa <= 20);
6:         print "sa is still less than 25 \n";
7:     }
8:     print "exiting";
9:     #1
10:    #2
11:    #3
12:    #4
13:    #5
14:    #6
15:    #7
16:    #8
DB2(2) -> /usr/bin/perl
2: -> sa = 15;
3:     while (sa < 25) {
4:         sa++;
5:         last if (sa <= 20);
6:         print "sa is still less than 25 \n";
7:     }
8:     print "exiting";
9:     #1
10:    #2
DB2(2) -
```

![](img/2070407c4a70134aab89572f10d21e60_430_0.png)

让我们看看这个命令在较长测试程序上的输出。以下是接几个示例中我们使用的程序：

```
#!/usr/bin/perl
$hash1 = (a, 1, b, 2, c, 3, d, 4);
$value = $hash1(a);
print "The value stored under the key a is $value \n";
$value2 = $hash1(c);
print "The value stored under the c key is $value1 \n";
$hash1e = 5;
$value2 = $hash1(e);
print "The value stored under the newly created e key is $value2 \n";
$hash2f = 5;
$value3 = $hash2(f);
print "The value stored in the new hash under the f key is $value3 \n";
@array = %hash1;
print "The contents of %hash1 are @array \n";
```

从图 12-8 可以看出，`w` 命令列出了指定行号之前的三行和之后的六行。它显示之前的三行代码的原因仅仅是为了让你更好地了解到指定行为止已经执行了什么。这在你尝试调试某个语句时会有帮助。

到目前为止，我们向你展示了在调试器中列出程序的几种方法，但还没有告诉你如何退出。这可以通过简单使用 `q` 命令来实现，发布 `q` 命令会处理调试器并返回到发布 `-d` 命令时所在目录的命令行。如果你停止了某个程序的调试并立即重新进入该程序的调试器，所有内容将重置为初始状态。

在单步执行程序之前还需要涵盖更多选项。这些选项对于调试大型程序很有帮助。第一个讨论的选项是搜索选项。

```
Command Prompt - perl -d figure24.code.pl
D:\Perbook\perl -d figure24.code.pl
Default handler restored.
Loading DB routines for perl5db.pl version 1.07
Editor trace enabled.

Enter h h h for help, or perldoc perldebug for more help.
main::(figure24.code.pl:12) $hash1 = <a, 1. b. 2. c. 3. d. 4>;
3: -> $value = $hash1(a);
4:     print "The value stored under the key a is $value \n";
5: -> $value = $hash1(b);
6:     print "The value stored under the key b is $value \n";
7: -> $value = $hash1(c);
8:     $value2 = $hash1(e);
9:     print "The value stored under the newly created e key is $value2 \n";
10: -> $value3 = $hash2(f);
11:     print "The value stored in the new hash under the f key is $value3 \n"
DB<2>
```

![](img/2070407c4a70134aab89572f10d21e60_431_0.png)
# 第12 节：错误消息与调试 | 409

搜索选项可用于程序中搜索字符串。使用此选项时不需要指定行号，你只需要提供要在程序中搜索的字符串。搜索字符串听起来熟悉吗？搜索字符串与正则表达式相似，实际上你实现程序时也采用了类似的操作。要搜索的字符串必须用斜杠 `/` 包围。以下是发布此命令的示例，图 12-9 显示了屏幕输出：

```
DB(6) /key/
```

在图 12-9 中，我们正在搜索 "key"。程序中多次出现此字符串；要显示后续，可以重新输入搜索命令。如果你想从程序结尾搜索指定的字符串，你只需要用问号 `?` 代替斜杠。此命令也会从头开始

![](img/2070407c4a70134aab89572f10d21e60_432_0.png)
