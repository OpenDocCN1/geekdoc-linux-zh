
## 16.3.5 Globbing（文件名扩展与通配符）

如果你在 UNIX 或 MS-DOS 命令行上工作过，你就已经接触过用于扩展文件名的 shell 元字符。星号（*）用于匹配文件名中的所有字符，问号（?）用于匹配文件名中的一个字符，括号（[]）用于匹配文件名中字符集里的一个字符。将这些 shell 元字符扩展为文件名的过程称为 **globbing（文件名扩展）**。

如果文件名放在尖括号（即读取运算符）内，Perl 支持 globbing。不过，如今你应该使用内置的 `glob` 函数，如下图所示。此处保留该示例是为了让你明白，当遇到旧代码时，你能够理解其中发生的事情。

![](img/8556abcb353c0991f12099420ec28735_692_0.png)

### 说明

1.  在数组上下文中，globbing 操作执行完毕后，所有匹配文件的列表会被返回到数组 `@myfiles` 中。该列表包含所有以任意字符出现零次或多次开头，随后是一个句号，并以 1 到 5 之间的数字结尾的文件。
2.  打印匹配文件的列表。
3.  进入 `foreach` 循环。每次循环时，标量 `$file` 会被设置为下一个成功 glob 的文件：即任何以 p 开头，随后是任意两个字符，接着是数字 1，然后是 1 到 5 之间的数字，最后以任意字符出现零次或多次结尾的文件。
4.  如果该文件是文本文件（-T），则打印其名称。

**`glob` 函数。** 内置的 `glob` 函数执行的操作与 `<*>` 运算符相同，是你在进行文件名 globbing 时应使用的函数。它扩展文件名元字符的方式与 shell 相同，并返回扩展后的文件名。

### 示例 16.62

```perl
# (Command Line)
$ perl -e 'while(glob("p???[1-5]*")) { print "$_\n";}'
perl
perl2
perl3
perl4
perl5
```

```perl
# (In Script)
while ( glob("p???[1-5]*")) {
  print "$_\n";
}
```

**输出**

```
perl
perl2
perl3
perl4
perl5
```

### 说明

1.  在命令行中，`glob` 函数将 glob 当前工作目录下所有名称以 p 开头，随后是任意三个字符（???），接着是 1 到 5 之间的任意数字（[1-5]）的文件。每个匹配该表达式的文件名都会被赋值给 `$_`，然后被打印。
2.  这次，`glob` 是在脚本中使用的。其行为与第一个示例相同。
3.  打印扩展后的文件名。

## 16.4 错误处理

在许多情况下系统调用可能会失败；例如，当你试图打开一个不存在的文件，或者删除一个仍包含文件的目录，或者尝试读取你没有读权限的文件时。虽然我们之前的示例中使用过 `die` 函数，但现在我们将详细介绍错误处理以及可用于处理错误的函数。这些函数包括 `die` 函数、`warn` 函数和 `eval` 函数。

-   使用 `die` 函数在命令或文件句柄失败时终止 Perl 脚本。
-   `warn` 函数类似于 `die` 函数，但它不会退出脚本。
-   `eval` 函数有多种用途，但主要用于异常处理。

你可能记得 *短路（short-circuit）* 运算符 `&&` 和 `||` 会先计算左侧的操作数，然后计算右侧的操作数。如果 `&&` 左侧的操作数为 *真（true）*，则计算右侧。如果 `||` 左侧的操作数为 *假（false）*，则计算右侧。

### 16.4.1 Carp 模块

*死亡（die）* 有很多种方式。Perl 5 的 *Carp* 模块扩展了 *die* 和 *warn* 的功能。

**`die` 函数。** 如果系统调用失败，*die* 函数会向 *STDERR* 打印一个字符串，并以 `$!` 的当前值退出。`$!` 变量产生 *errno* 的当前值，这是包含表示系统错误数字的 UNIX 全局变量。*errno* 仅在系统调用 *失败* 时被更新。当系统调用失败时，会向 *errno* 分配一个代码数字以指示错误类型。如果字符串中省略了换行符，消息将与其行号一起打印。（完整列表请参阅 */usr/include/sys/errno.h*。）

以下是来自 */usr/include/sys/errno.h* 的一个示例：

```c
#define EPERM    1 /* Not owner */
#define ENOENT   2 /* No such file or directory */
#define ESRCH    3 /* No such process */
#define EINTR    4 /* Interrupted system call */
#define EIO      5 /* I/O error */
...
```

