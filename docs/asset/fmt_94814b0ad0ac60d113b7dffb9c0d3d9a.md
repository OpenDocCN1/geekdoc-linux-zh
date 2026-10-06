
你将得到以下结果：
`Number of parameters is 2`
`Program name is mypgm2`
`Parameters as a single string is Sanjiv Guha`

## 特殊字符

某些字符对 Linux shell 具有特殊含义；这些字符代表命令、指定周围文本的特定用法，或提供搜索参数。特殊字符通过将这些复杂的含义整合到一个单一字符中，提供了简便的方法。表 22.2 显示了一些特殊字符。

### 表 22.2 特殊 shell 字符

| 字符 | 解释 |
| --- | --- |
| `$` | 表示 shell 变量名的开始 |
| `|` | 将标准输出管道到下一个命令 |
| `#` | 开始注释 |
| `&` | 在后台执行进程 |
| `?` | 匹配一个字符 |
| `*` | 匹配一个或多个字符 |
| `>` | 输出重定向运算符 |
| `<` | 输入重定向运算符 |

### 表 22.2 续表

| 字符 | 解释 |
|---|---|
| `.` | 命令替换（反引号或反引线——大多数键盘上 Tab 键上方的键） |
| `>>` | 输出重定向运算符（追加到文件） |
| `<<` | 等待后续的输入结束字符串（HERE 运算符） |
| `]` | 字符范围 |
| `[a-z]` | 从 a 到 z的所有字符 |
| `[a,z]` 或 `[az]` | 字符 a 或 z |
| 空格 | 两个单词之间的分隔符 |

特殊字符对你非常有用，但如果你无意中将特殊字符用变量名或字符串，你的程序行为将出现错误。正如你在本节的后续部分中学到的，你可以在特殊字符前面加上一个转义字符（`\` 或反斜杠）来使用它，以指示它不被用作特殊字符，程序也不应将其视为。

有几个字符值得特别注意。它们是双引号（`"`）、单引号（`'`）、反斜杠（`\`）和反引号（`` ` ``）——这些将在接后的章节中讨论。

## 使用双引号解析包含空格的字符串中的变量

如果字符串包含嵌入空格，你可以用双引号（`"`）将字符串括起来，让 shell 将整个字符串解释为一个实体，而不是多个实体。

例如，如果你在 shell 程序中如下将值 `abc def`（`abc` 后面跟空格、`def`）赋值给变量 `x`，你将得到错误，因为 shell 会尝试将 `def` 执行为单独命令。

| 命令 | 环境 |
|---|---|
| `x=abc def` | `pdksh` and `bash` |
| `set x=abc def` | `tsh` |

如果你用双引号括住字符串，shell 将把该字符串作为单个命令执行：

| 命令 | 环境 |
|---|---|
| `x="abc def"` | `pdksh` and `bash` |
| `set x="abc def"` | `tsh` |

双引号会解析字符串中的所有变量。以下是 `pdksh` 和 `bash` 的示例：

```sh
var="test string"
newvar="Value of var is $var"
echo $newvar
```

以下是针对 `tsh` 的相同示例：

```sh
set var="test string"
set newvar="Value of var is $var"
echo $newvar
```

如果你执行包含上述三行的 shell 程序，你将得到以下结果：

`Value of var is test string`

## 使用单引号保持变量未展开状态

你可以用单引号（`'`）将将字符串括起来，以停止 shell 扩展变量和解释特殊字符。当用于后者的目的时，单引号是一个转义字符，类似于反斜杠（你将在下一节中学习反斜杠）。在这里，你将学习如何使用单引号来避免扩展 shell 脚本中的变量。未展开的变量在输出中将保持其原始形式。

在以下示例中，前述示例中的双引号已改为单引号。

`pdksh` and `bash`:
```sh
var='test string'
newvar='Value of var is $var'
echo $newvar
```

`tsh`:
```sh
set var = 'test string'
set newvar = 'Value of var is $var'
echo $newvar
```

如果你执行包含这三行的 shell 程序，你将得到以下结果：

`Value of var is $var`

你可以看到，变量 `var` 在结果中保持了它的原始格式，而不是被扩展。

## 使用反斜杠作为转义字符

