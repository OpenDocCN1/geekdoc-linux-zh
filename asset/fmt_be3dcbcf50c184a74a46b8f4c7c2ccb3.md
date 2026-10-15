
```bash
$cat fruit2
#!/bin/bash
PS3="Choose your favorite fruit from these possibilities: "
select FRUIT in apple blueberry kiwi orange watermelon STOP
do
    if [ "$FRUIT" == "" ]; then
        echo -e "Invalid entry.\n"
        continue
    elif [ $FRUIT = STOP ]; then
        echo "Thanks for playing!"
        break
    fi
    echo "You chose $FRUIT as your favorite."
    echo -e "That is choice number $REPLY.\n"
done
```

- `1) apple` `3) blueberry` `5) orange` `7) STOP`

- `2) banana` `4) kiwi` `6) watermelon`

Choose your favorite fruit from these possibilities: `3`

You chose blueberry as your favorite.

That is choice number `3`.

Choose your favorite fruit from these possibilities: `99`

Invalid entry.

Choose your favorite fruit from these possibilities: `7`

Thanks for playing!

在设置 `PS3` 提示符并使用 `select` 语句建立菜单后，`fruit2` 会执行 `do` 和 `done` 之间的命令。如果用户输入无效内容，shell 将 `FRUIT` 设置为空值，shell 会显示错误并重新显示循环和 `PS3` 提示符。如果输入有效，shell 会显示名称和编号（参见第 63 页关于 `-e` 选项的信息）。

# Here Document（在此文档）

在此文档（Here document）允许你将输入重定向到 shell 脚本。这种文档之所以这样命名，是因为它“在这里”（在脚本中可以直接访问），而不是在“那里”（可能在另一个文件中）。

以下名为 `birthday` 的脚本包含一个在此文档。第一行的双小于符号 `<<` 缩进了一个在此文档。起始分隔符必须与符号相邻，结束分隔符必须独占一行。shell 将分隔符之间的所有内容作为标准输入发送给进程。如下例：

```bash
$cat birthday
grep -i "$1" <<+
Alex June 22
Barbara February 3
Darlene May 8
Helen March 13
Jenny January 23
Nancy June 26
+
```

当你运行 `birthday` 时，它会列出包含你调用参数的所有文档行。在这种情况下，第一次运行 `birthday` 会显示 `Jenny` 的生日，因为它带有参数 `Jenny` 调用的。第二次运行显示 6 月的所有生日。`-i` 参数导致 `grep` 的搜索不区分大小写。

# optional（可选）

下一个名为 `bundle` 的脚本包含了在此文档的巧妙用法。`bundle` 脚本是创建 归档（`shar`）文件的优雅示例。该脚本创建一个包含其他文件以及重建原始文件代码的脚本文件：

```bash
$cat bundle
#!/bin/bash

# bundle: group files into distribution package

echo "# To unbundle, bash this file"
for i
do
    echo "echo $i" 1>&2
    echo "cat >$i <<'End of $i'"
    cat $i
    echo "End of $i"
done
```

就像 shell 不将脚本标准输入中的特殊字符视为特殊一样，shell 在此文档分隔符之间的特殊字符视为特殊。

如下例，`bundle` 的输出是一个 shell 脚本，被重定向到名为 `bothfiles` 的文件。它在此文档内部包含了作为 `bundle` 参数的文件（在这种情况下为 `file1`, `file2`）的内容。要从 `bothfiles` 提取原始文件，你只需将其作为 `bash` 命令的参数运行即可。

```bash
$cat file1
This is a file.
It contains two lines.
```

```bash
$cat file2
This is another file.
It contains
three lines.
```

```bash
$bundle file1 file2 > bothfiles
$cat bothfiles
# To unbundle, bash this file
echo file1&2
cat >file1<<End of file1'
This is a file.
It contains two lines.
End of file1
echo file2&2
cat >file2 <<End of file2'
This is another file.
It contains
three lines.
End of file2
```

在下一个示例中，在运行 `bothfiles` 之前，`file1` 和 `file2` 被删除了。`bothfiles` 脚本在创建文件时会回显它所创建的文件名。随后 `ls` 命令显示 `bothfiles` 重新创建了 `file1` 和 `file2`：

```bash
$rm file1 file2
$bash bothfiles
file1
file2
$ls
bothfiles
file1
file2
```

[2] 感谢 Brian W. Kernighan 和 Rob Pike, 《The Unix Programming Environment》(Englewood Cliffs, N.J.: Prentice-Hall, 1984), 98. 经许可重印。

## 文件描述符

如第 260 页所述，在进程从文件读取或写入文件之前，它必须打开该文件。当进程打开一个文件时，Linux 将一个数字关联到文件（称为文件描述符）。每个进程都有自己的一组打开的文件和其文件描述符。打开文件后，进程通过引用其文件描述符进行读取和写入。当它不再需要该文件时，进程会关闭文件并释放描述符。

