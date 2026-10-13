
请注意，在这个特定示例中，赋给 `address` 的值是用单引号还是双引号括起来并没有区别。无论哪种情况，shell 都会显示辅助命令提示符，表示它正在等待对应的右引号。

将两行地址赋给 `address` 之后，`echo` 会显示该变量的值。如果不给变量加引号，地址会显示在一行中。原因与导致

```text
echo one        two      three    four
```

显示为

```text
one two three four
```

的原因相同。

因为 shell 会从命令行中删除空格、制表符和换行符（空白字符），然后在将命令行交给所请求的命令之前将其拆分成参数，所以命令

```sh
echo $address
```

会使 shell 去除内嵌的换行符，将它当作空格或制表符一样的参数分隔符来处理。然后 shell 将九个参数传给 `echo` 显示。`echo` 永远看不到那个换行符；shell 先一步处理了它（见图 5.5）。

![](img/29b87b4d3daf7eb41fe5066130730f4c_129_0.png)

图 5.5  `echo $address`

而当使用命令

```sh
echo "$address"
```

时，shell 与之前一样替换 `address` 的值，只是双引号告诉它保留任何内嵌的空白字符。因此在这种情况下，shell 传给 `echo` 的是单个参数——一个包含内嵌换行符的参数。然后 `echo` 显示它的这一个参数。图 5.6 展示了这一点，其中换行符用序列 `\n` 表示。

![](img/29b87b4d3daf7eb41fe5066130730f4c_130_0.png)

图 5.6  `echo "$address"`

有一点比较奇怪的是，双引号可以用来对 shell 隐藏单引号，反之亦然：

```sh
$ x="'Hello,' he said"
$ echo $x
'Hello,' he said
$ article="'Keeping the Logins from Lagging,' Bell Labs Record"
$ echo $article
'Keeping the Logins from Lagging,' Bell Labs Record
$
```

## 反斜杠

从功能上讲，反斜杠（用作前缀）等价于将单个字符放在单引号中，不过有少数细微的例外。反斜杠会*转义*紧随其后的字符。通用格式如下：

```sh
\c
```

其中 *c* 是你要加引号的字符。该字符通常附带的任何特殊含义都会被移除。下面是一个例子：

```sh
$ echo >
syntax error: 'newline or ;' unexpected
$ echo \>
>
$
```

在第一种用法中，shell 看到 `>`，以为你想将 echo 的输出重定向到文件，因此它期望后面跟着一个文件名。由于后面没有文件名，shell 便输出了错误信息。

在接下来的用法中，反斜杠转义了 `>` 的特殊含义，于是它被当作一个要显示的字符传给 echo。

```sh
$ x=*
$ echo \$x
$x
$
```

在这种情况下，shell 会忽略反斜杠后面的 `$`，因此不会执行变量替换。

因为反斜杠会移除后面字符的特殊含义，你能猜到如果后面的字符是另一个反斜杠，会发生什么吗？它会移除那个反斜杠的特殊含义：

```sh
$ echo \\\\
\\
$
```

你也可以使用单引号来完成这个任务：

```sh
$ echo '\\'
\\
$
```

### 使用反斜杠续行

正如本节开头提到的，`\c` 基本上等同于 `'c'`。这个规则的一个例外是，当反斜杠正好是一行中的最后一个字符时：

```sh
$ lines=one'
> 'two
$ echo "$lines"
one
two
$ lines=one\
> two
$ echo "$lines"
onetwo
$
```

> 单引号告诉 shell 忽略换行符

