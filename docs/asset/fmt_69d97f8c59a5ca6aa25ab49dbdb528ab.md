
# 高级 Bash 脚本指南

## 第 4 章 特殊字符

```bash
$ touch .hidden-file
$ ls -al
total 10
--rw-r-- 1 user 0 18 22 .addressfile
--rw-r-- 1 group 0 25 13 .addressbook
--rw-r-- 1 group 0 17 00 .addressbook.bak
--rw-r-- 1 user 0 29 54 .hidden-file
drwxr-xr-x 3 group 4096 18 22 ..
drwx------ 2 group 0 25 13 .
--rw-r-- 1 group 0 17 00 .addressbook.bak
drwxr-xr-x 3 user 4096 18 22 .addressfile
--rw-r-- 1 user 0 29 54 .hidden-file
```

部分引用。`"` 保留了字符串中的大部分特殊字符。见第 6 章。

全引用。`'` 保留了字符串中的所有特殊字符。这是使用第 6 章的一种强引用形式。

逗号运算符。逗号运算符连接一系列算术操作。所有操作都会求值，但只有最后一个会被赋值。

```bash
let a = 9, b = 10
```

转义。`\` 转义字符 `X`。这具有引用 `X` 的效果。`\'` 用于字面量引用。

### 文件名分隔符

`/` 分隔文件名的组成部分（如 `/home/projects/`）。这也是除法运算符。

### 命令替换

`` `command` `` 使 `command` 的输出可用于设置变量。也被称为反引号。

### 空命令

`:` 在 shell 中相当于 `NOP`（无操作）。`:` 命令是 `Bash` 内置命令，它的退出状态为 `0`。

```bash
echo $? # 0
```

无限循环：

```bash
while true
do
  operation-1
  operation-2
  ...
  operation-n
done
```

`if/then` 测试中的占位符：

```bash
if condition
then
    : # 什么都不做
else
  take-some-action
fi
```

在期望二进制的地方占位符，见示例 8–2 和默认参数。

```bash
$ $(username=whoami) 没有前导符会报错
# 除非 "username" 是命令或内置命令...
```

在此文档（here document）中期望命令的地方提供占位符。见示例 1–8。

使用参数替换求值变量字符串（如示例 9–12）。

```bash
${HOSTNAME} ${USER} ${MAIL}
# 如果一个或多个基本环境变量未设置，则打印错误信息。
```

变量扩展。结合 `>` 运算符使用，可以将文件截断为零长度而不改变其属性。如果文件之前不存在，则创建它。

```bash
> data.xxx # 文件 "data.xxx" 现在为空。
# 效果等同于 cat /dev/null >data.xxx
```

结合 `>>` 运算符使用，更新文件的访问/修改时间。这等同于 `touch`。

![](img/1ce1edffaa36e4f698a85430e71c6d3b_17_0.png)

这适用于普通文件、管道、符号链接和特殊文件。

可以用来开始注释行，但不建议这样做。使用 `#` 作为注释会关闭对该行剩余部分的检查，因此任何内容都可以位于注释中。然而，`:` 并非如此：

```bash
> : 这是一个会产生错误的注释（如果 $ x -eq 3 ）。
```

`:` 作为字段分隔符存在于 `/etc/passwd` 中以及 `PATH` 变量中。

```bash
echo $PATH
/usr/local/bin:/usr/bin:/usr/X11R/bin:/bin:/usr/sbin:/sbin:/usr/games
```

反转（或否定）测试或退出状态的意义。`!` 运算符反转其应用的命令的退出状态（示例 3–2），意味着一个测试运算符。这可以将“等于” (`=`) 的意义变为“不等于” (`!`)。`!` 也是 `Bash` 的一个关键字。

在另一个上下文中，`!` 也出现在间接变量引用中。

![](img/1ce1edffaa36e4f698a85430e71c6d3b_17_1.png)

### 通配符

`*` 字符在文件名扩展（globbing）中用作“通配符”，在正则表达式中表示任意数量（或零）字符。

双星号 `**` 是幂运算符。

`?` 字符在通配符（globbing）中作为单字符“文件名通配符”，在扩展正则表达式中也表示一个字符。

在双括号内，`?` 作为 C 风格的三元运算符使用。示例 9–25。

### 变量替换

`$` 是变量替换前缀。

```bash
var1=5
var2=23skidoo
echo $var1    # 5
echo $var2    # 23skidoo
```

在正则表达式中，`$` 匹配行尾。

### 参数替换

`${*}` 和 `${@}`

### 位置参数

`()`, `()`, `[ ]`, `[[ ... ]]`, `(( ... ))`, `>`, `>>`, `<`

### 命令组

```bash
(a=hello; echo $a)
```

![](img/1ce1edffaa36e4f698a85430e71c6d3b_18_0.png)

圆括号内的命令列表会启动一个子 shell（subshell）。

子 shell 内括号内的变量对脚本的其他部分不可见。父进程（脚本）无法读取在子进程（子 shell）中创建的变量。

```bash
a=123
( a=321; "$a")
echo "$a"    # a = 123
      # "$a"   在括号内的作用类似于局部变量。
```

