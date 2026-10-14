
如果你执行包含这三行的 `shell` 程序，你将得到以下结果：

`Value of var $var`

如你所见，变量 `var` 在结果中保持了其原始格式，而不是被展开。

# 使用反斜杠作为转义字符

正如你之前学过的，反斜杠（`\`）作为转义字符，可以停止后续字符被视为特殊字符。假设你想将 `$test` 的值赋值给名为 `var` 的变量。如果你使用以下命令，`shell` 会读取特殊字符 `$` 并将 `$test` 解释为变量的值。没有值被赋值给 `test`；`var` 中存储了一个空值，如下：

| 命令 | 环境 |
| --- | --- |
| `var=$test` | `pdksh` and `bash` |
| `set var=$test` | `tcsh` |

遗憾的是，这种赋值在 `bash` 和 `pdksh` 中可能有效，但在 `tcsh` 中使用它时会返回“undefined variable”错误。使用以下命令可以将 `$test` 正确存储在 `var` 中：

| 命令 | 环境 |
| --- | --- |
| `var=\$test` | `pdksh` and `bash` |
| `set var = \$test` | `tcsh` |

美元符号前的反斜杠（`\$`）指示 `shell` 将 `$` 解释为任何其他普通字符，而不赋予其任何特殊含义。你也可以使用单引号（`''`）包围 `$test` 变量来获得相同的结果。

# 使用反引号替换字符串为输出

你可以使用反引号（`` `` ``）字符来指示 `shell` 将字符串替换为其执行的输出。这也被称为命令替换。当你想要将命令执行的结果存储在变量中时，可以在 `shell` 程序中使用这个特殊字符。例如，如果你想统计当前目录下文件 `test.txt` 的行数并将结果存储在变量 `var` 中，你可以使用以下命令：

| 命令 | 环境 |
| --- | --- |
| `var=`wc -l test.txt`` | `pdsh` and `bash` |
| `set var = `wc -l test.txt`` | `tcsh` |

# pdsh 和 bash 中表达式的比较

比较值或评估相似数据之间的差异——例如文件信息、字符字符串或数字——是一项被称为表达式比较的任务。表达式比较是在 `shell` 程序中使用逻辑来完成任务的不可或缺的一部分。在 `pdsh` 和 `bash` 中，对两个操作符（数字或字符串）的逻辑比较在不同的 `shell` 中实现略有不同。在 `pdsh` 中，可以使用 `test` 命令来实现表达式比较。在 `tcsh` 中，你可以写一个表达式来实现相同的操作。

本节涵盖了使用 `pdsh` 和 `bash shell` 的比较操作。在章节的后面，你将学习如何在 `test shell` 中比较表达式。

`pdsh` 和 `bash shell` 语法提供了一个名为 `test` 的命令来比较字符串、数字和文件。`test` 命令的语法如下：

```
test expression
or
[ expression ]
```

两种形式的 `test` 在 `pdsh` 和 `bash` 中以相同的方式处理。`test` 命令支持以下类型的比较：

- 字符串比较
- 数字比较
- 文件运算符
- 逻辑运算符

## 字符串比较

你可以使用以下运算符来比较字符串：

- `=` To比较两个字符串是否相等。
- `!=` To比较两个字符串是否不等。
- `-n` To判断字符串长度是否大于零。
- `-z` To判断字符串是否为空。

下面是使用这些运算符比较 `string1` 和 `string2` 的示例，在一个名为 `compare` 的 `shell` 程序中：

```
#!/bin/sh
string1="abc"
string2="abd"
if [ $string1 = $string2 ]; then
    echo "string1 equal to string2"
else
    echo "string1 not equal to string2"
fi
if [ $string1 != $string2 ]; then
    echo "string1 not equal to string2"
else
    echo "string1 equal to string2"
fi
if [ -n $string1 ]; then
    echo "string1 is not empty"
else
    echo "string1 is empty"
fi
if [ -z $string1 ]; then
    echo "string1 is empty"
else
    echo "string1 is not empty"
fi
```

如果你执行该 `shell` 程序，你将得到以下结果：

`string1 not equal to string2`

`string1 not equal to string2`

`string1 is not empty`

## 数字比较

可以使用以下运算符比较两个数字：

- `-eq` To比较两个数字是否相等。
- `-ge` To比较一个数字是否大于等于数字。
- `-le` To比较一个数字是否小于等于数字。
- `-ne` To比较两个数字是否不等。
- `-gt` To比较一个数字是否大于数字。
- `-lt` To比较一个数字是否小于数字。

假设一个名为 `compare3` 的 `shell` 程序比较名为 `file1` 的文件和当前目录下的子目录 `dir1`。假设 `file1` 具有 `r-x`（读和执行）权限，`dir1` 具有 `rwx`（读、写和执行）权限。该 `shell` 程序的代码如下：

```
#!/bin/sh
if [ -d $dir1 ]; then
    echo "dir1 is a directory"
else
    echo "dir1 is not a directory"
fi
```

## 文件运算符

你可以使用以下运算符作为文件运算符：

- `-d` To判断文件是否为目录。
- `-t` To判断文件是否为普通文件。
- `-r` To判断文件是否具有读取权限。
- `-s` To判断文件是否存在且长度大于零。
- `-w` To判断文件是否具有写入权限。
- `-x` To判断文件是否具有执行权限。

```bash
if [ -f $dir ]; then
  echo "$dir is a regular file"
else
  echo "$dir is not a regular file"
fi
```

```bash
if [ -r $file1 ]; then
  echo "$file1 has read permission"
else
  echo "$file1 does not have read permission"
fi
```

```bash
if [ -w $file1 ]; then
  echo "$file1 has write permission"
else
  echo "$file1 does not have write permission"
fi
```

```bash
if [ -x $dir ]; then
  echo "$dir has execute permission"
else
  echo "$dir does not have execute permission"
fi
```

如果你执行该 `shell` 程序，将得到以下结果：

- `dir` 是一个目录
- `file1` 是一个普通文件
- `file1` 具有读取权限
- `file1` 没有读取权限
- `dir` 具有执行权限

## 逻辑运算符

你使用逻辑运算符通过布尔逻辑来比较表达式，布尔逻辑使用表示 NOT（非）、AND（与）和 OR（或）的字符来比较值：

- `!` — 对逻辑表达式取反。
- `-a` — 对两个逻辑表达式逻辑与。
- `-o` — 对两个逻辑表达式逻辑或。

这个命名逻辑使用了上一个比较示例中提到的文件和目录：

```sh
#!/bin/sh
if [ -x file1 -a -x $dir ]; then
```

## 编写并执行 Shell 脚本

```bash
if [ -w file1 -o -w dirl ]; then
  echo file1 or dirl are writable
else
  echo neither file1 or dirl are executable
fi
```

```bash
if [ ! -w file1 ]; then
  echo file1 is not writable
else
  echo file1 is writable
fi
```

如果你执行该逻辑判断，它将产生以下结果：

`file1` 和 `dirl` 是可执行的

`file1` 或 `dirl` 是可写的

`file1` 不可写

# 使用 tcsh 比较表达式

如前所述，在 `tcsh` 中比较表达式的方法与在 `pdsh` 和 `bash` 中的方法不同。本节演示的表达式比较使用了 `tcsh shell` 环境所需的语法。

## 字符串比较

你可以使用以下运算符来比较两个字符串表达式：

- `==` — 比较两个字符串是否相等。
- `!=` — 比较两个字符串是否不相等。
