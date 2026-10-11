
当你添加一个条件时，它会通过 `test` 命令进行测试。例如，使用 `test` 命令，你可以判断一个变量是否包含内容。需要一个简单的条件表达式来确定变量是否包含内容：

```bash
$ cat test6.sh

!/bin/bash

# Testing the test command

#

my_variable="Full"

#
```

```bash
if test $my_variable
then
  echo "The $my_variable expression returns a True"

#
else
  echo "The $my_variable expression returns a False"
fi
$ ./test6.sh
The Full expression returns a True

$
```

变量 `my_variable` 包含内容（Full），所以当 `test` 命令检查条件时，退出状态返回零。这触发了测试代码中的语句。

正如你所料的那样，当变量不包含内容时，情况相反：

```bash
$ cat test6.sh
!/bin/bash

# Testing the test command

#
my_variable=""

#
if test $my_variable
then
  echo "The $my_variable expression returns a True"

#
else
  echo "The $my_variable expression returns a False"
fi
$ ./test6.sh
The  returns a False

$
```

Bash shell 提供了一种另一种测试条件的方法，而无需在 `if-then` 语句中声明 `test` 命令：

```bash
if [ condition ]
then
  commands
```

方括号定义了条件。注意；在第一个括号之后和最后一个括号之前必须有一个空格，否则你会得到错误。`test` 命令和 `test` 条件可以评估三类条件：

- 数值比较
- 字符串比较
- 文件比较

接下来的章节描述了如何在你的 `if-then` 语句中使用这些每一类条件。

# 使用数值比较

最常用的评估方法是对两个数值值进行比较。表 12.1 显示了用于测试两个值的参数列表。

| 比较 | 描述 |
| :--- | :--- |
| n1 -eq | 检查 n1 是否等于 n2 |
| n1 -ge | 检查 n1 是否大于或等于 n2 |
| n1 -gt | 检查 n1 是否大于 n2 |
| n1 -le | 检查 n1 是否小于或等于 n2 |
| n1 -lt | 检查 n1 是否小于 n2 |
| n1 -ne | 检查 n1 是否不等于 n2 |

由于数值比较可以评估三类条件中的第一类。下面是使用数值比较的测试示例：

```bash
$ cat numeric_test.sh

#!/bin/bash

# Testing numeric comparisons

#
n1=10
n2=20
#
if [ $n1 -eq $n2 ]; then
    echo "$n1 is equal to $n2"
fi
if [ $n1 -ge $n2 ]; then
    echo "$n1 is greater or equal to $n2"
fi
if [ $n1 -gt $n2 ]; then
    echo "$n1 is greater than $n2"
fi
if [ $n1 -le $n2 ]; then
    echo "$n1 is less or equal to $n2"
fi
if [ $n1 -lt $n2 ]; then
    echo "$n1 is less than $n2"
fi
if [ $n1 -ne $n2 ]; then
    echo "$n1 is not equal to $n2"
fi
$ ./numeric_test.sh
10 is less or equal to 20
10 is less than 20
10 is not equal to 20
```

字符串比较可以评估三类条件中的第二类。下面是使用字符串比较的测试示例：

```bash
$ cat string_test.sh

#!/bin/bash

# Testing string comparisons

#
str1="apple"
str2="orange"
#
if [ "$str1" = "$str2" ]; then
    echo "$str1 is equal to $str2"
fi
if [ "$str1" != "$str2" ]; then
    echo "$str1 is not equal to $str2"
fi
$ ./string_test.sh
apple is not equal to orange
```

文件比较可以评估三类条件中的第三类。下面是使用文件比较的测试示例：

```bash
$ cat file_test.sh

#!/bin/bash

# Testing file comparisons

#
file1="test1.txt"
file2="test2.txt"
#
touch $file1
echo "hello" > $file1
echo "world" > $file2
#
if [ -f $file1 ]; then
    echo "$file1 is a file"
fi
if [ -d $file1 ]; then
    echo "$file1 is a directory"
fi
if [ -s $file1 ]; then
    echo "$file1 is not empty"
fi
if [ -r $file1 ]; then
    echo "$file1 is readable"
fi
if [ -w $file1 ]; then
    echo "$file1 is writable"
fi
if [ -x $file1 ]; then
    echo "$file1 is executable"
fi
if [ -e $file1 ]; then
    echo "$file1 exists"
fi
if [ ! -e $file2 ]; then
    echo "$file2 does not exist"
fi
rm $file1
$ ./file_test.sh
test1.txt is a file
test1.txt is not empty
test1.txt is readable
test1.txt is writable
test1.txt exists
test2.txt does not exist
```

```bash
#
val1=baseball
val2=hockey
#
if [ $val1 > $val2 ]
then
    echo "$val1 is greater than $val2"
else
    echo "$val1 is less than $val2"
fi
$ ./badtest.sh
baseball is greater than hockey
$ ls -l hockey
-rw-r--r-- 1 rich             rich        0 Sep 30 19:08 hockey
```

在脚本中直接使用大于符号，不会产生错误，但结果是错误的。脚本将大于号解释为输出重定向（参见第 15 节）。因此，它创建了一个名为 `hockey` 的文件。由于重定向成功完成，测试条件返回零退出状态码，这会导致语句评估结果表现为操作成功完成！

要修复这个问题，你需要正确转义大于号：

```bash
$ cat test9.sh

#!/bin/bash

# mis-using string comparisons

#
val1=baseball
val2=hockey
#
if [ $val1 \> $val2 ]
then
    echo "$val1 is greater than $val2"
else
    echo "$val1 is less than $val2"
fi
$ ./test9.sh
baseball is less than hockey

$
```

现在的答案更符合你对字符串比较的预期。

第二个问题稍微微妙一些，除非你在处理大写和小写字母，否则可能根本不会遇到它。`sort` 命令处理大写字母的方式与测试条件考虑的方式相反：

```bash
$ cat test9.sh

#!/bin/bash

# testing string sort order
val1=testing
```