### 数组初始化

```bash
Array={element1 element2 element3}
{xxx,yyy,zzz,...}
```

### 大括号扩展

```bash
grep Linux file.*{txt,htm}
# 在 fileA.txt, "file2.txt", "fileR.html", "file-87.htm" 等文件中
# 单词 "Linux" 的所有实例
```

命令可以接受大括号之间用逗号分隔的文件规格列表。文件名扩展（通配符）适用于大括号之间的文件空间。

![](img/1ce1edffaa36e4f698a85430e71c6d3b_19_0.png)

大括号内不允许有空格，除非空格被引用或转义。

```bash
echo {file1,file2}\: \A, "B", 'C'
file1 : A file1 : B file : C file2
: A file2 : B file2 : C
```

### 代码块

也称为“内联组”（inline group），这种结构实际上创建了一个匿名函数。与函数不同，代码块中的变量将持续到脚本的剩余部分。

```bash
bash { local a; a=123; }
bash: local: can only be used in a function
```

```bash
a=123
{ a=321; }
echo "a = $a"    # a = 321    (代码块内部的值)

# 感谢 S.C.
```

大括号包裹的代码块可以对其进行 I/O 重定向。

#### 示例 4–1. 代码块和 I/O 重定向

```bash
#!/bin/bash
# 读取 /etc/fstab 中的行

File=/etc/fstab
{
read line1
read line2
} <$File
echo "First line in $File is:"
echo "$line1"
echo
echo "Second line in $File is:"
echo "$line2"

exit 0
```

与上述圆括号内的命令组不同，由花括号 `{}` 包围的代码块**不**通常会启动一个子 shell。

### 路径（pathname）

最常用于 `find` 结构。这不是一个 shell 内置命令。

`\\` 结束 `-exec` 命令序列。它需要转义以防止被 shell 解释。

```bash
{\\:
```

`test` 命令。`[ ]` 之间的表达式。它是 shell 内置命令 `test` 的同义词，而不是外部命令 `/usr/bin/test`。

```bash
[]
```

`test` 命令。`[[ ... ]]` 之间的表达式。参见 `[[ ... ]]` 结构。

```bash
[]
```

整数扩展。`(( ... ))` 之间的表达式。参见 `(( ... ))` 结构。

```bash
()
```

重定向。

`>`, `>>`, `<`

`scriptname > filename` 将 `scriptname` 的输出重定向到 `filename`。如果文件已存在则会覆盖。

`scriptname >> filename` 将 `scriptname` 的输出追加到 `filename`。如果文件不存在，则会创建。

```bash
command >
```

进程替换。`<(command)`

```bash
<(command)>
```

在不同的上下文中，`<` 和 `>` 字符作为字符串比较运算符。在另一个上下文中，`<` 和 `>` 字符作为整数比较运算符。

在此文档（here document）中使用重定向 `<<`。

### 管道

将上一个命令的输出传递给下一个命令，或 shell。这是一种链接命令的方法。

```bash
echo ls -1 | sh
# 将 "echo ls -1" 的输出传递给 shell
# 结果与简单的 "ls -1" 相同。
```

```bash
cat *.lst | sort
# 合并并排序所有 ".lst" 文件，然后删除重复行。
```

管道作为进程通信的经典方法将一个进程的 `stdout` 发送到另一个进程的 `stdin`。在通常情况下，如 `cat` 或 `echo` 等命令会将数据流管道到过滤器。

```bash
cat $filename | grep $search_word
```

命令或命令的输出可以管道到脚本。

```bash
#!/bin/bash

# uppercase.sh : 将输入转换为大写

tr 'a-z' 'A-Z' # 范围必须加引号以防止生成单个字符的文件。
```

现在，将 `ls -1` 的输出管道到 `uppercase.sh`。

```bash
bash ls -1 | /uppercase.sh
```

```bash
variable="initial_value"

echo "new_value" | read variable

echo "$variable" = initial_value
```

管道中每个进程的 `stdout` 必须作为下一个进程的 `stdin` 读取。如果不是这种情况，数据流将被阻塞，管道将无法按预期工作。

```bash
file2

# "cat file2" 的输出出现
```

管道运行子进程，因此无法更改变量。

### 强制重定向（即使设置了 `noclobber` 选项）

这将覆盖现有文件。在后台运行作业。命令后跟 `&` 将后台运行。在脚本内部，命令和循环可以在后台运行。

```bash
sleep 10 &
```

#### 示例 4–3. 在后台运行循环

```bash
#!/bin/bash

# background-loop.sh

for i in 2 3 4 5 6 7 8 9 10
do
    echo -n "$i"
done & # 在后台运行。有时会在第二个循环后执行。

echo

# 这个 'echo' 有时不会显示。
```

### 按键

坦率说，这有解决办法。从 `stdin` 到 `stdout` 的重定向。

```bash
cd /source/directory && tar cf - | (cd /dest/directory && tar xpvf -)

# 将整个文件树从一个目录移动到另一个 [感谢 Alan Cox <a.cox@swansea.ac.uk>]，这是一个重大变化
```