Win32 错误代码与 UNIX 错误代码不同，这使得依赖 `$!` 中返回的值变得不可能。有一些 Win32 扩展提供了自己的错误函数，以提供更有意义的结果。请参阅 ActiveState 附带标准 Perl 库中关于 Win32::*GetLastError* 的文档。

**格式**

```
die(LIST)
die LIST
die
```

**示例 16.63**

*（在脚本中）*

```perl
die "Can't cd to junk: $!\n" unless chdir "/usr/bin/junk";
```

*（输出）*

```
Can't cd to junk: No such file or directory
```

**说明**

1.  *chdir* 失败了。`$!` 包含来自 *errno* 的错误消息。换行符导致 *die* 函数后的字符串与 `$!` 变量的值一起打印。

**示例 16.64**

*（在脚本中）*

```perl
chdir '/Plop' or die "Stopped";
```

*（输出）*

```
Stopped at croak.perl line 4.
```

**说明**

1.  此示例产生的输出与上一个示例相同，但使用了不同的语法。如果 `chdir` 失败，则 *or* 右侧的 `die` 函数被执行。

**`warn` 函数。** `warn` 函数与 `die` 函数类似，区别在于程序会继续运行。如果 `die` 函数在 `eval` 块中被调用，则提供给 `die` 的参数字符串会被赋值给特殊变量 `$@`。在 `die` 之后，该变量可以作为参数传递给 `warn`，输出将发送到 STDERR。（参见第 16.4.2 节，“`eval` 函数”。）

### 16.4.2 `eval` 函数

使用 `eval` 函数进行异常处理；即捕获错误。`eval` 后面的块被处理和解析，就像一个独立的 Perl 程序一样，不同之处在于，在 `eval` 完成后，所有变量设置以及子程序和格式定义仍然保留。

`eval` 函数返回的值是最后评估的表达式之值。如果发生编译或运行时错误，或者执行了 `die` 语句，则返回一个未定义的值，并且一个特殊变量 `$@` 被设置为错误消息。如果没有错误，`$@` 是一个空字符串。

示例 16.65 展示了使用 `eval` 评估 Perl 表达式的例子。

**示例 16.65**

*（脚本）*

```perl
use warnings;
# The eval function will evaluate each line you type
# and return the result. It's as though you are
# running a little independent Perl script.
# Script name: ploh
my $result;
print "> ";       # Print the prompt
while(<STDIN>){
  $result=eval;   # eval evaluates the expression $_
  warn $@ if $@;  # If an error occurs, it will be assigned to $@
  print "$result\n" if $result;
  print "> ";     # Print the prompt
} # This line completes the while loop
```

**示例 16.65（续）**

*（输出）*

*（命令行）*

```
$ psh
> hello
hello
> bye
bye
> 5 + 4
9
> 8 / 3
2.66666666666667
> 5 / 0
illegal division by zero at (eval 5) line 3, <STDIN> line 5.
> 'Oh I see
Can't find string terminator '' '' anywhere before EOF at (eval 6) line 1, <STDIN> line
> exit
```

**说明**

1.  此行打印用户提示。这个程序就像一个小小的 Perl shell。它可以帮助你在将表达式放入程序之前对其进行评估，特别是当你不确定 Perl 将如何处理它时。
2.  进入 `while` 循环。每次进入循环时，它将读取用户的一行输入并赋值给 `$_`。
3.  不带参数的 `eval` 函数将评估 `$_` 中的表达式，并将评估结果赋值给 `$result`。
4.  如果 `eval` 发现语法错误或表达式评估导致系统错误，返回的错误消息将被赋值给 `$@` 变量。如果没有错误，`$@` 变量被赋值为空字符串。
5.  如果表达式成功评估，则打印结果。
6.  显示提示并重新进入循环。

接下来，我们将了解如何使用 `eval` 捕获程序中的错误。

**示例 16.66**

*（在脚本中）*

```perl
#!/bin/perl
print "Give me a number. ";
chop($a=<STDIN>);
print "Give me a divisor. ";
chop($b=<STDIN>);
eval{ die unless $answer = $a/$b };
warn $@ if $@;
printf "Division of %.2f by %.2f is %.2f\n",$a,$b,$answer if $answer;
print "I'm here now. Good-day!\n";
```

