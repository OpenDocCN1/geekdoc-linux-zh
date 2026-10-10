
```bash
$ /home/max/bin/safedit memo
$ ./safedit memo
$ safedit memo
```

在设置 `script` 变量后，它会在用法和错误消息中替换脚本的文件名。通过使用从调用脚本的命令中派生的变量，而不是硬编码在脚本中的文件名，你可以创建指向该脚本的链接或重命名该脚本，用法和错误消息仍将提供准确的信息。

`**safedit**` 的另一个功能与在临时文件名称中使用 `$$` 参数有关。`esac` 语句后面的语句创建并分配给 `tempfile` 变量。该变量存储在 `/tmp` 目录中的临时文件的名称，许多临时文件都存储在此处。临时文件名以 shell 的 `PID` 号开头，并以脚本名称结尾。使用 `PID` 号确保文件名是唯一的。因此，`safedit` 不会尝试覆盖现有文件，这种情况可能在两个人同时使用 `safedit` 时发生。附加脚本名称是为了在文件因某种原因遗留在 `/tmp` 时，你可以弄清楚它的来源。

`PID` 号位于文件名中 `$script` 之前而非之后，这是因为某些旧版本的 UNIX 对文件名施加了 14 个字符的限制。Linux 系统没有这种限制。由于 `PID` 号确保了文件名的唯一性，因此将其放在前面，使其不会被截断。（如果 `$script` 部分被截断，文件名仍然是唯一的。）出于同样的原因，当在脚本稍后的 `if` 控制结构中创建备份文件时，文件名由字符串 `bak` 开头，后跟正在编辑的文件名。在旧系统上，如果使用 `bak` 作为后缀而非前缀，且原始文件名为 14 个字符，则 `bak` 可能会丢失，从而导致原始文件被覆盖。`basename` 实用程序在添加 `bak` 前缀之前提取 `$editfile` 的简单文件名。

`safedit` 脚本在 `if` 结构中使用了一个不寻常的测试命令：`vim.tiny $editfile`。该测试命令调用 `vim` 来编辑 `$editfile`。当你完成文件编辑并退出 `vim` 时，`vim` 返回一个退出代码。`if` 控制结构使用该退出代码来确定采用哪个分支。如果编辑会话成功完成，`vim` 返回 0，并执行 `then` 语句后面的语句。如果 `vim` 没有正常终止（例如用户终止了 `vim` 进程），`vim` 返回非零退出状态，脚本执行 `else` 后面的语句。

- 命名临时文件

## select

`select` 控制结构基于 Korn Shell 中发现的结构。它显示一个菜单，根据用户对项目的选择将值分配给变量，并执行一系列命令。`select` 控制结构具有以下语法：

```bash
select varname [in arg...]   
do   
commands   
done
```

`select` 结构显示一个包含 `arg` 项目的菜单。如果省略关键字 `in` 和参数列表，`select` 使用位置参数代替 `arg` 各项。该菜单在每一项前使用数字进行格式化。例如，以下 `select` 结构：

```bash
select fruit in apple banana blueberry kiwi orange watermelon STOP
```

将显示如下菜单：

- 1) apple 3) blueberry 5) orange 7) STOP
- 2) banana 4) kiwi 6) watermelon

`select` 结构使用 `LINES` 和 `COLUMNS` 变量的值来指定显示的大小。（`LINES` 的默认值为 24；`COLUMNS` 的默认值为 80。）当 `COLUMNS` 设置为 20 时，菜单看起来像这样：

- 1) apple
- 2) banana
- 3) blueberry
- 4) kiwi
- 5) orange
- 6) watermelon
- 7) STOP

在显示菜单后，`select` 会显示 `PS3` 的值，即 `select` 提示符。`PS3` 的默认值是 `?#`，但通常会被设置为更有意义的值。当你在响应 `PS3` 提示符时输入一个有效数字（在菜单范围内的数字）时，`select` 会将 `varname` 设置为你输入的数字对应的参数。无效输入会导致 shell 将 `varname` 设置为空值。无论哪种情况，`select` 都会将你的响应存储在关键字变量 `REPLY` 中，然后执行 `do` 和 `done` 之间的命令。如果你按 `RETURN` 键而没有输入选择项，shell 会重新显示菜单和 `PS3` 提示符。

`select` 结构会持续发出 `PS3` 提示符并执行命令，直到有某些原因使其退出——通常是 `break` 或 `exit` 语句。`break` 语句会退出循环，而 `exit` 语句会退出脚本。

以下脚本展示了 `select` 的用法：

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

