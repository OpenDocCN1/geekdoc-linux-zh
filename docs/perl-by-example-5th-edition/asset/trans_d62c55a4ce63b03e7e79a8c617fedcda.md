

## 解释

- 1 `$!` 变量保证在每条打印语句执行后自动刷新输出缓冲区。（参见附录 A 中的 auto/flush 模块，“Perl 内置函数、程序、模块和调试器”。）
- 2 标量 `$tmpl` 被赋值为 temp，以便稍后用作输出文件。
- 3 打开数据文件用于读取，并将其附加到 DB 文件句柄。
- 4 正在将 STDOUT 复制并保存到一个名为 SAVED 的另一个文件句柄中。在后台，文件描述符正在被操作。
- 5 正在打开 tmp 文件用于写入，并将其分配给通常预留给 STDOUT（即屏幕）的文件描述符。STDOUT 的文件描述符已关闭并针对 temp 重新打开。
- 6 输出过滤器将被分配给 SORT。Perl 的输出将被发送到 sort 实用程序，该实用程序在 Windows 和 UNIX 上都能工作，用于从行首开始按字母顺序排序。
- 7 `$db` 文件句柄被打开用于读取。
- 8 输出文件句柄将在排序后发送到 tmp 文件。
- 9 关闭循环。
- 10 关闭管道。
- 11 打开标准输出文件句柄，以便将输出重定向回屏幕。
- 12 由于 STDOUT 已被重新分配回屏幕，因此这一行会打印到屏幕上。
- 13 将 tmp 文件重命名为 data，用 tmp 的内容覆盖 data 中的内容。

### 输入过滤器

在使用 open 函数创建文件句柄时，你还可以打开一个过滤器，以便将其管道连接到 Perl。操作系统 shell 通常处理处理过程中需要解释的任何特殊字符。

如果你不需要 shell 来处理管道中的命令（即你未使用重定向、通配符展开或多个管道），你可以使用之前示例 10.30 中所示的三参数格式。参见图 10.3。

## 格式

```perl
open (FILEHANDLE, COMMAND) ;
open (FILEHANDLE, "- | ", COMMAND) ;
```

## 示例 10.33

```perl
use warnings;
# $filename: $infile
1 open (INPIPE, "date *$D*" ) ; # Windows 用法: date /T
2 $today = <$INPIPE> ;
3 print $today;
4 close (INPIPE);
5 open (my $pipe, "- | ", "date *$D*" ) ; # 三个参数
6 $today = <$pipe> ;
print $today;
close $pipe ;
```

### 输出

Sun Feb 18 14:12:44 PST 2014

### 解释

- 1 用户定义的管道句柄 `$INPIPE` 将用于将命令的输出作为输入管道到 Perl。UNIX *date* 命令的输出将通过 *INPIPE* 管道句柄用作你的 Perl 脚本的输入。Windows 用户，请使用 *date /t*。
- 2 标量 `$today` 将从 *INPIPE* 管道句柄接收输入；换句话说，Perl 从 *INPIPE* 读取。
- 3 UNIX *date* 命令的值被赋值给 `$today` 并显示。
- 4 使用完管道句柄后，使用 close 函数关闭它。这保证命令在脚本退出前完成。如果你不关闭管道句柄，输出可能无法正确刷新。
- 5 此格式在 5.6 版本中可用。它允许你创建词法作用域的管道句柄，这些句柄将在句柄超出作用域时关闭。
- 6 现在 Perl 从管道读取，将 UNIX *date* 命令的输出存储在 `$today` 中。

![](img/8556abcb353c0991f12099420ec28735_360_0.png)

## 示例 10.34

### 脚本

```perl
use warnings;
open(LISTDIR, "ls \*" ) or
die "PIPE failed $!\n";  # 参见下一个示例了解 Windows 用法
while( $filename = <LISTDIR> ) {
    print $filename;
}
```

### 输出

    3  ./per12
       ./per13
       ./per1.man
       ./per1.arg

### 解释

- 1 UNIX ls 命令的输出将作为输入管道到 LISTDIR。当包含在尖括号中时，标准输入将来自 LISTDIR。如果 open 失败，die 操作符将打印 PIPE failed! 并退出脚本。
- 2 UNIX ls 命令的输出已管道到 LISTDIR。对于 while 循环的每次迭代，LISTDIR 中的一行将被赋值给标量变量 `$filename` 并打印。

## 示例 10.35

### 脚本

```perl
use warnings;
# 在 Win32 平台上打开输入过滤器
1 open(LISTDIR, 'dir "C:\perl" |') || die $!;
2 @filelist = <LISTDIR>;
3 foreach $file ( @filelist ){
    print $file;
}
```