正如你之前学到的，反斜杠（`\`）作为转义字符，可以停止 shell 将其后的字符解释为特殊字符。假设你想给一个名为 `var` 的变量赋值 `$test` 的值。如果你使用以下命令，shell 会读取特殊字符并将 `$test` 解释为变量 `test` 的值。没有给 `test` 赋值任何值；而是分配了一个空值。

| 命令 | 环境 |
|---|---|
| `var=$test` | `pdksh` and `bash` |
| `set var=$test` | `tsh` |

如果你用双引号括住字符串，shell 将把该字符串作为单个命令执行：

| 命令 | 环境 |
|---|---|
| `x="abc def"` | `pdksh` and `bash` |
| `set x="abc def"` | `tsh` |

## 使用反引号用输出替换字符串

你可以使用反引号（`` ` ``）来指示 shell 将字符串替换为输出。例如，如果你想统计当前目录下名为 `test.txt` 的文件的行数，并将结果存储在名为 `var` 的变量中，可以使用以下命令：

| 命令 | 环境 |
|---|---|
| `var=`wc -l test.txt`` | `pdksh` and `bash` |
| `set var=`wc -l test.txt`` | `tsh` |

```bash
echo "string1 not equal to string2"
fi
```

```bash
if [ $string2 != string1 ]; then
  echo "string2 not equal to string1"
else
  echo "string2 equal to string2"
fi
```

```bash
if [ $string1 ]; then
  echo "string1 is not empty"
else
  echo "string1 is empty"
fi
```

```bash
if [ -n $string2 ]; then
  echo "string2 has a length greater than zero"
else
  echo "string2 has length equal to zero"
fi
```

```bash
if [ -z $string1 ]; then
  echo "string1 has a length equal to zero"
else
  echo "string1 has a length greater than zero"
fi
```

如果你执行 `compare1`，你将得到以下结果：

`string1 not equal to string2`
`string2 not equal to string1`
`string1 is not empty`
`string2 has a length greater than zero`
`string1 has a length greater than zero`

如果两个字符串的大小不相等，系统会在比较时用较短的字符串末尾填充空格。也就是说，如果 `string1` 的值为 `abc`，而 `string2` 的值为 `ab`，则 `string2` 将在末尾填充一个空格以用于比较——它的值变为 `ab`。

## 表达式的比较

### 数字比较

可以使用以下运算符来比较两个数字：

- `eq`—比较两个数字是否相等
- `ge`—比较一个数字是否大于或等于另一个数字
- `le`—比较一个数字是否小于等于另一个数字
- `ne`—比较两个数字是否相等
- `gt`—比较一个数字是否大于另一个数字
- `lt`—比较一个数字是否小于另一个数字

以下 Shell 程序比较了三个数字：`number1`、`number2` 和 `number3`：

```bash
#!/bin/sh
number1=5
number2=10
number3=5
if [ $number1 -eq $number3 ]; then
    echo "number1 is equal to number3"
else
    echo "number1 is not equal to number3"
fi
if [ $number1 -ne $number2 ]; then
    echo "number1 is not equal to number2"
else
    echo "number1 is equal to number2"
fi
if [ $number1 -gt $number2 ]; then
    echo "number1 is greater than number2"
else
    echo "number1 is not greater than number2"
fi
if [ $number1 -ge $number3 ]; then
    echo "number1 is greater than or equal to number3"
else
    echo "number1 is not greater than or equal to number3"
fi
if [ $number1 -lt $number2 ]; then
echo "number1 is less than number2"
else
echo "number1 is not less than number2"
fi
if [ $number1 -le $number3 ]; then
echo "number1 is less than or equal to number3"
else
echo "number1 is not less than or equal to number3"
fi
```

执行该 Shell 程序时，你将得到以下结果：

- `number1 is equal to number3`
- `number1 is not equal to number2`
- `number1 is not greater than number2`
- `number1 is greater than or equal to number3`
- `number1 is less than number2`
- `number1 is less than or equal to number3`

### 文件运算符

可以使用以下运算符作为文件比较运算符：

- `d`—确定一个文件是否为目录
- `f`—确定一个文件是否为普通文件
- `r`—确定文件是否设置了读取权限
- `s`—确定文件是否存在且长度大于零
- `w`—确定文件是否设置了写权限
- `x`—确定文件是否设置了执行权限

假设 Shell 程序 `compare3` 位于当前目录下，该目录下包含一个名为 `file` 的文件和一个子目录 `dir`。假设 `file` 的权限为 `r-x`（读取、执行权限），`dir` 的权限为 `rwx`（权限）。该 Shell 程序的代码如下：