```bash
$ ./fruit2
1) apple   3) blueberry   5) orange   7) STOP
2) banana   4) kiwi   6) watermelon
Choose your favorite fruit from these possibilities: 3
You chose blueberry as your favorite.
That is choice number 3.

Choose your favorite fruit from these possibilities: 99
Invalid entry.

Choose your favorite fruit from these possibilities: 7
Thanks for playing!
```

在设置 `PS3` 提示符并通过 `select` 语句建立菜单后，`fruit2` 执行 `do` 和 `done` 之间的命令。如果用户提交无效输入，shell 会将 `varname`（`$FRUIT`）设置为空值。如果 `$FRUIT` 为空，`echo` 会显示错误；`continue` 然后导致 shell 重新显示 `PS3` 提示符。如果输入有效，脚本会测试用户是否想停止。如果是，`echo` 会显示一条消息，并且 `break` 会退出 `select` 结构（以及脚本）。如果用户输入了有效响应并且不想停止，脚本会显示用户响应的名称和编号。（关于 `echo -c` 选项的信息见第 980 页。）

## HERE DOCUMENT

Here document（重定向输入）允许你从 shell 脚本内部将输入重定向到 shell 脚本。Here document 之所以这样命名，是因为它是*在此处*——即在 shell 脚本中立即可访问——而不是*在彼处*，也许在另一个文件中。

以下名为 `birthday` 的脚本包含一个 Here document。第一行中的两个小于号符号 (`<<`) 指示后面跟着一个 Here document。分隔 Here document 的一个或多个字符跟随在小于号符号之后——此例中使用加号。尽管开始的分隔符必须紧邻小于号符号，但结束的分隔符必须单独位于一行上。Shell 将两个分隔符之间的所有内容作为标准输入发送给进程。在示例中，这就好像将数据从文件重定向标准输入到 `grep`，除了该文件是嵌入在 shell 脚本中的：

```bash
$ cat birthday
grep -i '$1' <<+
Max    June 22
Barbara February 3
Darlene May 8
Helen  March 13
Zach   January 23
Nancy  June 26
+
$ ./birthday Zach
Zach    January 23
$ ./birthday June
Max    June 22
Nancy  June 26
```

当你运行 `birthday` 时，它会列出所有包含你调用它时使用的参数的 Here document 行。在这种情况下，第一次运行 `birthday` 时，它显示 `Zach` 的 `birthday`，因为它是以 `Zach` 为参数调用的。第二次运行显示六月份所有的生日。`-i` 参数使 `grep` 的搜索不区分大小写。

### 可选

下一个名为 `bundle` 的脚本巧妙使用了 Here document。`bundle` 脚本是一个优雅的示例，展示了创建一个 shell 归档（shar）文件的脚本。该脚本创建一个文件，该文件本身是一个 shell 脚本，包含其他几个文件以及重新创建原始文件的代码：

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

正如 shell 不将 shell 脚本标准输入中出现的特殊字符视为特殊字符一样，shell 也不将 Here document 中分隔符之间出现的特殊字符视为特殊字符。

如下例所示，`bundle` 的输出是一个 shell 脚本，它被重定向到名为 `bothfiles` 的文件。它包含作为 `bundle` 参数给出的每个文件的内容（在本例中为 `file1` 和 `file2`），这些内容位于一个 Here document 中。要从 `bothfiles` 中提取原始文件，你只需将其作为参数传递给 `bash` 命令。在每个 Here document 之前都有一个 `cat` 命令，该命令导致在运行 `bothfiles` 时将 Here document 写入新文件：

```bash
$ cat file1
This is a file.
It contains two lines.

$ cat file2
This is another file.
It contains
three lines.

$ ./bundle file1 file2 > bothfiles
$ cat bothfiles
# To unbundle, bash this file
echo file1 1>&2
cat >file1 <<'End of file1'
This is a file.
It contains two lines.
End of file1
echo file2 1>file2
cat >file2 <<'End of file2'
This is another file.
It contains
three lines.
End of file2
```

在下一个示例中，`file1` 和 `file2` 在运行 `bothfiles` 之前被删除。`bothfiles` 脚本在创建文件时会回显它创建的文件名。然后 `ls` 命令显示 `bothfiles` 已重新创建 `file1` 和 `file2`：

```bash
$ rm file1 file2
$ bash bothfiles
file1
file2
$ ls
bothfiles
file1
file2
```

2. 感谢 Brian W. Kernighan 和 Rob Pike，《The Unix Programming Environment》（Englewood Cliffs, N.J.: Prentice-Hall, 1984），第 98 页。经许可重印。