### 输出

Volume in drive C is O10599
Volume Serial Number is 2237-130A

Directory of C:\perl

03/31/1999 10:34p   <DIR>  ..
03/31/1999 10:34p   <DIR>  .
03/31/1999 10:37p          30,366 DeisL1.su
03/31/1999 10:34p   <DIR>  bin
03/31/1999 10:34p   <DIR>  lib
03/31/1999 10:35p   <DIR>  html
03/31/1999 10:35p   <DIR>  eg
03/31/1999 10:35p   <DIR>  site
       1 File(s)   30,366 bytes
       7 Dir(s)   488,873,984 bytes free

### 解释

- 1 Windows dir 命令的输出将管道到 LISTDIR。当包含在尖括号中时，标准输入将来自 LISTDIR。如果 open 失败，die 操作符将打印错误并退出脚本。
- 2 Windows dir 命令的输出已管道到管道 `$LISTDIR`。从管道读取输入并赋值给数组 `@filelist`。数组的每个元素代表一行输入。
- 3 foreach 循环遍历数组，一次打印一行，直到数组结束。

# 10.3 传递参数

Perl 如何将命令行参数传递给 Perl 脚本？如果你来自 C、C++、awk 或 C shell 背景，乍一看你可能会想：“哦，我已经知道这个！”小心！有一些细微的差别。所以，请继续阅读。

## 10.3.1 @ARGV 数组

Perl 确实将参数存储在一个名为 `@ARGV` 的特殊数组中。下标从零开始，与 C 和 awk 不同，`$ARGV[0]` 不代表程序名称；它代表脚本名称后的第一个单词。与 shell 语言一样，`$0` 特殊变量用于保存 Perl 脚本的名称。与 C shell 不同，`$#ARGV` 表达式包含数组中最后一个下标的编号，而不是数组中元素的数目。参数的数量是 `$#ARGV + 1`。`$#ARGV` 的初始值为 -1。要获取 `@ARGV` 数组的大小，最简单的方法是只说 `scalar @ARGV`。

当 ARGV（文件句柄）被包含在尖括号中时，`<ARGV>`，命令行参数被视为文件名。文件名被分配给 ARGV，`@ARGV` 数组立即向左移动一位，从而缩短 `@ARGV` 数组。

从 `@ARGV` 数组移位出去的值被分配给 `$ARGV`。`$ARGV` 包含当前选定文件句柄的名称。参见图 10.4。

![](img/8556abcb353c0991f12099420ec28735_362_0.png)

图 10.4 ARGV 的多种面貌。

## 示例 10.36

### 脚本

```perl
#!/usr/bin/env perl
use warnings;

die "$0 requires an argument.\n" unless @ARGV;

1
die "$0 requires an argument.\n" unless @ARGV;
2
print "@ARGV\n";    # 必须至少有一个参数
3
print "@$ARGV[0]\n"; # 打印所有参数
4
print "@$ARGV[1]\n"; # 打印第一个参数
5
print The number of arguments is ", scalar @ARGV, ".\n";
6
print "There are ", $#ARGV + 1, " arguments.\n";
7
print "@$ARGV[$#ARGV] is the last one.\n"; # 打印最后一个参数
```

### 输出

$ perl.aarg
2 perl.arg requires an argument.

$ perl.arg fl f2 f3 f4 f5
2 f1 f2 f3 f4 f5
3 f1
4 f2
5 The number of arguments is 5.
6 There are 5 arguments.
7 f5 is the last one.

### 解释

- 1 如果没有命令行参数，执行 die 函数并终止脚本。`$0` 特殊变量保存 Perl 脚本的名称，即 perl.arg。
- 2 打印 `@ARGV` 数组的内容。
- 3 打印第一个参数，而不是脚本名称。
- 4 打印第二个参数。
- 5 标量函数在标量上下文中计算表达式；也就是说，它返回数组 `@ARGV` 的大小。
- 6 `$#ARGV` 变量包含最后一个索引值的数字。由于索引从零开始，`$#ARGV + 1` 是参数的总数（不包括脚本名称）；也是数组的大小。
- 7 由于 `$#ARGV` 包含最后一个索引值，`@$ARGV[$#ARGV]` 是 `@ARGV` 数组中最后一个元素的值。

## 10.3.2 ARGV 和空文件句柄

当在循环表达式中使用并包含在输入尖括号（<>）中时，`@ARGV` 数组的每个元素都被视为一个特殊的文件句柄。Perl 遍历数组，将数组的每个元素存储在变量 `$ARGV` 中。一组空的尖括号使用空文件句柄，Perl 隐式地将 ARGV 数组的每个元素用作文件句柄。