```bash
#!/bin/sh
if [ -d $dir ]; then
echo "dir is a directory"
else
echo "dir is not a directory"
fi
if [ -f $dir1 ]; then
echo "$dir1 is a regular file"
else
echo "$dir1 is not a regular file"
fi
if [ -r $file1 ]; then
echo "$file1 has read permission"
else
echo "$file1 does not have read permission"
fi
if [ -w $file1 ]; then
echo "$file1 has write permission"
else
echo "$file1 does not have write permission"
fi
if [ -x $dir1 ]; then
echo "$dir1 has execute permission"
else
echo "$dir1 does not have execute permission"
fi
```

执行该 Shell 程序，你将得到以下结果：
`dir1 is a directory`
`file1 is a regular file`
`file1 has read permission`
`file1 does not have write permission`
`dir1 has execute permission`

### 逻辑运算符

逻辑运算符用于使用布尔逻辑比较表达式，布尔逻辑使用代表 NOT（非）、AND（与）和 OR（或）的字符来比较值。

- `!`—取反
- `a`—与 (AND)
- `o`—或 (OR)

## 第 22 章 Shell 脚本

如果你执行文件 `compare3`，将得到以下结果：

```
dir1 is a directory
file1 is a regular file
file1 has read permission
file1 does not have write permission
dir1 has execute permission
file1 has greater than zero length
```

### 逻辑运算符
逻辑运算符用于条件语句。这些运算符用于否定逻辑表达式，或执行逻辑与（AND）和逻辑或（OR）。

- `!` : 否定逻辑表达式
- `&&` : 对两个逻辑表达式执行逻辑与
- `||` : 对两个逻辑表达式执行逻辑

此示例使用了之前 `compare3` 示例中提到的文件和目录。

```tcsh
bin/tcsh
if ( -x file1 && -x dir1 ) then
echo file1! and dir1 are executable
else
echo at least one of file1 or dir1 are executable
defif
```

```tcsh
if ( -w file1 || -w dir1 ) then
echo file1! or dir1 are writable
else
echo neither file1! or dir1 are executable
defif
```

```tcsh
if ( -w file1 ) then
echo file1! is not writable
else
echo file1! is writable
defif
```

如果你执行逻辑，它将产生以下结果：

```
file1 and dir1 are executable
file1 or dir1 are writable
file1! is not writable
```

## 迭代语句

迭代语句用于重复迭代语句内部包含的一系列命令。

### for 语句

`for` 语句用于在每当指定条件为真时执行一组命令。`for` 语句有多种格式。`pdksh` 和 `bash` 使用的第一种格式如下：

```bash
for curvar in list
do
  statements
done
```

如果你想对 `list` 中的每个值执行一次语句，则应使用这种形式。对于每次迭代，`list` 的当前值会被赋值给 `curvar`。`list` 可以是一个包含多个项的变量，也可以是一个由空格分隔的值列表。第二种格式如下：

```bash
for curvar
do
  statements
done
```

在此种形式下，语句会为传递给 shell 程序的每个位置参数执行一次。对于每次迭代，位置参数的当前值会被赋值给变量 `curvar`。

这种形式也可以写成：

```bash
for curvar in $@
do
  statements
done
```

记住，`$@` 会给你提供传递给 shell 程序的位置参数列表，其引用方式与用户最初调用命令的方式一致。

在 `tcsh` 中，`for` 语句被称为 `foreach`。其格式如下：

```tcsh
foreach curvar (list)
  statements
end
```

在此种形式下，语句会为 `list` 中的每个值执行一次，对于每次迭代，`list` 的当前值会被赋值给 `curvar`。

假设你想为目录中的每个文件在子目录 `backup` 创建备份版本。你可以在 `pksh` 和 `bash` 中执行操作：

```bash
#!/bin/sh
for filename in *
do
  cp $filename backup/$filename
  if [ $? -ne 0 ]; then
    echo "copy for $filename failed"
  fi
done
```

在前面的示例中，创建了每个文件的备份副本。如果复制失败，则会生成消息。

在 `tcsh` 中相同的示例如下：

```tcsh
#!/bin/ls
foreach filename ('/bin/ls')
  cp $filename backup/$filename
  if ($? != 0) then
    echo "copy for $filename failed"
  endif
end
```
