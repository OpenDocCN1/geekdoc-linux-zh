
# PS3 与 `select` 结构

PS3 在显示菜单后，`select` 显示 PS3 的值，即 `select` 提示符。PS3 的默认值为 `"#>"`，但通常会被设置为一个更有意义的值。当你输入一个值（菜单范围内的值）时，`select` 会响应 PS3 提示符设置参数中的 *varname*。无效输入会导致 shell 将 *varname* 设置为空值。`select` 要会将你的响应存储在关键字变量 `REPLY` 中，并执行一次菜单与 `do` 之间的命令。如果你在没有输入选择的情况下按了回车，shell 会重新显示菜单和 PS3 提示符。

`select` 结构会继续发布 PS3 提示符并执行命令，直到某些内容退出——通常是 `break` 或 `exit` 语句。`break` 语句退出循环，`exit` 语句退出脚本。

以下脚本说明了其用法：

```bash
$ select fruit
#!/bin/bash
PS3="Choose your favorite fruit from these possibilities: "
select fruit in apple blueberry kiwi watermelon STOP

if [ "$FRUIT" != "" ]; then
	echo -e "Invalid entry.\n"
	continue
elif [ "$FRUIT" = STOP ]; then
	echo "Thanks for playing!"
	break
fi
echo "You chose $FRUIT as your favorite."
echo -e "That is choice number $REPLY.\n"
done
```

```bash
$ - /Fruit2 3) blueberry 5) orange 7) STOP
1) apple
2) banana 4) kiwi 6) watermelon
Choose your favorite fruit from these possibilities: 3
You choose blueberry as your favorite.
That is choice number 3.

Choose your favorite fruit from these possibilities: 99
Invalid entry.

Choose your favorite fruit from these possibilities: 7
Thanks for playing!
```

在设置 PS3 提示符并使用 `select` 语句建立菜单后，程序会执行 `do` 和 `done` 之间的命令。如果用户插入了无效输入，shell 会将 `(FRUIT)` 设置为空值。如果 `FRUIT` 无效，`echo` 会显示错误；`continue` 导致 shell 显示 PS3 提示符。如果输入有效，脚本将测试用户是否想要停止。因此，`echo` 显示消息，`break` 退出 `select` 结构（并退出脚本）。如果用户输入了有效响应且不想停止，脚本将显示用户响应的名称和编号。（关于 `echo` 选项的信息请参见第 980 页。）

## Here Document（在此文档中）

在此文档（Here Document）允许你在 shell 脚本内部将输入重定向。之所以命名为在此文档，是因为它就在“这里”——脚本可以直接访问——而不是在另一个文件中。

以下名为 `birthday` 的脚本包含一个在此文档。两个 `<<` 符号指示后续有一个在此文档。一个或多个字符可以使用加号；起始分隔符必须相邻出现，结束分隔符必须独占一行。shell 将两个分隔符之间的所有内容作为标准输入发送给进程。示例中是将标准输入重定向到文件，只是该文件嵌入在 shell 脚本中。

- * $ cat birthday

grep "**" <<

Max June 22

Barbara 3

Darlene May 8

Helen March 13

Zach January 23

Nancy June 26

- * $ /birthday

Zach January 23

$ /birthday June

Max June 22

Nancy June 26

当你运行 `birthday` 时，它会列出包含你调用参数在此文档行。在这种情况下，第一次运行 `birthday` 时，它显示参数 Zach 的生日。第二次运行显示 June 的生日。`-l` 参数导致 `grep` 搜索时不显示文件名。

下一个名为 `bundle` 的脚本巧妙地使用了在此文档。`bundle` 脚本是创建归档（tar）脚本的优雅示例。该文件脚本创建一个本身也是 shell 脚本的文件，用于重建原始文件：

```bash
$ cat bundle
#!/bin/bash
# bundle: 将文件分组为发行文件

echo "- Unbundle, bash this file"
for i

	echo "echo $i"
	cat >$i <<'End of $i'
	cat $i
	echo "End of $i"
done
```

就像 shell 不处理特殊字符一样，shell 也不会将 shell 脚本中出现的在此文档中的分隔符视为特殊字符。

如下例所示，`bundle` 的输出是一个 shell 脚本，该脚本被重定向到包（在这种情况下为 `file1` 和 `file2`），包含了作为参数在此文档内部的每个文件的内容。要从 `bundles` 提取原始文件，只需将其作为 bash 命令的参数即可。在每个文档之前有一个 `cat` 命令，该命令导致运行 `bundles` 时会将在此文档写入新文件：

```bash
$ cat file1
This is a file.
It contains two lines.
$ cat file2
This is another file.
It contains three lines.

$ bundle file1 file2 > bundles
$ cat bundles
echo file1 1<2
cat >file1 <<'End of file1'
```

当你调用下一个示例中带参数的 shell 函数 `mycp` 时，你是作为 shell 脚本来执行它的，它会将第一个参数指定的文件复制到第二个参数指定的文件。如果你只提供一个参数，脚本将把该参数指定的文件复制到标准输出。如果你在不带参数的情况下调用 `mycp`，它会将标准输入复制到标准输出。函数不是脚本；当你将其作为参数执行时它将无法工作（它会生效：该函数将在一个短命的子 shell 中创建，这可能没什么用处）。你可以从键盘输入此函数。如果你将函数放在文件中，可以将其作为参数运行（见第 296 页）。如果你想让它始终可用，可以将其放在启动文件中（见第 51 页）。

# 文件描述符 987

这是一个文件。

它包含两行。

file1 结束

echo file2 1>&2

cat >file2 <<End of file2

这是另一个文件。

它包含

三行。

file2 结束。

在下一个示例中，在运行 `bothfiles` 之前，file1 和 file2 会被删除。`bothfiles` 脚本在创建文件时会输出它创建的文件名。随后 `ls` 命令显示 `bothfiles` 重新创建了 file1 和 file2。

```
$ rm file2
$ bash bothfiles
file2
$ ls
bothfiles
file1
file2
```

# 文件描述符

正如第 297 页讨论，在进程对文件进行读取或写入之前，它必须先打开该文件。当一个进程打开一个文件时，Linux 会将该文件与一个数字（称为文件描述符）关联。文件描述符是进程打开文件表中的索引。每个进程都有自己的打开文件列表和对应的文件描述符。打开文件后，进程通过引用其文件描述符对文件进行读取和写入。当它不再需要该文件时，进程会关闭文件并释放文件描述符。

一个典型的 Linux 进程从三个文件启动：标准输入（文件描述符 0）、标准输出（文件描述符 1）和标准错误（文件描述符 2）。这些是进程需要的文件。记住，你使用符号 `>` 或 `1>` 重定向输出，使用符号 `2>` 重定向标准错误。虽然你可以重定向其他描述符，但由于除 0、1 和 2 以外的文件描述符没有任何约定俗成的含义，这样做通常没有用。例外是你自己编写的程序，在这种情况下，你控制文件描述符的含义并可以利用重定向的便利处。

Bourne Shell 使用 `exec` 内置命令按如下方式打开文件：

```
exec n outfile
exec m< infile
```
