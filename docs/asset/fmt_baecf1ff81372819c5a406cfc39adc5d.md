
# 编写并执行 Shell 脚本

```
pdksh and bash:
var='test string'
newvar='Value of var is $var'
echo $newvar

tsh:
set var = 'test string'
set newvar = 'Value of var is $var'
echo $newvar
```

如果你执行包含这三行的 shell 程序，你将得到以下结果：

`Value of var is $var`

正如你所示，变量 `var` 在结果中保持其原始格式，而不是被扩展。

## 使用反斜杠作为转义字符

正如你之前学到的，反斜杠（`\`）充当转义字符，停止 shell 将其后的字符解释为特殊字符。假设你想给名为 `var` 的变量赋值为 `$test`。如果你使用以下命令，shell 会读取特殊字符 `$` 并将 `$test` 解释为变量 `test` 的值。`test` 没有被赋值值；`var` 中存储了一个空值，如下：

| 命令 | 环境 |
| --- | --- |
| `var=$test` | `pdksh` 和 `bash` |
| `set var=$test` | `Tcsh` |

不幸的是，这种赋值在 `bash` 中可能有效，但如果你在 `tcsh` 中使用它。请使用以下命令正确地将 `$test` 存储在 `var` 中：

| 命令 | 环境 |
| --- | --- |
| `var=\test` | `pdksh` 和 `bash` |
| `set var = \$test` | `Tcsh` |

美元符号之前的反斜杠（`\$`）指示 shell 将 `$` 解释为任何其他普通字符，而不是赋予任何特殊含义。你也可以在 `$test` 变量周围使用单引号（`''`）获得相同的结果。

## 使用反引号用输出替换字符串

你可以使用反引号（`` ` ``）字符指示 shell 在执行时将字符串替换为它的输出。这被称为命令替换。当你需要命令的结果时，可以在 shell 程序中使用这种特殊字符。

# 编写和执行 Shell 脚本

如果两个字符串的长度不相等，系统会在较短的字符串末尾填充空格以便比较。也就是说，如果 `string1` 的值为 "abc"，而 `string2` 的值为 "ab"，则为了进行比较，`string2` 的末尾会填充一个空格；其值将变为 "ab *（在字母后有一个空格）"。

## 数字比较

可以使用以下运算符来比较两个数字：

- `-eq`: 比较两个数字是否相等。
- `-ge`: 比较一个数字是否大于等于另一个数字。
- `-le`: 比较一个数字是否小于等于另一个数字。
- `-ne`: 比较两个数字是否不相等。
- `-gt`: 比较一个数字是否大于另一个。
- `-lt`: 比较一个数字是否小于另一个。

以下 Shell 程序比较三个数字——`number1`、`number2` 和 `number3`：

```
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

当您执行该 Shell 程序时，将获得结果：

number1 is equal to number3
number1 is not equal to number2
number1 is not greater than number2
number1 is greater than or equal to number3
number1 is less than number2
number1 is less than or equal to number3

## 文件运算符

可以使用以下运算符作为文件比较运算符：

- `-d`: 确定文件是否为目录。
- `-f`: 确定文件是否为常规普通文件。
- `-r`: 确定文件是否具有读取权限。
- `-s`: 确定文件是否存在且长度是否大于零。
- `-w`: 确定文件是否具有写入权限。
- `-x`: 确定文件是否具有执行权限。

假设当前目录下有一个名为 `compare3` 的 Shell 程序，其中包含一个名为 `file1` 的文件和一个名为 `dir1` 的子目录。假设 `file1` 的权限为 `r-x`（读取和执行权限），`dir1` 的权限为 `rwx`（读、写和执行权限）。该 Shell 程序的代码如下：

```
#!/bin/sh

if [ -d $dir1 ]; then

    echo "dir1 is a directory"

else

    echo "dir1 is not a directory"

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

如果您执行该 Shell 程序，将得到以下结果：

dir1 is a regular file
file1 is a regular file
file1 has read permission
file1 does not have write permission
dir1 has execute permission

### 逻辑运算符

逻辑运算符用于使用布尔逻辑比较表达式，布尔逻辑比较代表非（NOT）、与（AND）和或（OR）的字符：

- `!`: 对逻辑表达式取反。
- `-a`: 对两个逻辑表达式进行逻辑与。
- `-o`: 对两个逻辑表达式进行逻辑或。

这个名为 `logic` 的示例使用了之前 `compare3` 示例中提到的文件和目录：

```
#!/bin/sh

if [ -x $file1 -a $dir1 ]; then

    echo "$file1 and $dir1 are executable"

else

    echo at least one of file1 or dir1 are not executable

fi

if [ -w file1 ] -o -w dir1 ]; then

    echo file1 or dir1 are writable

else

    echo neither file1 or dir1 are executable

fi

if [ ! -w file1 ]; then

    echo file1 is not writable

else

    echo file1 is writable

fi
```
