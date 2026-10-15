
将变量内容的开头与指定的模式进行比较。如果识别出该模式，该结构将返回变量的内容，但会减去匹配搜索模式的最短文本。如果未找到模式，则返回变量的全部内容。在搜索模式中，可以使用相同的通配符来构建文件名（`*` `?` `[abc]`）。在任何情况下，变量都不会被改变：

```
$ dat=home/mk/book/book.tar.gz

$ echo ${dat#*/}

home/mk/book/book.tar.gz
```

## 分支 509

此外，可以从 `if` 结构内部删除第二个 `echo` 命令，因为由于 `exit` 指令，`fi` 之后的所有行只有在条件满足时才会执行。

```
#! /bin/sh

# shell file iftestft, 等变体

#

if [ $# -ne 2 ]; then

    echo "This command must be passed exactly two parameters!"

    exit 1

fi

echo "Parameter: $1, Parameter: $2"
```

我们用一个更实用的示例作为结束：脚本文件 `savequit` 将所有的 `*.tex` 文件保存到压缩包 `backup.tgz` 中。如果在创建压缩文件的没有发生错误（使用运算符 `&&`），则生成的文件将被复制到 A 盘的磁盘上。其判断标准是 `mcopy` 的返回值。如果一切顺利（且 A 盘不包含满额磁盘或根本没有磁盘），计算机随后将通过 `shutdown` 关闭机。

```
#! /bin/sh

# shell file savequit: save *.tex-files, switch off system

tar -czf backup.tgz *.tex && mcopy -n backup.tgz a:

shutdown -t 5 -h -q now
```

如果通过变量 `$?` 检查两个命令的结果，也可以通过在单独行中指定 `tar` 和 `mcopy` 命令来使程序更加清晰。

```
#! /bin/sh

# shell file savequit: save *.tex-files, switch off system

tar -czf backup.tgz *.tex && mcopy -n backup.tgz a:

if [ $? -ne 0 ]; then

    shutdown -t 5 -h -q now

fi
```

## 使用 test 制定条件

在 `bash` 中，无法直接指定条件——例如变量与值之间的比较。首先，`bash` 的整个核心理念基于所有操作都通过一个独特的概念执行的这一事实；其次，`>` 和 `<` 等特殊字符已用于其他用途。因此，你必须使用 `test` 命令来在循环和分支中制定条件。（顺便提一下，`test` 在 `bash` 之外也作为一个单独的 `LINUX` 命令存在。它主要被集成到 `bash` 中是为了获得更高的处理速度。）

## 510 BASH 编程

如果条件满足，`test` 返回值 0（真），如果条件不满足，则返回 1（假）。为了减少输入工作，可以使用方括号中的短表示法。该命令在本章末尾的参考部分有更详细的描述（见第 533 页）。

`test` 应用于三个领域：比较两个数字、比较字符字符串以及测试文件是否存在以及是否具有给定属性。以下示例显示了一些可能的应用：

`test "$x"`
检查 `x` 是否被占用（即当字符串包含 0 个字符时，结果为假，否则为真）。

`test x -gt 5`
检查 `x` 是否包含大于 5 的数值。如果 `x` 不包含数字，则会显示错误消息。除了 `-gt`（大于）之外还可以还可以以下比较运算符：`-eq`（等于）、`-ne`（不等于）、`-lt`（小于）、`-le`（小于等于）和 `-ge`（大于等于）。

`test -f $x`
检查名为 `x` 指定的文件是否存在。

当在 shell 中交互式执行 `test` 时，必须在 `test` 命令之后用 `echo` 读取上一个命令的变量 `$?` 返回值：

```
$ a=20

$ test a -eq 20; echo $?

0

$ test a -gt 20; echo $?
```

## case 分支

`case` 结构以关键字 `case` 开始，随后是待分析的参数（通常是一个变量）。在关键字 `in` 之后，可以指定多个字符字符串模式，并与参数进行比较。文件名也允许相同的通配符。模式用圆括号 `)` 结束，例如 `(*)` 用于识别以两个负号开头的字符字符串。多个模式可以用 `|` 彼此隔开——在这种情况下，会检查所有模式（例如 `*.h`），以便同一个分支中识别 `*.c` 和 `*.h` 文件。

括号后的命令必须以双分号 `;` 结束。如果需要 `else` 分支，最后一个指定的模式必须是 `*` —— 所有字符字符串都匹配此模式。在处理 `case` 结构时，只取参数匹配的第一个分支。

以下 `case` 示例展示了使用 `case` 将传递的参数分类文件名和选项。在循环内部，如果参数以 `-` 开头，则将其追加到变量 `opt` 的末尾，否则追加到 `dat` 的末尾。

```bash
#! /bin/sh

# shell file savequit: save *.tex-files, switch off system

opt=

dat=

for i do

    # 循环所有传递的参数

    case "$i" in

        *) opt=$opt $i ;;

        *) dat=$dat $i ;;

    esac

done

# 循环结束

echo "Options: $opt"

echo "Files: $dat"
```

`case` 的示例运行提供了分类的功能。按任意顺序传递的参数被分类为选项和文件名：
- `Options`: `-x -y`
- `Files`: `dat1`

遵循相同的方案，`case` 分支（通过在搜索中指定 `*.`）。如果你想深入参与 `case` 分析，你应该查看脚本文件 `/usr/bin/nroff`。该文件处理以 `nroff` 语法传递的参数的方式，使得相关的 `groff` 命令可以处理它们。

## 14.4 循环

`bash` 有三种循环方式：`for` 执行循环、`while` 在条件满足时执行循环、`until` 在条件不满足时执行循环。

### for 循环

在第一个示例中，变量 `i` 被赋值为 `a`。`for` 循环遍历列表中的所有元素。

```bash
for i in a b c; do

    echo $i

done
```

在第二个示例中，`for` 循环用于处理文件。

```bash
for i in *.txt; do

    ls $i

done
```

### while 循环

在第一个示例中，`while` 循环在条件为真时执行。

```bash
while [ $i -lt 5 ]; do

    echo $i

    ((i++))

done
```

在第二个示例中，`while` 循环用于读取文件内容。

```bash
while [ $i -ne 5 ]; do

    echo $i

    ((i++))

done
```

### until 循环

在第一个示例中，`until` 循环直到条件为真时停止。

```bash
until [ $i -ge 5 ]; do

    echo $i

    ((i++))

done
```

在第二个示例中，`until` 循环用于读取文件内容。

## break 和 continue

`break` 用于跳出当前的循环。

```bash
for i in {1..10}; do

    if [ $i -eq 5 ]; then

        break

    fi

    echo $i

done
```

`continue` 用于跳过当前循环的剩余。

```bash
for i in {1..10}; do

    if [ $i -eq 5 ]; then

        continue

    fi

    echo $i

done
```

## 514 BASH 编程

```bash
# /bin/sh

# dos2linux: eliminates CR characters

if [ $ -eq 0 ]; then # use as filter

  tr -d 'r'

elif [ $ -eq 1 ]; then # process one file

  mv $1 $1.tmp

  tr -d 'r' < $1.tmp

  rm $1.tmp

elif [ $ -eq 2 ]; then # process two files

  tr -d 'r' < $1 $2

else

    cat << EOF
```
