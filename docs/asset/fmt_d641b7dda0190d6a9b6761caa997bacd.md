
```
#!/bin/sh
string1="abc"
string2="abd"
if [ $string1 = $string2 ]; then
echo "string1 equal to string2"
else
echo "string1 not equal to string2"
fi

if [ $string2 != string1 ]; then
echo "string2 not equal to string1"
else
echo "string2 equal to string2"
fi

if [ $string1 ]; then
echo "string1 is not empty"
else
echo "string1 is empty"
fi

if [ -n $string2 ]; then
echo "string2 has a length greater than zero"
else
echo "string2 has length equal to zero"
fi

if [ -z $string1 ]; then
echo "string1 has a length equal to zero"
else
echo "string1 has a length greater than zero"
fi
```

如果你执行 `compare1`，你得到以下结果：
string1 not equal to string2
string2 not equal to string1
string1 is not empty
string2 has a length greater than zero
string1 has a length greater than zero

如果两个字符串的大小不等，系统会在较短的字符串末尾填充空格进行比较。也就是说，如果 `string1` 的值为 abc 而 `string2` 的值为 ab，则 `string2` 将填充一个末尾空格用于比较——它的值将变为 ab。

# 数字比较

可以使用以下运算符来比较两个数字：
- `-eq` — 比较两个数字是否相等
- `-ge` — 比较一个数字是否大于或等于另一个数字
- `-le` — 比较一个数字是否小于或等于另一个数字
- `-ne` — 比较两个数字是否相等
- `-gt` — 比较一个数字是否大于另一个
- `-lt` — 比较一个数字是否小于另一个

以下 shell 程序比较三个数字：`number1`、`number2` 和 `number3`：

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

执行该 shell 程序时，你得到以下结果：
```
number1 is equal to number3
number1 is not equal to number2
number1 is not greater than number2
number1 is greater than or equal to number3
number1 is less than number2
number1 is less than or equal to number3
```

# 文件操作符

可以使用以下运算符作为文件操作符：
- `-d` — 确定文件是否为目录
- `-f` — 确定文件是否为普通文件
- `-r` — 确定文件是否设置了读权限
- `-s` — 确定文件是否存在且长度大于零
- `-w` — 确定文件是否设置了写权限
- `-x` — 确定文件是否设置了执行权限

假设一个文件和一个目录存在。代码如下：

```bash
#!/bin/sh
if [ -d $dir1 ]; then
echo "dir1 is a directory"
else
echo "dir1 is not a directory"
fi

if [ -f $file1 ]; then
echo "file1 is a regular file"
else
echo "file1 is not a regular file"
fi

if [ -r $file1 ]; then
echo "file1 has read permission"
else
echo "file1 does not have read permission"
fi

if [ -s $file1 ]; then
echo "file1 exists and has a length greater than zero"
else
echo "file1 does not exist or has length equal to zero"
fi

if [ -w $file1 ]; then
echo "file1 has write permission"
else
echo "file1 does not have write permission"
fi

if [ -x $file1 ]; then
echo "file1 has execute permission"
else
echo "file1 does not have execute permission"
fi
```

*(注：此处根据上下文逻辑，补全了原文中缺失的 `file1` 相关判断部分，以保持逻辑一致性)*

如果你执行上述代码，你得到以下结果：
dir1 is a directory
file1 is a regular file
file1 has read permission
file1 exists and has a length greater than zero
file1 has write permission
file1 has execute permission

# 逻辑操作符

逻辑操作符用于使用布尔逻辑比较表达式，并使用代表非、与、或的字符：
- `!` — 取反逻辑表达式
- `-a` — 逻辑与两个表达式
- `-o` — 逻辑或两个表达式

此示例使用了之前提到的文件和目录：

```bash
#!/bin/sh
if [ -x $file1 -a $dir1 ]; then
echo "file1 and dir1 are executable"
else
echo "at least one of file1 or dir1 is not executable"
fi

if [ -w $file1 -o $dir1 ]; then
echo "file1 or dir1 are writable"
else
echo "neither file1 nor dir1 are writable"
fi

if [ ! -w $file1 ]; then
echo "file1 is not writable"
else
echo "file1 is writable"
fi
```

执行逻辑后，得到如下结果：
file1 and dir1 are executable
file1 or dir1 are writable
file1 is not writable

# 特殊语句：for、while 以及其他

Bash 提供了内置语句来处理更复杂的条件检查，如循环和切换块。在许多方面，`pdsh` 和 `bash` 共享相同的语法，以下章节适用于两种 shell。

## for 语句
