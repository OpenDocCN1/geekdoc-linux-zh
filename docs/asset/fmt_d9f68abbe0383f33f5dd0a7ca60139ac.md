
print "This statement ends with a semicolon\n"

# 元字符有许多用途，包括以下：

- 在 HTML 文档的锚点指针中。`#` 元字符位于目标名称之前。目标允许用户导航到单个网页内部的特定点。你可能在 URL 中见过此类锚点引用，例如：`http://www.mcp/index.html#toc`。这将带你进入 `index.html` 文档中的 `toc` 目标。

- 在脚本和配置文件中注释掉行。`#` 字符之后的任何行都会被忽略（除非换行到下一行，在这种情况下通常需要另一个 `#`）。

- 与感叹号 `bang` 符号结合使用，用于指定给定脚本要使用的 shell 或命令解释器（例如 `#!bin/sh` 或 `#!usr/bin/perl`）。

- 在 C 编程语言源文件中包含指令（例如 `#include <stdio.h>`）。

`!` `csh` 中的元字符或感叹号符号通过 `csh` 历史记录调回最近的命令。例如，命令 `!143` 会调回命令 143。（你可以通过输入双感叹号 `!!` 来快速调回上一个命令。）在其他实例中，`!` 表示逻辑非（NOT）。

``` 
If(userfield eq "Okay") {

    print "The user did not agree\n"

}
```

这段代码表示，如果 `userfield` 不等于文本 `"Okay"`，系统应该打印用户不同意。

`;` `|` 管道符号用于命令的管道，其中一个命令的输出成为另一个命令的输入。例如，假设你想检查最后 10 次 root 登录的日志。你可以执行此命令：

```
last root | head -10
```

这将获取所有记录的 root 登录（`last root`）。产生的输出随后成为 `head` 的输入，它将剥离最近的 10 次登录（`head -10`）。管道符号在 C 中也表示逻辑或（OR）。

`;;` `||` 双管道元字符组合表示两个或多个命令之间的逻辑或。例如，语句 `command1 || command2` 告诉 shell 如果 `command1` 失败，则执行 `command2`。

# 词汇表

# 附录 E

`&` 单安符元字符 (`&`) 告诉 shell 在后台运行前一个命令。当你想要执行的命令会锁定 shell 提示符一段时间时，使用它。（某些命令可能需要几分钟或几小时。）例如：

```
complex - &
```

另见后台。（`&` 符号在 C 中也是逻辑与（AND）。）

`# &&` 或双安符元字符表示两个或多个命令之间的逻辑与。例如，语句 `command && command2` 告诉 shell 如果 `command1` 成功，则执行 `command2`。

在命令末尾发布 `>&` 组合会将 STDOUT 和 STDERR 重定向到文件（并覆盖文件）。另见标准输出 (`STDOUT`) 和标准错误 (`STDERR`)。

`>>` 在命令末尾发布 `>>` 组合会将 STDOUT 和 STDERR 重定向（追加）到文件。另见标准输出 (`STDOUT`) 和标准错误 (`STDERR`)。

`$` 元字符用于变量赋值（特别是在某些 shell 和 Perl 中）。例如：

```
$myfile = '/usr/bin/date';
```

此语句将当前日期分配给 `$myfile`。从现在起，你可以使用 `$myfile` 来调用或打印当前日期和时间。例如：

```
$myfile = '/usr/bin/date'

print 'Your comments were received on about $myfile\n';
```

- 星号 (`*`) 用于在文件搜索中匹配任何字符（或数量数量字符）。

- `?` 符号将匹配文件名搜索中的任何字符。因此，搜索 `myfile.txt` 将匹配 `myfile.txt`、`myfile.txt` 等。

- `@` 符号用于 Perl 中的数组赋值 (`fruits='apples', 'peaches'`)。`@` 符号也用于电子邮件地址 (`bonehead@shankmaster.net`)。

- `<` 用于将输入重定向到指定的文件。在许多编程语言中，`<` 符号也用于其更传统的角色，即比较运算符，众所周知的“小于”符号。

- `>` 用于将输出重定向到指定的文件或进程。例如，`dir-listing.txt` 将你的目录列表请求 (`dir`) 重定向到文件 (`dir-listing.txt`) 以供以后查看。在许多编程语言中，`>` 符号也是比较运算符。

# 附录
第五部分

`;` 元字符通常用于分隔顺序执行的 shell 命令（例如 `command1;command2`）；也用于某些编程语言（Perl, C, C++）来结束一个语句。例如：

```
print "This statement ends with a semicolon\n"
```
