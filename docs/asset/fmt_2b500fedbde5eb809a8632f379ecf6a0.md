
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

图 11-1 使用管道将数据发送到 `more` 命令

不出所料，`rpm.list` 文件中的数据现在已排序！

迄今为止，最受欢迎的用法之一是将产生较长输出的命令结果管道传输到 `more` 命令。这在 `ls` 命令中尤为常见，如图 11-2 所示。

`ls -l` 命令生成目录中所有文件的长列表。对于包含大量文件的目录，这会是一个很长的列表。通过将输出管道传输到 `more` 命令，你强制输出在每屏数据末尾停止。

### 执行数学运算

对任何编程语言至关重要的另一个功能是操纵数字的能力。不幸的是，对于 shell 脚本，这个过程有点麻烦。你有两种方法在 shell 脚本中执行数学运算。

![](img/a5025f22e05b92f409563a958cac7312_400_0.png)

#### expr 命令

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

##### 表 11-1 `expr` 命令运算符

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

#### 字符串：正则表达式

| 命令 | 描述 |
| :--- | :--- |
| `STRING : REGEXP` | 如果 REGEXP 在 STRING 中匹配某个模式，则返回该模式匹配项。 |
| `match STRING REGEXP` | 如果 REGEXP 在 STRING 中匹配某个模式，则返回该模式匹配项。 |
| `substr STRING POS LENGTH` | 返回长度为 LENGTH 的子字符串，从位置 POS（起始位置为 1）开始。 |
| `index STRING CHARS` | 返回 CHARS 在 STRING 中找到的位置；否则返回 0。 |
| `length STRING` | 返回字符串 STRING 的数值长度。 |
| `+ TOKEN` | 即使 TOKEN 是关键字，也将其解释为字符串。 |
| `(EXPRESSION)` | 返回 EXPRESSION 的值。 |

为了解决这个问题，你需要使用 shell 转义字符（反斜杠）来标识那些在传递给 `expr` 命令之前可能会被 shell 错误解释的字符：

```bash
$ expr 5 \* 2
10
$
```

这就真的开始变得很难用了！在 shell 脚本中使用 `expr` 命令同样笨重：

```bash
$ cat test6
#!/bin/bash
# 一个使用 expr 命令的示例
var1=10
var2=20
var3=$(expr $var2 / $var1)
echo 结果是 $var3
```

要将数学方程的结果分配给变量，你必须使用命令替换从 `expr` 命令中提取输出：

```bash
$ chmod u+x test6
$ ./test6
结果是 2
$
```

幸运的是，Bash shell 在处理数学运算符方面有所改进，你将在下一节中看到。

#### 使用方括号

Bash shell 包含了 *expr* 命令以保持与 Bourne shell 的兼容性；然而，它也提供了一种进行数学方程计算更简单的方法。在 Bash 中，当将数学值分配给变量时，你可以使用美元符号和方括号（$[ 操作 ]）来包围数学方程：

```bash
$ var1=$[ 1 + 5]
$ echo $var1
6
$ var2=$[$var1 * 2]
$ echo $var2
12
$
```

使用方括号使 shell 数学运算比使用 *expr* 命令容易得多。同样的技术也适用于 shell 脚本：
