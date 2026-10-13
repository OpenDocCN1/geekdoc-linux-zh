
# 24小时自学学会 Shell 编程

## 第18小时：杂项工具

**Frank Watson 著**

在本章中，你将看到几种在 shell 脚本中经常遇到的 UNIX 杂项命令，并且你可以在自己的程序中使用它们。其中第一类包括*内置* shell 命令，这意味着 shell 可以在不从磁盘读取单独的实用程序的情况下执行它们：

- `eval`
- `:`
- `type`

然后，你将介绍几种以二进制程序形式存在于磁盘上的外部命令：

- `sleep`
- `find` 和 `xargs`
- `bc` 和 `expr`
- `remsh`（有时称为 `rsh`、`rcmd` 或 `remote`）

内置工具的运行效率比外部程序略高，因为它们不需要从磁盘读取。除非你循环数千次，否则你通常不需要担心使用的工具是内置的还是外部的。

| 24小时自学学会 Shell 编程 | 目录 | 索引 |
| :--- | :--- | :--- |
| 第18小时：杂项工具 | 上一章 | 下一章 |
| 本章章节： | | |
| `eval` 命令 | `expr` 命令 | |
| | `bc` 命令 | |
| `type` 命令 | `remsh`/`rcmd`/`remote`（远程 shell） | |
| `sleep` 命令 | 总结 | |
| `find` 命令 | 问题 | |
| `xargs` | 术语 | |

© Copyright Macmillan Computer Publishing. 版权所有。

### eval 命令

当你想要 shell 第二次对命令行进行重新处理时，可以使用 `eval` 命令。基本语法为

```
eval any-UNIX-command
```

在任何 UNIX shell 命令的开头插入 `eval` 命令。当通过变量替换或命令替换插入特殊字符时，需要此操作（参见第 8 章“替换”）。例如，

```
OUTPUT=\> out.file

echo hello $OUTPUT
```

`OUTPUT` 变量包含 `>` 符号，用于将标准输出重定向到名为 `out.file` 的文件。但当你在 `echo` 语句中使用 `OUTPUT` 变量时，你会发现一个问题。运行这段代码时，屏幕上显示的内容如下：

```
hello > out.file
```

输出到了屏幕，而不是文件，因为当 shell 第一次查找原始命令行中的重定向符号时，`>` 符号并不存在。你可以通过在 `echo` 命令的开头插入 `eval` 命令来修复这个问题：

```
OUTPUT=\> out.file

eval echo hello $OUTPUT
```

现在当你运行代码时，它返回到 shell 提示符而不在屏幕上显示任何文本。它创建了一个包含单词 `hello` 的 `out.file` 文件，这是预期结果。你可能会问：这有什么用？答案是你之后更改 `OUTPUT` 的初始定义，它会影响所有以 `eval` 开头并以 `$OUTPUT` 结尾的行。例如：

```
OUTPUT=" >> out.file
```

是追加到 `out.file` 而不是覆盖。

`OUTPUT=` 导致输出到屏幕而不是文件。

`eval` 命令用于你想要 shell 第二次对命令行进行重新处理时。对于那些通过变量替换或命令替换插入特殊字符的情况，该命令是很有用的。

### type 命令

`type` 命令告诉给定的 UNIX 命令的完整路径。

基本语法为

```
type command1 command2 ...
```

如果给定的命令不是作为磁盘文件存在的实用程序，`type` 会告诉它是否是以下之一：

- shell 内置命令
- shell 关键字或保留字
- 别名

如果命令是另一个命令的别名，`type` 还会给出运行该别名时实际调用的命令。

例如，

```
$ true vi ulimit history

true is /bin/true

vi is /usr/bin/vi

case is a keyword

ulimit is a shell builtin

history is an exported alias for fc -1

$
```

不同类型的 UNIX 系统以不同的方式实现同一个命令。例如，`true` 是某些 UNIX 系统和某些 UNIX shell 内置的，使用 `:` 命令同样高效。你可以使用 `type` 命令检查 `true` 是否内置在你的系统中。

本章章节：

- `eval` 命令
- `expr` 命令
- `:` 命令
- `bc` 命令
- `remsh`/`rsh`/`rcmd`/`remote` (远程 Shell)
- `type` 命令
- `sleep` 命令
- 总结
- `find` 命令
- 问题
- `xargs`
- 术语

### sleep 命令

`sleep` 命令暂停指定的秒数。其基本语法为：

```
sleep n
```

其中 `n` 是睡眠或暂停的秒数。某些 UNIX 类型允许指定其他时间单位。通常建议 `n` 不要超过 65,534。

`sleep` 可用于在清除屏幕之前给用户留出阅读输出信息的时间。它也可以用于你想产生一系列蜂鸣时：

```
echo -e "A value must be input!\a"

sleep 1

echo -ne "\a"

sleep 1

echo -ne "\a"
```

`\a` 导致 `echo` 输出可听的蜂鸣声。在某些 UNIX 系统上，需要 `-e` 才能让 `\a` 发出声音。`-n` 抑制 `echo` 正常打印的换行。在上一个示例中，`sleep` 命令用于产生间隔一秒的一系列蜂鸣声。

`sleep` 可以用于循环中定期执行某任务：

```
while :
do

  date

  who

  sleep 300

done >> logfile
```

这段代码允许每 5 分钟（300 秒）将登录系统的用户列表追加到 `logfile` 中。

> 注意：如果你想让这段代码一直运行，必须定期清理 `logfile`，否则它会占用你所有的磁盘空间。

### find 命令

- `find`: 起始目录
- `find`: `-name` 选项
- `find`: `-type` 选项
- `find`: `-mtime`, `-atime`, `-ctime`
- `find`: `-size` 选项
- `find`: 组合选项
- `find`: 否定选项
- `find`: `-print` 动作
- `find`: `-exec` 动作

**`find`** 命令是一种强大且灵活的方法，用于创建符合给定标准的文件列表。

```
find start-dir options actions
```

这是一个简单的 **`find`** 示例：

```
find / -name alpha -print
```

## 第17小时：使用 awk 过滤文本

目录 索引 上一章 下一章

本章章节：

- 什么是 `awk`？问题
- 使用 `awk` 特性 术语
- 总结

上一节 下一节

# 萨姆 24 小时自学 Shell 编程

目录索引

第 18 小时：杂杂工具

本章章节：
- `expr` 命令
- `:` 命令
- `bc` 命令
- `type` 命令
- `remsh`/`rsh`/`rcmd`/`remote` (远程 Shell)
- `sleep` 命令
- 总结
- `find` 命令
- 术语
- `xargs`