一个典型的 Linux 进程启动时带有三个打开的文件：标准输入（文件描述符 0）、标准输出（文件描述符 1）。这些是进程需要的唯一文件。记住，你使用符号 `>` 或符号 `1` 重定向标准输出，使用符号 `2->` 重定向标准错误。虽然你可以重定向其他文件描述符，但除 0、1 和 2 以外的文件描述符没有任何特殊的常规含义，这样做通常很少用。

例外情况是你自己编写的程序，在这种情况下，你控制文件描述符的含义，并可以利用重定向。

## 打开文件描述符

Bourne Again 使用 `exec` 内置命令如下所示打开文件：

```bash
exec>outfile
exec<infile
```

第一行打开 `outfile` 用于输出并保持打开状态，将其与文件描述符 n 关联。第二行打开 `infile` 用于输入并保持打开状态，将其与文件描述符 m 关联。

## 复制文件描述符

`<&` 令牌复制输入文件描述符；使用 `>&` 复制输出文件描述符。你可以通过让文件描述符指向另一个打开的描述符相同的文件（例如标准输入或输出）来复制文件描述符。使用以下格式将文件描述符 n 打开或重定向为文件描述符 m 的副本：

```bash
execn<&
```

一旦你打开了文件，你可以通过两种不同的方式对其进行输入和输出。首先，你在任何命令行上使用 I/O 重定向，通过 `>&n` 将标准输出重定向到文件描述符，通过 `<&n` 从文件描述符重定向标准输入。其次，你可以使用 `read`（第 487 页）和 `echo` 内置命令。当你调用其他命令（包括函数，第 315 页）时，它们会继承这些打开的文件和描述符。当你完成对文件的使用后，可以使用以下命令关闭它：

```bash
exec<&-
```

当你调用下一个示例中名为 `mycp` 的 shell 函数并带有两个参数时，它会将第一个参数命名的文件复制到第二个参数命名的文件。如果你只提供一个参数，脚本将该参数命名的文件复制到标准输出。如果你在不带任何参数的情况下调用 `mycp`，它会将标准输入复制到标准输出。

## 提示：函数不是 shell 脚本

`mycp` 示例是一个 shell 函数；如果你将其作为 shell 脚本执行，它将不会如你预期那样工作（它可以运行：该函数将在非常短的子进程中创建，这可能没什么用）。你可以从键盘输入此函数。如果你将该函数放在文件中，可以将其作为 `.`（点）内置命令（第 259 页）的参数来运行。如果你想让它始终可用，可以将其放在启动文件中（第 317 页）。

```bash
function mycp ()
{
case $# in
0)
  # 零参数
  # 文件描述符 3 复制标准输入
  # 文件描述符 4 复制标准输出
  exec 3<&0 4<&1
  ;
1)
  # 一个参数
  # 打开参数命名的文件用于输入
  # 并将其与文件描述符 3 关联
  # 文件描述符 4 复制标准输出
  exec 3<$1
;;
2)
# 两个参数
  # 打开第一个参数命名的文件用于输入
  # 并将其与文件描述符 3 关联
  # 打开第二个参数命名的文件用于输出
  # 并将其与文件描述符 4 关联
  exec 3<$1 4>$2
;;
*)
echo "Usage: mycp [source [dest]]"
return 1
;;
esac
}

# 调用 cat，输入来自文件描述符 3
# 输出到文件描述符 4
cat <&3 >&4

# 关闭描述符 3 和 4
exec 3<- 4<-
```

当你调用下一个示例中名为 `mycp` 的 shell 函数并带有两个参数时，它会将第一个参数命名的文件复制到第二个参数命名的文件。如果你只提供一个参数，脚本将该参数命名的文件复制到标准输出。如果你在不带任何参数的情况下调用 `mycp`，它会将标准输入复制到标准输出。

## 参数与变量

Shell 参数和变量在第 277 页。本节对之前的内容进行了扩展，增加了对数组变量、全局与局部变量、特殊参数以及未设置变量的讨论。

### 数组变量

Bourne Again Shell 支持一维数组变量。下标是零索引的整数（即数组第一个元素的下标为 0）。使用以下格式声明并赋值数组：

```bash
name=(element1 element2 ...)
```

以下示例为数组 `NAMES` 分配了四个值：

```bash
$NAMES=(max helen sam zach)
```

如下所示引用数组的单个元素：

```bash
$echo ${NAMES[2]}
sam
```

下标 `[*]` 和 `[@]` 都提取整个数组，但在双引号内使用时表现不同。`@` 产生原始数组的副本数组；`*` 产生一个数组元素（或普通变量），包含由 `IFS` 中的第一个字符（通常是空格）分隔的数组所有元素。在以下示例中，使用 `*` 将 `NAMES` 变量的元素填充到数组 `A` 中，使用 `@` 填充到 `B` 中。带有 `-a` 选项的 `declare` 内置命令显示数组的值（并提醒你 `bash` 对数组使用零索引）：

```bash
$A=("${NAMES[*]}")
$B=("${NAMES[@]}")
```

