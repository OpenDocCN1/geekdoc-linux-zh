
## 菜单显示逻辑

菜单会在每个条目前添加编号。例如，以下 select 结构：

```bash
select fruit in apple banana blueberry kiwi orange watermelon STOP
```

会显示如下菜单：

```text
1) apple        3) blueberry    5) orange       7) STOP
2) banana       4) kiwi         6) watermelon
```

select 结构使用 LINES（默认值为 80）和 COLUMNS（默认值为 80）变量的值来指定显示大小。如果将 COLUMNS 设置为 20，菜单看起来像这样：

```text
1) apple
2) banana
3) blueberry
4) kiwi
5) orange
6) watermelon
7) STOP
```

**PS3** 在显示菜单后，select 会显示 **PS3** 的值，即 select 的提示符。**PS3** 的默认值是 `#`，但通常会被设置为更有意义的值。当你在 **PS3** 提示符下输入一个有效数字（菜单范围内的数字）时，select 会将 varname 设置为你所输入数字对应的参数。无效输入会导致 shell 将 varname 设置为 null。无论哪种情况，select 都会将你的响应存储在关键字变量 REPLY 中，然后执行 do 和 done 之间的命令。如果你在不输入选择的情况下按下回车键，shell 会重新显示菜单和 **PS3** 提示符。

select 结构会不断发出 **PS3** 提示符并执行命令，直到某件事使其退出——通常是 break 或 exit 语句。break 语句会跳出循环，而 exit 语句会退出脚本。

### 示例脚本：fruit2

以下脚本说明了 select 的使用方法：

```bash
$ cat fruit2
#!/bin/bash
PS3="Choose your favorite fruit from these possibilities: "
select FRUIT in apple banana blueberry kiwi orange watermelon STOP
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

执行此脚本会产生以下交互：

```text
$ ./fruit2
1) apple 2) banana 3) blueberry 4) kiwi 5) orange 6) watermelon 7) STOP
Choose your favorite fruit from these possibilities: 3
You chose blueberry as your favorite.
That is choice number 3.
Choose your favorite fruit from these possibilities: 99
Invalid entry.
Choose your favorite fruit from these possibilities: 7
Thanks for playing!
```

在设置 PS3 提示符并通过 select 语句建立菜单后，fruit2 执行 do 和 done 之间的命令。如果用户提交无效输入，shell 会将 varname（$FRUIT）设置为 null 值。如果 $FRUIT 为 null，echo 会显示错误消息；continue 随后会使 shell 重新显示 PS3 提示符。如果输入有效，脚本会测试用户是否想要停止。如果是，echo 会显示适当的消息，break 会退出 select 结构（以及脚本）。如果用户输入有效响应且不想要停止，脚本会显示用户响应的名称和编号。（关于 echo -e 选项的信息，请参见第 1009 页。）

# Here 文档（ heredoc）

Here 文档允许你在 shell 脚本内部将输入重定向到 shell 脚本。Here 文档之所以这样命名，是因为它“在这里”——即在 shell 脚本中立即可访问——而不是“在那里”，比如在另一个文件中。

### 示例脚本：birthday

以下名为 birthday 的脚本包含一个 Here 文档。第一行中的两个小于符号（`<<`）表示后面跟着一个 Here 文档。分隔 Here 文档的一个或多个字符位于小于符号之后——本例使用加号。虽然打开的分隔符必须紧邻小于符号，但关闭的分隔符必须单独占一行。shell 将两个分隔符之间的所有内容作为标准输入发送给进程。在示例中，这相当于你将标准输入重定向到 grep 的一个文件，除了该文件嵌入在 shell 脚本中：

```bash
$ cat birthday
grep -i "\$1" <<+
Max		June 22
Barbara	February 3
Darlene	May 8
Helen		March 13
Zach		January 23
Nancy		June 26
+

$ ./birthday Zach
Zach		January 23

$ ./birthday june
Max      June 22
Nancy    June 26
```

当你运行 **birthday** 时，它会列出所有包含你调用时传入的参数所在行的 Here 文档行。在这种情况下，第一次运行 **birthday** 时，因为它被传入了参数 **Zach**，所以它会显示 Zach 的生日。第二次运行显示了六月份所有的生日。`-i` 参数使 **grep** 的搜索不区分大小写。

### 可选：bundle 脚本

下一个名为 **bundle** 的脚本包含了对 Here 文档的巧妙使用。**bundle** 脚本是创建 shell 归档（**shar**）文件的脚本的优雅示例。该脚本创建一个文件，该文件本身是一个 shell 脚本，其中包含其他几个文件以及重建原始文件所需的代码：

```bash
$ cat bundle
#!/bin/bash
# bundle: group files into distribution package