> 试试改用 `\`

当反斜杠是输入行的最后一个字符时，shell 会将它视为续行符。它会移除后面的换行符，并且不会把该换行符当作参数分隔符（就好像它从未被输入过一样）。这种结构通常用于跨多行输入长命令。

例如，下面的写法完全有效：

```text
Longinput="The shell treats a backslash that's the \
last character of a line of input as a line \
continuation. It removes the newline too."
```

### 双引号内的反斜杠

我们前面提到过，反斜杠是 shell 在双引号内会解释的三种字符之一。这意味着你可以在双引号内使用反斜杠，来移除那些在双引号内本来会被解释的字符的含义（也就是其他反斜杠、美元符号、反引号、换行符以及其他双引号）。如果反斜杠在双引号内位于任何其他字符之前，shell 会忽略这个反斜杠，并将它传给程序：

```sh
$ echo "\$x"
$x
$ echo "\ is the backslash character"
\ is the backslash character
$ x=5
$ echo "The value of x is \"$x\""
The value of x is "5"
$
```

在第一个示例中，反斜杠位于美元符号之前，因此 shell 会忽略美元符号，移除反斜杠，并把结果交给 echo。在第二个示例中，反斜杠位于空格之前，而空格在双引号内不会被 shell 解释。所以 shell 会忽略反斜杠，并将它传给 echo 命令。最后一个示例展示了反斜杠在双引号字符串内用来括起双引号。

作为引号用法的一个练习，假设你想在终端上显示下面这一行：

```text
<<< echo $x >>> displays the value of x, which is $x
```

这里的意图是：在第二处 `$x` 中替换 x 的值，但第一处不替换。先给 x 赋一个值：

```sh
$ x=1
$
```

现在尝试不使用任何引号来显示这一行：

```sh
$ echo <<< echo $x >>> displays the value of x, which is $x
syntax error: '<' unexpected
$
```

`<` 向 shell 表示输入重定向，但后面缺少文件名，因此产生了错误信息。

如果你把整条消息放在单引号内，最后那处 x 的值不会被替换。如果你把整个字符串放在双引号内，两处 `$x` 都会被替换。有点棘手！

下面给出了两种不同的方法，可以正确地为这个字符串加引号，让一切都按预期工作：

```sh
$ echo "<<< echo \$x >>> displays the value of x, which is $x"
<<< echo $x >>> displays the value of x, which is 1
$ echo '<<< echo $x >>> displays the value of x, which is' $x
<<< echo $x >>> displays the value of x, which is 1
$
```

在第一种情况下，所有内容都用双引号括起来，并用反斜杠来防止 shell 在第一处 `$x` 中执行变量替换。在第二种情况下，直到最后一处 `$x` 之前的所有内容都用单引号括起来，但需要被替换的那个变量在添加时没有加引号。

然而，后一种方案有一点风险：如果变量 `x` 中包含文件名替换或空白字符，这些字符会被解释。更安全的 echo 写法应该是：

```sh
echo '<<< echo $x >>> displays the value of x, which is' "$x"
```

## 命令替换

*命令替换*是指 shell 在命令行的任意位置，用指定命令的输出来替换该命令的能力。shell 中有两种执行命令替换的方式：将命令括在反引号中，或用 `$(...)` 结构将其括起来。

### 反引号

反引号——常被称为“back tick”——不同于之前遇到的任何类型的引号，因为它的目的不是保护字符不受 shell 影响，而是告诉 shell 用所括命令的输出来替换该命令。使用反引号的一般格式是：

```text
`command`
```

其中 *command* 是要执行的命令名，该命令的输出将被插入到相应位置。

> **注意**
>
> 使用反引号进行命令替换已不再是首选方法；不过，我们在这里介绍它，是因为大量旧版 shell 脚本仍在使用这种结构。你也应该了解反引号，以防万一需要编写可移植到较老 Unix 系统的 shell 程序，而这些系统的 shell 不支持较新的、更受推荐的 `$(...)` 结构。

下面是一个示例：

```sh
$ echo The date and time is: `date`
The date and time is: Wed Aug 28 14:28:43 EDT 2002
$
```

当 shell 对命令行进行初始扫描时，它会识别出反引号，并期望后面跟着一个命令。在这个例子中，shell 找到 date 命令，于是执行 date，并用 date 的输出来替换命令行中的 `date` 序列。之后，shell 以正常方式将所得命令行划分为多个参数，然后将它们全部交给 echo 命令。

```sh
$ echo Your current working directory is `pwd`
Your current working directory is /user/steve/shell/ch6
$
```