要移动的文件所在的源目录。“列表：如果 `cd` 操作成功，则执行。`c` 选项 `tar` 归档命令创建一个归包，`f` 文件选项后的 `-` 指定目标及其当前目录树 (`.`)。

1. `cd /source/directory`
2. `&&`
3. `tar cf -`
4. `|`
5. `(...)`
6. `cd /dest/directory`
7. `&&`
8. `tar xpvf -`

切换到目标目录。“列表”：同上。解压缩 (`x`)，保留所有权和文件权限 (`p` 并向 `stdout` 发送详细信息 (`v`)），从 `stdin` 读取数据 (`f` 后跟 `-`)。

管道到。注意 `x` 是一个命令，而 `p`、`v`、`f` 是选项。

一个子 shell

呼！

更优雅，但等同于：

```bash
cd source-directory
tar cf - | (cd ../target-directory; tar xf -)
cp -a /source/directory /dest 也有效果。
```

```bash
bunzip2-linux-2.4.3.tar.bz | tar xvf-

--压缩文件-- | --将其传递给 "tar"---

如果 `tar` 没有修补以处理 `bunzip2`，则需要使用管道分两个离散步骤完成。练习的目的是解压缩“压缩过的”内核源码。

注意在这种情况下，`-` 本身不是 Bash 运算符，而是 Unix 写入 stdout 时识别的选项，如 `tar`、`cal`、`cat`。
```

```bash
bash echo "whatever" | cat
whatever
```

这一次，它接受来自标准输入的输入并进行过滤。

`-` 可以将标准输出管道到其他命令。这允许进行一些技巧操作，例如在文件开头添加行。

使用 `diff` 比较文件与另一个文件的部分：

```bash
grep bash file1 | diff file2 -
```

最后，是一个使用 `tar` 的真实示例。

#### 示例 4–4. 备份昨天更改的所有文件

```bash
#!/bin/bash

# 将当前目录下在过去 24 小时内修改过的文件
# 备份到“tar 包”（tar 压缩并 gzip 文件）。

NOARGS=0
E_BADARGS=65

if [ $# == $NOARGS ]
then
  echo "Usage: basename $0 filename"
  exit $E_BADARGS
fi

find . -mtime -1 -type f -print > $1.tar
gzip $1.tar

# Stephanie Chalaz 指出，如果找到的文件过多
# 上述代码将会失败
# 如果任何文件名包含空白字符。

# 他建议了以下替代方案：
# find -mtime -1 -type f -print | xargs -0 tar rvf "$1.tar"
# 使用 GNU 版本的 "find"
# find -mtime -1 -type f -exec tar rvf "$1.tar" '{}' \; 
# 可移植到其他 UNIX 变体，但慢得多。

exit 0
```

以 `--` 开头的文件名与重定向运算符配合时会导致问题。脚本应该检查此并将此类文件名作为变量或 `$PWD` 传递。如果变量的值以 `--` 开头，可能也会创建类似的问题。

### 上一个工作目录

`cd` 切换到上一个目录。这使用了 `$PWD`。不要与 `-` 重定向混淆。`-` 取决于它出现的上下文。

重定向方向：

- `>` 将标准输出重定向到文件。
- `<` 将标准输入从文件重定向。
- `>>` 将标准输出追加到文件。
- `2>` 将标准错误重定向到文件。
- `2>&1` 将标准错误重定向到标准输出。
- `> /dev/null` 将标准输出重定向到空设备。
- `&> /dev/null` 将标准输出和标准错误都重定向。

### 减号（Minus）

算术运算中的减号。

### 等号（Equals）

赋值运算符

```bash
a=28
echo $a
```

在不同的上下文中，`=` 是字符串比较。

### 加号（Plus）

加法运算。

在不同的上下文中，`+` 是正则表达式运算符。

### 取模（Modulo）

除法的余数算术运算。

在不同的上下文中，`%` 是模式匹配运算符。

### 主目录（Home）

`~` 这对应于内部变量 `$HOME`。`~` 是用户的主目录，`ls` 列出内容。`~/` 是当前目录，`ls` 列出内容。

```bash
echo $HOME
echo ~
```

### 控制字符

- `Ctrl+C` 终止前台作业。
- `Ctrl+D` 退出 shell（类似于 `exit`）。它发送 `EOF`（文件结束符）。
- `Ctrl+J` 回车。
- `Ctrl+L` 清除终端屏幕。
- `Ctrl+M` 换行。
- `Ctrl+U` 擦除输入行。
- `Ctrl+Z` 暂停前台作业。
- `Ctrl+A` 行首。
- `Ctrl+G` 蜂鸣。
- `Ctrl+H` 退格。

```bash
#!/bin/bash
# 在字符串中嵌入 Ctrl+H。
a="*H" # 两个 Ctrl+H（退格）。
echo -n "abcdef" # 末尾有两个空格。
echo -n "abcdef$a" # abcdef
# 末尾没有空格时不退格（为什么？）。
echo; echo # 结果可能不符合预期。
```

### 空白字符（Whitespace）
