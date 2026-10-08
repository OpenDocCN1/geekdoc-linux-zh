

# 高级 Bash 脚本指南

- `*` 在正则表达式中表示任意数量（或零个）的字符。

算术运算符。在算术运算上下文中，`*` 表示乘法。

- 双星号 `**` 可以表示幂运算符或扩展的文件匹配通配符（globbing）。

- `?` 测试运算符。在某些表达式中，`?` 表示对条件的测试。

在双括号结构中，`?` 可以作为 C 风格三元运算符的元素。[171]

条件?结果-如果为真:结果-如果为假

```
((var0 = var1<98?9:21 ))
#n# if [ "$var1" -lt 98 ]
# then
#   var0=0
# else
#   var0=21
# fi
```

在参数表达式中，`?` 测试变量是否已设置。

通配符。该字符在通配符的文件名扩展中作为单字符“通配符”，同时在扩展正则表达式中表示一个字符。

变量替换（变量的内容）。

```
var1=5
var2=23skidoo
echo $var1 # 5
echo $var2 # 23skidoo
```

变量名前的前缀 `$` 表示变量所持有的值。

行尾。在正则表达式中，`$` 指向文本行的末尾。

参数替换。

引号字符串扩展。此结构将将一个或多个转义的八进制或十六进制值扩展为 ASCII [18] 或 Unicode 字符。

位置参数。

退出状态变量。`$?` 变量持有命令、函数或脚本本身的退出状态。

进程 ID 变量。`$$` 变量持有其出现的脚本的进程 ID [19]。

命令组。

## 第 3 章 特殊字符

# 高级 Bash 脚本指南

```
(a=hello; echo $a)
```

在括号内的命令列表会启动一个子 shell（subshell）。

括号内（即子 shell）内部的变量对脚本的其他部分是不可见的。父进程（脚本）无法读取子进程（子 shell）创建的变量。

```
a=123
( a=321 );
echo "a = $a" # a = 123
# "a" 在括号内的作用类似于局部变量。
# 初始化。
```

## 数组扩展

```
Array=(element1 element2 element3)
{xxx,yyy,zzz,...}
```

## 大括号扩展

```
echo "{These,word,are,quoted}" # " 前缀和后缀
# "These "words" are "quoted"
```

```
cat {file1,file2,file3} > combined_file
# 将文件 file1, file2 和 file3 合并到 combined_file
```

```
cp file22.{txt,backup} "file22.backup"
# 将 "file22.txt" 复制到 "file22.backup"
```

命令可以对大括号内逗号分隔的文件列表进行操作。[20] 文件名扩展（通配符）适用于括号内的文件规格。

大括号内不允许有空格，除非空格经过转义。

```
echo {file1,file2\}: \"A,\"B\",\ 'C'
```

```
file : file1 : B file1 : C file2 : A file2 : B file2 :
C
```

```
{a..z}
```

## 扩展扩展 [a..z]

```
echo [a..z] # a b c d e f g h i j k l m n o p q r s t v w x y z
# 输出 a 到 z 之间的字符。
```

```
echo (0..3) # 0 1 2 3
# 输出 0 到 3 之间的字符。
```

```
base64-char={A..Z} {a..z} {0..9} + =
# 使用扩展大括号扩展初始化数组。
# 来自 vlad 的 "base64.sh" 示例脚本。
```

`{a..z}` 扩展大括号扩展是 Bash 版本 3 中引入的特性。

代码块 [大括号]。也称为内联组（inline group），此结构创建一个匿名函数（没有名字的函数）。然而，与“标准”函数不同，

## 第 3 章 特殊字符

# 高级 Bash 脚本指南

块内部的变量对脚本的剩余部分仍然可见。

```bash
bash$ { local a;
  a=123; }
# 仅能在函数中使用
echo "a" # 空（块内部的值）
# 感谢 S。
```

在大括号内的代码块有 I/O 重定向输入输出。

## 示例 3-1. 代码块和 I/O 重定向

```bash
#!/bin/bash
# 读取 /etc/fstab 中的行。

File=/etc/fstab

{
  read line1
  read line2
} < $File

echo "First line in $File is:"
echo "$line1"
echo "Second line in $File is:"
echo "$line2"

exit 0

# 现在，如何解析每行的独立字段？提示：使用 awk 或 "set"。
```

## 示例 3-2. 将代码块的输出保存到文件

```bash
#!/bin/bash
# rpm-check.sh

# 查询 rpm文件的描述、列表以及是否可以安装。
SUCCESS=0
E_NOARGS=65

if [ -z "$1" ]
then
    echo "Usage: `basename $0` -file"
    echo "Archive Description:"
    echo "Archive Listing:"
    rpm -q $1 # 查询文件是否可以安装。
    echo "$1 can be installed."
else
    echo "$1 cannot be installed."
fi

# 代码块结束。
# 重定向块中所有内容的输出到文件。
> "$1.test"

echo "Results of test in file $1.test"
# 选项解释请参见 rpm man 手页。
exit 0
```

与上述命令组（括号）不同，由 `{}` 括起来的代码块通常会启动一个子 shell。可以使用非标准循环（替换字符串）来迭代代码块。`{}` 双括号是输出文本的占位符。

```
ls | xargs -i cp ./1
# 来自 "ex42.sh" (copydir.sh) 示例。
```

路径。主要用于 find 结构。这不是一个内置命令。定义：路径是一个包含完整路径的文件名。/home/bozo/Thursday/schedule.txt。这有时被称为绝对路径。

find 命令的 -exec 选项。需要防止 shell 解释。

第 3 章 特殊字符

# 高级 Bash 脚本指南

测试表达式之间的 `[ ]`。注意 `[` 是内置命令（类似于外部命令 `/usr/bin/test`）。

数组元素。在数组上下文中，`[]` 设置数组的索引。

```
Array[1]=slot_1
echo ${Array[1]}
```

字符范围。在正则表达式中，`[]` 限定了匹配的字符范围。

整数扩展。在 `$[]` 之间计算。

```
a=3
b=7
echo $[a+$b]  # 10
echo $[a*b]  # 21
```

注意这种用法已过时，已被 `(( ))` 结构取代。

整数扩展。在 `(( ))` 之间扩展并计算整数表达式。参见 `(( ))` 结构。

重定向。`scriptname >filename` 将脚本输出重定向到文件。如果文件已存在，则覆盖。

`command &2` 将命令的标准输出重定向到标准错误。

> 这是用于测试条件时抑制输出。例如，让我们测试某个命令是否存在。

```bash
bash type bogus_command &>/dev/null
```

第 3 章 特殊字符

```bash
bash$ echo $?
1
```

或者在脚本中：

```bash
command_test () { type "$1" &>/dev/null; }
#
cmd=rmdir              # 合法命令。
command_test $cmd; echo $?       # 0

cmd=bogus_command                # 非法命令
command_test $cmd; echo $?       # 1
```