echo "# To unbundle, bash this file"
for i
do
    echo "echo $i 1>&2"
    echo "cat >$i <<'End of $i'"
    cat $i
    echo "End of $i"
done
```

正如 shell 不会将 shell 脚本标准输入中出现的特殊字符视为特殊字符一样，shell 也不会将 Here 文档分隔符之间出现的特殊字符视为特殊字符。

如下例所示，**bundle** 的输出是一个 shell 脚本，被重定向到名为 **bothfiles** 的文件。它包含作为 **bundle** 参数传入的每个文件的内容（在本例中为 **file1** 和 **file2**）在一个 Here 文档中。要从 **bothfiles** 中提取原始文件，你只需将其作为 **bash** 命令的参数传入。在每个 Here 文档之前都有一个 **cat** 命令，当运行 **bothfiles** 时，该命令使 Here 文档写入新文件：

```text
$ cat file1
This is a file.
It contains two lines.
$ cat file2
This is another file.
It contains three lines.
```

执行输出如下：

```text
$ ./bundle file1 file2 > bothfiles
$ cat bothfiles
# To unbundle, bash this file
echo file1 1>&2
cat >file1 <<'End of file1'
This is a file.
It contains two lines.
End of file1
echo file2 1>&2
cat >file2 <<'End of file2'
This is another file.
It contains
three lines.
End of file2
```

在下一个示例中，在运行 bothfiles 之前删除了 file1 和 file2。bothfiles 脚本在创建文件时回显它创建的文件的名称。然后 ls 命令表明 bothfiles 已重新创建了 file1 和 file2：

```text
$ rm file1 file2
$ bash bothfiles
file1
file2
$ ls
bothfiles
file1
file2
```

# 文件描述符

如第 334 页所述，在进程从文件或向文件写入之前，它必须打开该文件。当进程打开一个文件时，Linux 会将一个数字（称为文件描述符）与该文件关联。文件描述符是进程打开文件表中的索引。每个进程都有自己的打开文件集合和文件描述符。打开文件后，进程通过引用其文件描述符从该文件读取和写入数据。当不再需要文件时，进程关闭文件，释放文件描述符。

典型的 Linux 进程开始时打开了三个文件：标准输入（文件描述符 0）、标准输出（文件描述符 1）和标准错误（文件描述符 2）。通常，这些是进程需要的唯一文件。请记住，你使用符号 `>` 或符号 `1>` 重定向标准输出，使用符号 `2>` 重定向标准错误。虽然你可以重定向其他文件描述符，但由于 0、1 和 2 以外的文件描述符没有特殊的传统含义，这样做很少有用。例外是你自己编写的程序，在这种情况下，你控制文件描述符的含义并利用重定向。

## 打开文件描述符

Bourne Again Shell 使用 **exec** 内置命令打开文件，语法如下：

```bash
exec n> outfile  
exec m< infile
```

第一行打开 `outfile` 用于输出并保持打开状态，将其与文件描述符 *n* 关联。第二行打开 `infile` 用于输入并保持打开状态，将其与文件描述符 *m* 关联。

## 复制文件描述符

`<&` 标记复制输入文件描述符；`>&` 复制输出文件描述符。你可以通过使文件描述符引用与另一个打开的文件描述符相同的文件来复制文件描述符，例如标准输入或输出。使用以下语法打开或重定向文件描述符 *n* 作为文件描述符 *m* 的副本：

```bash
exec n<&m
```

一旦你打开了一个文件，你可以用两种方式将其用于输入和输出。首先，你可以在任何命令行上使用 I/O 重定向，使用 `>&n` 将标准输出重定向到文件描述符，或使用 `<&n` 从文件描述符重定向标准输入。其次，你可以使用 `read`（第 1041 页）和 `echo` 内置命令。如果你调用其他命令，包括函数（第 396 页），它们会继承这些打开的文件和文件描述符。当你完成使用文件后，可以使用以下语法关闭它：

```bash
exec n<&-
```

## 文件描述符示例

当你用两个参数调用以下 `mycp` 函数时，它会将第一个参数指定的文件复制到第二个参数指定的文件。如果你只提供一个参数，脚本会将参数指定的文件复制到标准输出。如果你不带参数调用 `mycp`，它将标准输入复制到标准输出。

### 注意：函数不是 shell 脚本

`mycp` 示例是一个 shell 函数；如果你将其作为 shell 脚本执行，它不会按预期工作。（它会工作。函数将在一个非常短命的子 shell 中创建，这没什么用。）你可以从键盘输入此函数。如果你将函数放入文件中，你可以将其作为 `. `（点）内置命令（第 332 页）的参数运行。如果你希望它始终可用，也可以将函数放入启动文件中（第 397 页）。

