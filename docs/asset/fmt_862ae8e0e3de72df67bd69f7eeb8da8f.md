
本节涵盖了使用`pdksh`或`bash` shell的比较操作。在本章的后面部分，你将学习如何在`test` shell中比较表达式。

`pdksh`和`bash`的shell语法提供了一个名为`test`的命令来比较字符串、数字和文件。`test`命令的语法如下：

```
test expression
or
[ expression ]
```

`pdksh`和`bash`以相同的方式处理两种形式的`test`命令。`test`命令支持以下类型的比较：

- 字符串比较
- 数值比较
- 文件操作符
- 逻辑运算符

## 字符串比较

你可以使用以下运算符来比较两个字符串表达式：

- `=` 比较两个字符串是否相等
- `!=` 比较两个字符串是否不等
- `-n` 评估字符串长度是否大于零
- `-z` 评估字符串长度是否等于零

以下是在一个名为`compare`的shell程序中比较两个字符串`string1`和`string2`时使用这些运算符的示例：

```
#!/bin/sh
string1="abc"
string2="abd"
if [ $string1 = $string2 ]; then
echo "string1 equal to string2"
else
echo "string1 not equal to string2"
fi
```

```
if [ $string2 != $string1 ]; then
echo "string2 not equal to string1"
else
echo "string2 equal to string2"
fi
```

```
if [ $string1 ]; then
echo "string1 is not empty"
else
echo "string1 is empty"
fi
```

```
if [ -n $string2 ]; then
echo "string2 has a length greater than zero"
else
echo "string2 has length equal to zero"
fi
```

```
if [ -z $string1 ]; then
echo "string1 has a length equal to zero"
else
echo "string1 has a length greater than zero"
fi
```

如果你执行`compare`，将得到以下结果：

```
string1 not equal to string2
string2 not equal to string1
string1 is not empty
string2 has a length greater than zero
string1 has a length the shorter string with trailing
```

## 数值比较

可以使用以下运算符比较两个数字：

- `-eq` 比较两个数字是否相等
- `-ge` 比较一个数字是否大于或等于另一个
- `-le` 比较一个数字是否小于或等于另一个
- `-ne` 比较两个数字是否不等
- `-gt` 比较一个数字是否大于另一个
- `-lt` 比较一个数字是否小于另一个

以下脚本用于比较两个数字`num1`和`num2`：

```bash
#!/bin/sh
num1=10
num2=20
if [ $num1 -eq $num2 ]; then
echo "num1 is equal to num2"
else
echo "num1 is not equal to num2"
fi
```

```
if [ $num1 -ge $num2 ]; then
echo "num1 is greater than or equal to num2"
else
echo "num1 is not greater than or equal to num2"
fi
```

```
if [ $num1 -le $num2 ]; then
echo "num1 is less than or equal to num2"
else
echo "num1 is not less than or equal to num2"
fi
```

```
if [ $num1 -ne $num2 ]; then
echo "num1 is not equal to num2"
else
echo "num1 is equal to num2"
fi
```

```
if [ $num1 -gt $num2 ]; then
echo "num1 is greater than num2"
else
echo "num1 is not greater than num2"
fi
```

```
if [ $num1 -lt $num2 ]; then
echo "num1 is less than num2"
else
echo "num1 is not less than num2"
fi
```

## 文件操作符

可以使用以下操作符来检查文件：

- `-d` 检查路径是否为目录
- `-f` 检查是否为普通文件
- `-r` 检查文件是否可读
- `-w` 检查文件是否可写
- `-x` 检查文件是否可执行
- `-s` 检查文件大小是否大于零

以下是一个名为`file_test`的示例程序，演示了这些操作符的使用：

```bash
#!/bin/sh
file="test.txt"
if [ -d $file ]; then
echo "$file is a directory"
else
echo "$file is not a directory"
fi

if [ -f $file ]; then
echo "$file is a regular file"
else
echo "$file is not a regular file"
fi

if [ -r $file ]; then
echo "$file is readable"
else
echo "$file is not readable"
fi

if [ -w $file ]; then
echo "$file is writable"
else
echo "$file is not writable"
fi

if [ -x $file ]; then
echo "$file is executable"
else
echo "$file is not executable"
fi

if [ -s $file ]; then
echo "$file is not empty"
else
echo "$file is empty"
fi
```

## 逻辑运算符

你可以使用以下逻辑运算符来组合多个测试条件：

- `!` 取反一个逻辑表达式
- `-a` 逻辑与（AND）
- `-o` 逻辑或（OR）

以下是使用逻辑运算符的示例：

```bash
#!/bin/sh
if [ -f test.txt -a -r test.txt ]; then
echo "test.txt exists and is readable"
else
echo "test.txt does not exist or is not readable"
fi

if [ -f test.txt -o -w test.txt ]; then
echo "test.txt exists or is writable"
else
echo "test.txt does not exist and is not writable"
fi

if [ ! -r test.txt ]; then
echo "test.txt is not readable"
else
echo "test.txt is readable"
fi
```

```bash
if (string1 == string2) then
    echo "string1 equal to string2"
else
    echo "string1 not equal to string2"
endif
```

```bash
if (string2 != string1) then
    echo "string2 not equal to string1"
else
    echo "string2 equal to string1"
endif
```

如果你执行`compare`，你将得到以下结果：

```
string1 not equal to string2
string2 not equal to string1
```

# 数字比较

你可以使用以下操作符来比较两个数字：

- `>=` 用于比较一个数字是否大于或等于另一个
- `<=` 用于比较一个数字是否小于或等于另一个
- `>` 用于比较一个数字是否大于另一个
- `<` 用于比较一个数字是否小于另一个

接下来的示例在一个名为`compare2`的shell程序中比较了三个数字：`number1`、`number2`和`number3`。 
