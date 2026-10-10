
在命令行上使用内联输入重定向时，shell 会使用由 `ps2` 环境变量（参见第 6 章）定义的第二级提示符来提示用户输入数据。以下是其实际使用效果：

```
$ wc << EOF
> test string 1
> test string 2
> test string 3
> EOF
        3           9          42

$ 
```

第二级提示符会持续提示输入更多数据，直到你输入文本标记的字符串值。`wc` 命令会对通过内联输入重定向提供的数据执行行数、单词数和字节数的统计。

## 使用管道

有时你需要将一个命令的输出发送到另一个命令的输入中。虽然可以通过重定向实现这一点，但这种方式略显笨拙：

```
$ rpm -qa>  rpm.list
$ sort < rpm.list
abattis-cantarell-fonts-0.0.25-1.el7.noarch
abrt-2.1.11-52.el7.centos.x86_64
abrt-addon-ccpp-2.1.11-52.el7.centos.x86_64
abrt-addon-kerneloops-2.1.11-52.el7.centos.x86_64
abrt-addon-pstoreoops-2.1.11-52.el7.centos.x86_64
abrt-addon-python-2.1.11-52.el7.centos.x86_64
abrt-addon-vccore-2.1.11-52.el7.centos.x86_64
abrt-addon-xorg-2.1.11-52.el7.centos.x86_64
abrt-cli-2.1.11-52.el7.centos.x86_64
abrt-console-notification-2.1.11-52.el7.centos.x86_64
...
```

`rpm` 命令用于管理在 Red Hat 包管理系统（RPM）上安装的系统（如所示的 CentOS 系统）上的软件包。当与 `-qa` 参数一起使用时，它会生成已安装包列表，但不一定按特定顺序排列。如果你正在查找特定的包或包组，使用 `rpm` 命令的输出可能会很难找到它们。

使用标准输出重定向，`rpm` 命令的输出被重定向到名为 `rpm.list` 的文件中。命令完成后，`rpm.list` 文件包含该系统上所有已安装软件包的列表。接下来，使用输入重定向将 `rpm.list` 文件的内容发送到 `sort` 命令，以按字母顺序对包名进行排序。

这很有用，但同样是一种略显笨拙的信息生成方式。与其将命令的输出重定向到文件，你可以将输出重定向到另一个命令。这个过程称为*管道*。

