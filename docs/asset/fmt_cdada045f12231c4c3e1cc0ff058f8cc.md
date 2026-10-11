
仅仅在脚本中使用大于符号本身不会产生错误，但结果是错误的。脚本将大于符号解释为输出重定向（参见第 15 章）。因此，它创建了一个名为 `zorfootball` 的文件。由于重定向成功完成，测试条件返回 0 退出状态代码，`if` 语句将其评估为一切正常完成！

要修复这个问题，你需要使用反斜杠（`\`）正确转义大于符号：

```bash
$ cat good_string_comparison.sh
#!/bin/bash
# 正确使用字符串比较
#
string1=soccer
string2=zorfootball
#
if [ $string1 \> $string2 ]
then
    echo "$string1 大于 $string2"
else
    echo "$string1 小于 $string2"
fi
$
$ rm -i zorfootball
rm: 移除常规空文件 'zorfootball'? y
$
$ ./good_string_comparison.sh
soccer 小于 zorfootball
$
$ ls z*
ls: 无法访问 'z*': 没有那个文件或目录
$
```

现在这个回答更接近你期望的字符串比较结果。

> **注意**
>
> `soccer` 字符串小于 `zorfootball` 字符串，因为测试比较使用每个字符的 Unicode 数值。小写 `s` 对应 115，而 `z` 是 122。因此，`s` 小于 `z`，所以 `soccer` 小于 `zorfootball`。

第二个问题稍微微妙一些，除非你正在处理大小写字母，否则你可能甚至不会遇到它。`sort` 命令处理大写字母的方式与 `test` 条件考虑的方式相反：

```bash
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
# 测试字符串排序顺序
#
string1=Soccer
string2=soccer
#
if [ $string1 \> $string2 ]
then
    echo "$string1 大于 $string2"
else
    echo "$string1 小于 $string2"
fi
$
$ ./sort_order_comparison.sh
Soccer 小于 soccer
$
```

在 `test` 比较中，大写字母被视为小于小写字母。然而，`sort` 命令则相反。当你将相同的字符串放入文件并使用 `sort` 命令时，小写字母会首先出现。这是由于不同的排序技术所致。

`test` 比较使用标准的 Unicode 顺序，利用每个字符的 Unicode 数值来确定排序顺序。`sort` 命令使用系统区域设置语言定义中的排序顺序。对于英语，区域设置指定在排序顺序中小写字母出现在大写字母之前。

> **注意**
>
> `test` 命令和 `test` 表达式在字符串比较中使用标准的数学比较符号，在数值比较中使用文本代码。这是一个许多程序员容易弄反的微妙特性。如果你对数值使用数学比较符号，shell 会将它们解释为字符串值，并且可能无法产生正确的结果。

# 第二部分：Shell 脚本编程基础

## 查看字符串大小

当你试图评估变量是否包含数据时，`-n` 和 `-z` 比较非常有用：

```bash
$ cat variable_content_eval.sh
#!/bin/bash
# 测试字符串长度
#
string1=Soccer
string2=''
#
if [ -n $string1 ]
then
        echo "字符串 '$string1' 不为空"
else
        echo "字符串 '$string1' 为空"
fi
#
if [ -z $string2 ]
then
        echo "字符串 '$string2' 为空"
else
        echo "字符串 '$string2' 不为空"
fi
#
if [ -z $string3 ]
then
        echo "字符串 '$string3' 为空"
else
        echo "字符串 '$string3' 不为空"
fi
$
$ ./variable_content_eval.sh
字符串 'Soccer' 不为空
字符串 '' 为空
字符串 '' 为空
$ 
```

此示例创建了两个字符串变量。`*string1*` 变量包含一个字符串，而 `*string2*` 变量被创建为空字符串。进行了以下比较：

```bash
if [ -n $string1 ]
```

前面的代码确定 `*string1*` 变量的长度是否非零，其长度确实非零，因此处理其 `then` 部分。

```bash
if [ -z $string2 ]
```

前面的代码确定 `*string2*` 变量的长度是否为零，其长度确实为零，因此处理其 `then` 部分。

```bash
if [ -z $string3 ]
```

前面的代码用于判断 `string3` 变量的长度是否为零。由于该变量从未在 shell 脚本中定义过，因此表明字符串长度仍为零，即使它并未被定义。

> **警告**
>
> 空变量和未初始化的变量可能会对你的 shell 脚本测试产生灾难性的影响。如果你不确定变量的内容，最好在使用 `-n` 或 `-z` 测试变量是否包含值之前再将其用于数值或字符串比较。

## 使用文件比较

测试比较的最后一类很可能是 shell 脚本中最强大且使用最广泛的比较方式。这一类别允许你测试 Linux 文件系统中文件和目录的状态。表 12.3 列出了这些比较操作。

**表 12.3 test 文件比较操作**

| 比较操作 | 描述 |
| :--- | :--- |
| `-d file` | 检查 `file` 是否存在且为目录 |
| `-e file` | 检查 `file` 是否存在 |
| `-f file` | 检查 `file` 是否存在且为普通文件 |
| `-r file` | 检查 `file` 是否存在且可读 |
| `-s file` | 检查 `file` 是否存在且非空 |
| `-w file` | 检查 `file` 是否存在且可写 |
| `-x file` | 检查 `file` 是否存在且可执行 |
| `-O file` | 检查 `file` 是否存在且由当前用户所有 |
| `-G file` | 检查 `file` 是否存在且默认组与当前用户所属组相同 |
| `file1 -nt file2` | 检查 `file1` 是否比 `file2` 更新 |
| `file1 -ot file2` | 检查 `file1` 是否比 `file2` 更旧 |

这些条件使你能在 shell 脚本中检查文件系统中的文件。它们常用于访问文件的脚本中。由于它们被频繁使用，让我们逐一看看这些条件。

### 检查目录

`-d` 测试用于检查指定的目录是否存在于系统中。如果你试图向目录写入文件或在更改到某个目录位置之前，这通常是个不错的选择：

```bash
$ cat jump_point.sh
#!/bin/bash
# Look before you leap
#
jump_directory=/home/Torfa
#
if [ -d $jump_directory ]
then
    echo "The $jump_directory directory exists."
    cd $jump_directory
    ls
else
    echo "The $jump_directory directory does NOT exist."
fi
$
$ ./jump_point.sh
The /home/Torfa directory does NOT exist.
$
```

`-d` 测试条件检查 `jump_directory` 变量的目录是否存在。如果存在，它将继续使用 `cd` 命令切换到当前目录并执行目录列表显示。如果不存在，脚本会发出警告消息并退出脚本。

### 检查对象是否存在

`-e` 比较操作允许你在脚本中尝试使用文件或目录对象之前，检查其是否存在：
