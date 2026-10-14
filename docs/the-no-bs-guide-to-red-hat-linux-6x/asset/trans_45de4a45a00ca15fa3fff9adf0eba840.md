

```text
+ shift
+ count=1+1
+ { def = }
+ echo Arg 1+1 : def
Arg 1+1 : def
+ shift
+ count=1+1+1
+ { = }
```

嗯……

不对！

本来应该打印出 Arg 2 : def，结果却得到了 Arg 1+1 : def。不过，显示 `count=1+1` 的跟踪输出行准确地指出了问题所在。你忘记使用 `expr` 命令了，因此 shell 将其当作字符串连接，而不是数学计算。

> 注意：你始终可以按 CTRL-C 来停止正在运行的 shell 脚本。如果你不小心创建了一个无限循环脚本（即无法自行结束的脚本），这个功能会非常有用。

## 使用 PERL 编写程序脚本

Perl 是一种解释型语言，在 Unix 社区中非常流行，因为它功能丰富而强大，同时仍然易于使用。Perl 大量借鉴了 C 和 awk 等其他语言，尤其适用于处理文本、生成报告，以及处理由 Web 浏览器提交的通用网关接口（CGI）请求。

Perl 已被移植到许多非 Unix 环境中，包括 DOS、OS/2、Macintosh、VMS 和 Windows NT。Perl 程序能够在许多不同平台上几乎无需修改或完全无需修改即可运行，这也是其广受欢迎的另一个原因。在本节中，我将向你介绍 Perl 的基础知识，并为你提供一些可以进一步学习的资源。

### PERL 基础知识

要创建 Perl 脚本，请使用文本编辑器输入 Perl 命令，将文件保存为 `.pl` 扩展名（例如 `sample.pl`），然后使用 chmod 将文件标记为可执行文件。扩展名并非必需，但这是 Unix 中常见的约定，并且无需查看文件内容，就能帮助你识别 Perl 源文件。

下面是一个非常简单的 Perl 脚本：

```perl
#!/usr/bin/perl
print "I am here. \n";
```

神秘的第一行以“井号-感叹号-斜杠”开头，所有 Perl 脚本要运行都必须包含这一行；它告诉系统到哪里查找 Perl 解释器。希望你已经看出，这个程序会打印一条消息，后面跟着换行符。

与 Bash 脚本中的 echo 命令不同，Perl 的 print 命令不会自动发送回车和换行。如果忘记 `\n` 序列，下一个 print 命令就会从同一行开始。另外请注意，所有 Perl 语句都必须以分号结尾。

### 变量和引号

Perl 脚本中的变量是一种引用数值或字符值的方式。和 Bash 脚本一样，Perl 不要求你为变量声明类型。Perl 会根据上下文判断某个值应被视为数字还是字符字符串，并且在必要时，甚至会执行从字符到数值的转换。要给变量赋值或访问变量的值（内容），请在变量前加上美元符号。等号前后的空格是可选的，但如果要为包含字符数据的变量赋值，必须在字符串两侧加上引号。

```perl
$num=5;
$stuff = "chocolate truffles";
$user = $ENV{USER};
```

在这些示例中，Perl 将 5 赋给数值变量 `$num`，将 “chocolate truffles” 赋给变量 `$stuff`，并将 USER 环境变量的值赋给 `$user`。

现在正好可以说明，在 Perl 脚本中使用引号有几种不同的方式。下面让我们看看单引号、双引号、反引号和反斜杠字符之间的区别，然后再通过一些示例进行说明。

- 单引号（如前面的示例所示）会始终原样保留引号内的内容——任何本来可能具有特殊含义的字符（例如美元符号或反斜杠）都会按字面意义处理。
- 如果要赋值的字符串包含需要进行解释的特殊字符，请使用双引号。
- 反斜杠用于转义（按字面意义处理）单个字符（例如 `$` 或 `*`），以避免该字符被当作特殊字符处理。
- 使用反引号表示字符串是一个应当执行的 Linux 命令，并将执行结果赋给一个变量。

下面通过一些示例来看看分别应在何时使用这些引号方式：

```text
$user = $ENV{USER};
print 'Good Morning $user';
Yields: Good Morning $user

$user = $ENV{USER};
print "Good Morning $user";
Yields: Good Morning hermie
```

在第一个示例中，结果可能不是你想要的。单引号使 Perl 不会将 `$user` 当作变量处理。在第二个示例中，结果看起来就好多了。双引号允许 Perl 将 `$user` 的值替换到字符串中。下面再看一个展示常见错误的示例：

```text
$costmsg = "Price is $5.00";
print "$costmsg";
Yields: Price is .00
```

我们已经注意给字符串加上引号，但美元符号告诉 Perl 使用 `$5` 变量中的值，而该变量目前尚未定义。只需在美元符号前加上反斜杠即可轻松解决这个问题，如下所示：

```text
$costmsg = "Price is \$5.00";
print "$costmsg";
Actual result: Price is $5.00
```

最后，下面是一个使用反引号执行 Linux 命令，并将结果捕获到 Perl 变量中的示例：

```text
$currdir = `pwd`;
print "Current directory is $currdir";
Yields: Current directory is /home/hermie
```

