
> 2018-10-06 Mary Stephens Added data backup rules.

比较两个文本文件。

### 语法

`diff` 命令的语法为 `diff [file name 1] [file name 2]`

# diff 命令选项

`diff` 命令有各种选项允许你指定输出的性质。

- `-b` 忽略空格差异。
- `-i` 忽略大小写差异。
- `-t` 在输出行中扩展制表符。
- `-w` 忽略空格差异并
- `-c` 显示带有三行上下文的差异列表。

`-u` 以统一模式输出结果，提供了一种更精简的格式。

# grep 命令

`grep` 命令在最基本的形式是一个搜索工具。与 `find` 或 `locate` 不同，它不限于查找文件名；它通常用于在文件中搜索特定的文本字符串。作为输出，`grep` 显示找到你搜索模式的文件的每个完整行。你可以使用 `grep` 处理文本文件并读取与你最相关的内容。例如，你可能通过查看访问日志来审核用户的登录事件。与其读取整个日志或在文本编辑器中逐步查找搜索词，你可以可以使用 `grep` 命令将所有相关行打印到屏幕上。

# 搜索词

# 要搜索的文件

```
[root@server01 ~]## grep /var/log/secure

Jan 7 18:47:08 server01 su: pam_unix(su-session): sessio

opened for user ailey by student01(uid=0)

Jan 7 18:48:00 server01 su: pam_unix(su-session): sessio

closed for user ailey

Jan 7 18:48:27 server01 su: pam_unix(su-session): sessio

opened for user ailey by student01(uid=0)

Jan 7 18:48:39 server01 su: pam_unix(su-session): sessio

closed for user ailey

[root@server01 ~]#
```

# 上文中行

# 包含术语的行

搜索包含特定术语的文件。

### 语法

`grep` 命令的语法为 `grep [options] [search pattern] [file names]`

# grep 命令选项

`grep` 命令有很多选项。下表描述了几个常用的选项。

- `-E [pattern]` 作为扩展正则表达式 (ERE) 匹配模式。
- `-F [pattern]` 作为固定字符串列表匹配模式。
- `-f [file name]` 指定文件中包含的模式。
- `-i` 忽略大小写。
- `-v` 只输出不匹配提供模式的行。
- `-c` 只打印匹配行的数，而不是行本身。
- `-l` 只打印行的匹配部分，而不是整个行。
- `-o`

# 使用 grep 查找文件

除了搜索文件内容外，你还可以 `grep` 搜索目录以定位特定文件。`ls -l | grep audit` 命令返回当前目录下任何名称包含 "audit" 的文件的长列表。

# egrep 命令

`egrep` 命令本质与 `grep -E` 命令相同。然而，`egrep` 已弃用，因为 `grep -E` 是首选语法。

> 注意：正则表达式超出了课程的范围。有关更多信息，请访问 https://www.regular-expressions.info/quickstart.html。

# awk 命令

`awk` 命令对文件执行模式匹配。它基于 AWK 编程语言。`awk` 关键字后面跟着模式、要执行的操作以及文件名。要执行的操作应该放在大括号内。如果没有指定模式，则对所有输入数据执行操作；然而，如果没有指定操作，则打印整行。`awk` 命令可以从命令行或在 `awk` 脚本文件中执行。

`awk` 命令可以使用多种方式处理文本文件，例如提取匹配模式的文本；删除匹配模式的文本；添加匹配模式的文本；以及更多。

注意：GNU 的 awk 版本称为 `gawk`

![](img/b739f72e1850e8363ae440b6c753d29_125_0.png)

搜索日志中 1 月记录的所有条目。

```bash
[root@server01 ~]$ $1 == "Jan" /var/log/secure

Jan 7 18:47:08 server01 su: pam_unix(su-session): sessio

opened for user ailey by student01(uid=0)

Jan 7 18:48:00 server01 su: pam_unix(su-session): sessio

closed for user ailey

Jan 7 18:48:27 server01 su: pam_unix(su-session): sessio

opened for user ailey by student01(uid=0)

Jan 7 18:48:39 server01 su: pam_unix(su-session): sessio

closed for user ailey

[root@server01 ~]#
```
