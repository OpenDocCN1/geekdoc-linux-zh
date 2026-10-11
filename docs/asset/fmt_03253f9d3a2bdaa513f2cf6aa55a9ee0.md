
```
$ cat bad_string_comparison.sh
#!/bin/bash
# Misusing string comparisons
#
string1=soccer
string2=zorbffootball
#
if [ $string1> $string2 ]
then
    echo "$string1 is greater than $string2"
else
    echo "$string1 is less than $string2"
fi
$
$ ./bad_string_comparison.sh
soccer is greater than zorbffootball
$
$ ls z*
zorbffootball
$
```

仅仅在脚本中使用大于符号本身，不会生成错误，但结果是错误的。脚本将大于符号解释为输出重定向（参见 [第 15 章](#chapter-15)）。因此，它创建了一个名为 `zorbffootball` 的文件。由于重定向成功完成，测试条件返回零退出状态码，`if` 语句将其评估为事情成功完成！

要解决这个问题，你需要使用反斜杠 `\` 正确转义大于符号：

```
$ cat good_string_comparison.sh
#!/bin/bash
# Properly using string comparisons
#
string1=soccer
string2=zorbffootball
#
if [ $string1 \> $string2 ]
then	echo "$string1 is greater than $string2"
else	echo "$string1 is less than $string2"
fi
$
$ rm -i zorbfutbol1
rm: remove regular empty file 'zorbfutbol1'? y
$
$ ./good_string_comparison.sh
soccer is less than zorbfutbol1
$ ls z*
ls: cannot access 'z\*': No such file or directory
$
```

现在那个答案更接近你从字符串比较中预期的结果。

### 注意

> 字符串 `soccer` 小于字符串 `zorbfutbol1`，因为测试比较使用每个字符的 Unicode 数值。小写 `s` 等于 115，而 `z` 是 122。因此，`s` 小于 `z`，从而 `soccer` 小于 `zorbfutbol1`。

第二个问题要微妙一些，除非你处理大写字母和小写字母，否则你可能甚至不会遇到它。`sort` 命令处理大写字母的方式与测试条件考虑的方式相反：

```
$ cat SportsFile.txt
Soccer
soccer
$
$ sort SportsFile.txt
soccer
Soccer
$
$ cat sort_order_comparison.sh
#!/bin/bash
# Testing string sort order
#
string1=Soccer
string2=soccer
#
if [ $string1 \> $string2 ]
then	echo "$string1 is greater than $string2"
else	echo "$string1 is less than $string2"
fi
$
$ ./sort_order_comparison.sh
Soccer is less than soccer
$
```

在测试比较中，大写字母被视为小于小写字母。然而，`sort` 命令的做法恰恰相反。当你将相同的字符串放入文件并使用 `sort` 命令时，小写字母首先出现。这是由于不同的排序技术。

测试比较使用标准的 Unicode 排序，使用每个字符的 Unicode 数值来确定排序顺序。`sort` 命令使用系统区域语言设置定义的排序顺序。对于英语，区域设置指定在排序顺序中小写字母出现在大写字母之前。

### 注意

> `test` 命令和测试表达式使用标准的数学比较符号进行字符串比较，使用文本代码进行数值比较。这是一个许多程序员设法弄反的微妙特性。如果你对数值使用数学比较符号，shell 会将它们解释为字符串值，可能无法产生正确的结果。

#### 查看字符串大小

在评估变量是否包含数据时，`-n` 和 `-z` 比较非常实用：

```bash
$ cat variable_content_eval.sh
#!/bin/bash
# 测试字符串长度
#
string1=Soccer
string2=''
#
if [ -n $string1 ]
then	echo "字符串 '$string1' 不为空"
else	echo "字符串 '$string1' 为空"
fi
#
if [ -z $string2 ]
then	echo "字符串 '$string2' 为空"
else	echo "字符串 '$string2' 不为空"
fi
#
if [ -z $string3 ]
then	echo "字符串 '$string3' 为空"
else	echo "字符串 '$string3' 不为空"
fi
$
$ ./variable_content_eval.sh
字符串 'Soccer' 不为空
字符串 '' 为空
字符串 '' 为空
$
```

此示例创建了两个字符串变量。`string1` 变量包含一个字符串，而 `string2` 变量被创建为空字符串。执行了以下比较：

```
if [ -n $string1 ]
```

上述代码确定 `string1` 变量的长度是否非零。由于它确实非零，因此处理其 `then` 部分。

```
if [ -z $string2 ]
```

上述代码确定 `string2` 变量的长度是否为零。由于它确实为零，因此处理其 `then` 部分。

```
if [ -z $string3 ]
```

上述代码确定 `string3` 变量的长度是否为零。该变量从未在 shell 脚本中定义，因此表明即使未定义，其字符串长度仍被视为零。

> **警告**
>
> 空变量和未初始化的变量可能会对你的 shell 脚本测试产生灾难性影响。如果你不确定变量的内容，最好在将其用于数值或字符串比较之前，使用 `-n` 或 `-z` 测试该变量是否包含值。

#### 使用文件比较

测试比较的最后一类包括 shell 脚本中可能最强大且使用最广泛的比较。此类允许你测试 Linux 文件系统中文件和目录的状态。表 12-3 列出了这些比较。

##### 表 12-3 测试文件比较

| 比较 | 描述 |
| :--- | :--- |
| `-d file` | 检查文件是否存在且为目录。 |
| `-e file` | 检查文件是否存在。 |
| `-f file` | 检查文件是否存在且为普通文件。 |
| `-r file` | 检查文件是否存在且可读。 |
| `-s file` | 检查文件是否存在且不为空。 |
| `-w file` | 检查文件是否存在且可写。 |
| `-x file` | 检查文件是否存在且可执行。 |
| `-o file` | 检查文件是否存在且由当前用户拥有。 |
| `-G file` | 检查文件是否存在且默认组与当前用户相同。 |
| `file1 -nt file2` | 检查 `file1` 是否比 `file2` 更新。 |
| `file1 -ot file2` | 检查 `file1` 是否比 `file2` 更旧。 |

这些条件使你能在 shell 脚本中检查文件系统文件。它们常用于访问文件的脚本中。由于使用非常频繁，让我们逐一查看它们。

##### 检查目录

`-d` 测试检查指定目录是否存在于系统中。如果你试图向目录写入文件或尝试更改到某个目录位置，这通常是件好事：

```bash
$ cat jump_point.sh
#!/bin/bash
# 跳跃前先查看
#
jump_directory=/home/Torfa
#
if [ -d $jump_directory ]
then
	echo "$jump_directory 目录存在。"
	cd $jump_directory
	ls
else
	echo "$jump_directory 目录不存在。"
fi
$ ./jump_point.sh
/home/Torfa 目录不存在。
$
```

`-d` 测试条件检查 `jump_directory` 变量的目录是否存在。如果存在，它继续执行 `cd` 命令更改到当前目录并执行目录列表。如果不存在，脚本会发出警告消息并退出脚本。

##### 检查对象是否存在

`-e` 比较允许你在尝试在脚本中使用文件或目录对象之前，检查其是否存在：