## FILE DESCRIPTORS

如第 297 页所述，在进程可以读取或写入文件之前，它必须打开该文件。当进程打开一个文件时，Linux 会将一个数字（称为文件描述符）与该文件关联。文件描述符是进程打开文件表中的一个索引。每个进程都有自己的一组打开的文件和文件描述符。打开文件后，进程通过引用其文件描述符来读取和写入该文件。当不再需要该文件时，进程关闭文件，释放文件描述符。

典型的 Linux 进程以三个打开的文件开始：标准输入（文件描述符 0）、标准输出（文件描述符 1）和标准错误（文件描述符 2）。通常，这些是进程所需的唯一文件。请记住，你可以使用符号 `>` 或符号 `1>` 重定向标准输出，并使用符号 `2>` 重定向标准错误。虽然你可以重定向其他文件描述符，但由于除 0、1 和 2 以外的文件描述符没有特殊的传统含义，因此这样做很少是有用的。例外情况是你自己编写的程序，在这种情况下，你控制文件描述符的含义并可以利用重定向。

Bourne Again Shell 使用 `exec` 内置命令按以下方式打开文件：

> 打开文件描述符

```bash
exec n> outfile
exec m< infile
```

第一行打开 `outfile` 用于输出并保持打开状态，将其与文件描述符 `n` 关联。第二行打开 `infile` 用于输入并保持打开状态，将其与文件描述符 `m` 关联。

## 函数不等于 shell 脚本

`<<&` 标记用于复制输入文件描述符；`>&` 用于复制输出文件描述符。你可以通过使某个文件描述符指向另一个已打开的文件描述符（如标准输入或标准输出）所引用的同一文件，来复制该文件描述符。使用以下格式将文件描述符 `n` 作为文件描述符 `m` 的副本打开或重定向：

```bash
exec n<&m
```

一旦你打开了一个文件，就可以以两种方式将其用于输入和输出。首先，你可以在任何命令行上使用 I/O 重定向，使用 `>&n` 将标准输出重定向到文件描述符，或使用 `<&n` 将标准输入从文件描述符重定向。其次，你可以使用 `read`（第 1003 页）和 `echo` 内置命令。如果你调用其他命令，包括函数（第 349 页），它们将继承这些打开的文件和文件描述符。当你不再使用某个文件时，可以使用以下命令关闭它：

```bash
exec n<&-
```

当你调用下一个示例中名为 `mycp` 的 shell 函数并提供两个参数时，它会将第一个参数指定的文件复制到第二个参数指定的文件。如果你只提供这一个参数，脚本会将该参数指定的文件复制到标准输出。如果你在不提供任何参数的情况下调用 `mycp`，它会将标准输入复制到标准输出。

> **提示** `mycp` 示例是一个 shell 函数；如果你将其作为 shell 脚本执行，它不会按预期工作。（它确实会运行：该函数将在一个寿命极短的子 shell 中创建，这通常没什么用。）你可以从键盘输入此函数。如果你将函数放入文件中，可以作为 `.`（点）内置命令（第 296 页）的参数来运行它。如果你希望它始终可用，也可以将函数放入启动文件中（第 351 页）。

```bash
function mycp ()
{
    case $# in
        0)
            # 零个参数
            # 文件描述符 3 复制标准输入
            # 文件描述符 4 复制标准输出
            exec 3<&0 4>&1
            ;;
        1)
            # 一个参数
            # 打开参数指定的文件用于输入
            # 并将其与文件描述符 3 关联
            # 文件描述符 4 复制标准输出
            exec 3< $1 4>&1
            ;;
        2)
            # 两个参数
            # 打开第一个参数指定的文件用于输入
            # 并将其与文件描述符 3 关联
            # 打开第二个参数指定的文件用于输出
            # 并将其与文件描述符 4 关联
            exec 3< $1 4> $2
            ;;
        *)
            echo "Usage: mycp [source [dest]]"
            return 1
            ;;
    esac

    # 调用 cat，输入来自文件描述符 3
    # 输出去往文件描述符 4
    cat <&3 >&4

    # 关闭文件描述符 3 和 4
    exec 3<&- 4<&-
}
```

该函数的实际工作是在以 `cat` 开头的那一行完成的。脚本的其余部分安排文件描述符 3 和 4（即 `cat` 命令的输入和输出）与适当的文件相关联。

**可选** 下一个程序在命令行上接收两个文件名，对它们进行排序，并将输出发送到临时文件。然后，程序将排序后的文件合并到标准输出，并在每行前面加上一个数字，指示该行来自哪个文件。