```bash
$declare -a
declare -a A='([0]="max helen sam zach')
declare -a B='([0]="max" [1]="helen" [2]="sam" [3]="zach")
...
declare -a NAMES='([0]="max" [1]="helen" [2]="sam" [3]="zach")
```

从 `declare` 的输出中你可以看到 `NAMES` 和 `B` 拥有多个元素。相比之下，在双引号内*赋值*了赋值的 `A` 只有一个元素：A 的所有元素都包含在引号之间。

在下一个示例中，`echo` 尝试显示数组 `A` 的第 1 个元素。没有显示任何内容，因为 A 只有一个元素，且该元素的索引为 0。数组 A 的第 0 个元素持有全部四个名字。B 的第 1 个元素持有数组中的第二项，第 0 个元素持有第一项。

```bash
$echo ${A[1]}
```

```bash
$echo ${A[0]}
max helen sam zach
$echo ${B[1]}
helen
$echo ${B[0]}
```

你可以将 `${#name*}` 操作符应用于数组变量，它返回数组中的元素数量：

```bash
$echo ${#NAMES[*]}
4
```

当给该操作符以数组元素的索引而不是 `*` 时，同一种操作符会返回该元素的长度：

```bash
$echo ${#NAMES[1]}
5
```

你可以在赋值语句的左侧使用下标来替换数组中的指定元素：

```bash
$NAMES[1]=alex
$echo \${NAMES[*]}
max alex sam zach
```

# 变量的局部性

默认情况下，变量对于声明它们的进程是局部的。因此，除非你显式地让变量可用（全局），否则 shell 脚本无法访问在登录 shell 中声明的变量。在 `bash` 中，`export` 使一个变量对子进程可用。在 `tcsh` 中，`setenv`（第 356 页）为变量赋值并使其对子进程可用。本节中的示例使用了 `bash` 语法，该理论同样适用于这两种 shell。

一旦你使用 `export` 内置命令并将变量名作为参数，shell 会将变量的值放在子进程的调用环境中。这种按值传递为每个进程提供了一个变量的副本供其使用。

以下 `textext1` 脚本为变量 `cheese` 赋值并显示其文件名 (`textext1`) 和 cheese 的值。`textext1` 脚本调用 `subtest`，后者尝试显示相同的信息。当下一个 `subtest` 声明 `cheese` 变量并显示其值时。当 `subtest` 返回控制权给执行 `textext1` 的父进程时。此时，`textext1` 再次显示原始 `cheese` 变量的值。

```bash
$cat textext1
cheese=american
echo "textext1 1: $cheese"
subtest
echo "textext1 2: $cheese"
$cat subtest
echo "subtest 1: $cheese"
cheese=swiss
echo "subtest 2: $cheese"
$textext1
textext1 1: american
subtest 1:
subtest 2: swiss
textext1 2: american
```

`subtest` 脚本从未接收到来自 `textext1` 的 `cheese` 的值，且 `textext1` 永远不会丢失该值。与现实世界不同，进程永远不会影响父进程的属性。当进程尝试显示未声明变量的值时（如 `subtest` 所示），进程不会显示任何内容；未声明变量的值为空字符串。

以下 `extest2` 脚本与 `extest1` 相同，但它使用 `export` 使 `cheese` 对 `subtest` 可用：

```bash
$cat extest2
export cheese=american
echo "extest2 1: $cheese"
subtest
echo "extest2 2: $cheese"
subtest
subtest 1: american
subtest 2: swiss
extest2 2: american
```

子进程继承了 `cheese` 的值 `american`，并在显示该值后将其更改为 `swiss`。当控制权返回时，父进程的 `cheese` 副本保持其原始值：`american`。

`export` 内置命令可以包含赋值：

```bash
export cheese=american
```

上述语句等同于以下两条语句：

```bash
cheese=american
export cheese
```

虽然很少这样做，但你可以在赋值之前导出变量。在更改其值后，不需要再次导出已导出的变量。例如，在 `~/.bash_profile` 中为 `PATH` 赋值时不需要，因为它在 `/etc/profile` 中通常被导出。

# 函数

由于函数运行在调用它们的 shell 相同的环境中，变量在 shell 调用的函数之间是隐式共享的。

```bash
$function nam () {
>echo $mname
>mname=zach
>
```

```bash
$mname=sam
$nam
sam
$echo $mname
zach
```

在前面的示例中，`myname` 在交互 shell 中设置为 `sam`。然后调用 `nam` 函数。它显示它拥有的 `mname` 值（`sam`）并将 `mname` 设置为 `zach`。

# 函数变量

局部变量对函数非常有用，可以防止它们影响 shell 环境中的其他变量。在 `bash` 中声明局部变量，请使用 `local` 关键字：

```bash
$function count () {
>local count=$1
>while [ $count -gt 0 ]; do
>echo $count
((count=count-1))
>done
}
$count 3
3
2
1
1
```

`local` 关键字确保该变量仅在函数内部可用。当函数返回时，局部变量会被销毁。

# 全局变量

全局变量可以在 shell 环境中的任何地方访问。默认情况下，除非在函数内部声明为局部，否则 `bash` 中的所有变量都是全局的。