与命令替换的反引号（`` ` ``）一样，管道符号在 shell 脚本之外并不常用。该符号是两条垂直线，一条在另一条上方。然而，印刷体中的管道符号通常看起来像单条垂直线（|）。在美国键盘上，它通常与反斜杠（\）位于同一个键上。管道放在命令之间，以将一个命令的输出重定向到另一个命令：

```
command1 | command2
```

不要认为管道是连续运行两个命令。Linux 系统实际上同时运行这两个命令，并在系统内部将它们链接在一起。当第一个命令产生输出时，它会立即发送到第二个命令。不使用中间文件或缓冲区来传输数据。

现在，使用管道可以轻松地将 `rpm` 命令的输出直接管道传输到 `sort` 命令以生成结果：

```
$ rpm -qa | sort
abattis-cantarell-fonts-0.0.25-1.el7.noarch
abrt-2.1.11-52.el7.centos.x86_64
abrt-addon-ccpp-2.1.11-52.el7.centos.x86_64
abrt-addon-kerneloops-2.1.11-52.el7.centos.x86_64
abrt-addon-pstoreoops-2.1.11-52.el7.centos.x86_64
abrt-addon-python-2.1.11-52.el7.centos.x86_64
abrt-addon-vmcore-2.1.11-52.el7.centos.x86_64
abrt-addon-xorg-2.1.11-52.el7.centos.x86_64
abrt-cli-2.1.11-52.el7.centos.x86_64
abrt-console-notification-2.1.11-52.el7.centos.x86_64
…
```

除非你阅读速度非常快，否则你可能无法跟上此命令生成的输出。由于管道功能实时操作，一旦 `rpm` 命令产生数据，`sort` 命令就开始对其排序。等到 `rpm` 命令完成数据输出时，`sort` 命令已经排序完毕，并开始在显示器上显示数据。

你可以使用的管道数量没有限制。你可以继续将命令的输出管道传输到其他命令以细化操作。

在这种情况下，由于 `sort` 命令的输出速度很快，你可以使用文本分页命令（如 `less` 或 `more`）强制输出在每一屏数据结束时停止：

```
$ rpm -qa | sort | more
```

此命令序列运行 `rpm` 命令，将输出管道传输到 `sort` 命令，然后再将该输出管道传输到 `more` 命令以显示数据，并在每屏信息后停止。这现在允许你在继续之前暂停并阅读显示屏上的内容，如图 11-1 所示。

要想更高级一点，你可以将重定向与管道结合使用，将输出保存到文件：

```
$ rpm -qa | sort> rpm.list
$ more rpm.list
abrt-1.1.14-1.fc14.i686
abrt-addon-ccpp-1.1.14-1.fc14.i686
abrt-addon-kerneloops-1.1.14-1.fc14.i686
abrt-addon-python-1.1.14-1.fc14.i686
abrt-desktop-1.1.14-1.fc14.i686
abrt-gui-1.1.14-1.fc14.i686
abrt-libs-1.1.14-1.fc14.i686
abrt-plugin-bugzilla-1.1.14-1.fc14.i686
abrt-plugin-logger-1.1.14-1.fc14.i686
abrt-plugin-runapp-1.1.14-1.fc14.i686
acl-2.2.49-8.fc14.i686
```

![](img/a5025f22e05b92f409563a958cac7312_399_0.png)

图 11-1 使用管道将数据发送到 more 命令

不出所料，`rpm.list` 文件中的数据现在已排序！

迄今为止，最受欢迎的用法之一是将产生较长输出的命令结果管道传输到 `more` 命令。这在 `ls` 命令中尤为常见，如图 11-2 所示。

`ls -l` 命令生成目录中所有文件的长列表。对于包含大量文件的目录，这会是一个很长的列表。通过将输出管道传输到 `more` 命令，你强制输出在每屏数据末尾停止。

## 执行数学运算

对任何编程语言至关重要的另一个功能是操纵数字的能力。不幸的是，对于 shell 脚本，这个过程有点麻烦。你有两种方法在 shell 脚本中执行数学运算。

![](img/a5025f22e05b92f409563a958cac7312_400_0.png)

### expr 命令

最初，Bourne shell 提供了一种用于处理数学方程的特殊命令。`expr` 命令允许从命令行处理方程，但它非常笨拙：

```
$ expr  1 + 5
6
```

`expr` 命令识别几种不同的数学和字符串运算符，如表 11-1 所示。

标准运算符在 `expr` 命令中运行良好，但问题出现在从脚本或命令行使用它们时。许多 `expr` 命令运算符在 shell 中有其他含义（例如星号）。在 `expr` 命令中使用它们会产生奇怪的结果：

```
$ expr 5 * 2
expr: syntax error
$ 
```

### 表 11-1 `expr` 命令运算符

| 运算符 | 描述 |
| :--- | :--- |
| ARG1 \| ARG2 | 如果两个参数都不是 null 或 0，则返回 ARG1；否则，返回 ARG2。 |
| ARG1 & ARG2 | 如果两个参数都不是 null 或 0，则返回 ARG1；否则，返回 0。 |
| ARG1 < ARG2 | 如果 ARG1 小于 ARG2，则返回 1；否则，返回 0。 |
| ARG1 <= ARG2 | 如果 ARG1 小于或等于 ARG2，则返回 1；否则，返回 0。 |
| ARG1 = ARG2 | 如果 ARG1 等于 ARG2，则返回 1；否则，返回 0。 |
| ARG1 != ARG2 | 如果 ARG1 不等于 ARG2，则返回 1；否则，返回 0。 |
| ARG1 >= ARG2 | 如果 ARG1 大于或等于 ARG2，则返回 1；否则，返回 0。 |
| ARG1 > ARG2 | 如果 ARG1 大于 ARG2，则返回 1；否则，返回 0。 |
| ARG1 + ARG2 | 返回 ARG1 和 ARG2 的算术和。 |
| ARG1 - ARG2 | 返回 ARG1 和 ARG2 的算术差。 |
| ARG1 * ARG2 | 返回 ARG1 和 ARG2 的算术积。 |
| ARG1 / ARG2 | 返回 ARG1 除以 ARG2 的算术商。 |
| ARG1 % ARG2 | 返回 ARG1 除以 ARG2 的算术余数。 |

