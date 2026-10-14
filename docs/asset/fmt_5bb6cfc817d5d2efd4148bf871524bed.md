
符号链接是为了克服硬链接的局限性而创建的。它们通过创建一个特殊类型的文件来工作，该文件包含一个指向被引用文件或目录的文本指针。在这方面，它们的操作方式与 Windows 快捷方式相似，尽管它们早于 Windows 的这一功能多年。

被符号链接指向的文件和符号链接本身是无法区分的。例如，如果你向符号链接写入内容，内容会被写入所指向的文件。然而，当你删除符号链接时，删除的只是链接，而不是文件。如果在删除符号链接之前删除了文件，链接将继续存在但指向空值。在这种情况下，该链接被称为“断开的”。在许多实现中，`ls` 命令将用不同的颜色（如红色）显示断开的链接以显示它们的存在。

链接的概念可能看起来很混乱，但请坚持。我们将尝试所有这些内容，理想情况下它们会变得清晰。

目标文件相对于符号链接的路径描述。通过查看 `ls` 的输出可以更容易看到这一点，如下所示：

目录中 `fun-sym` 的列表显示，通过第一个文件的开头字符可以看出它是一个符号链接，并且它指向 `../fun`，这是正确的。相对于 `fun-sym` 的位置，它在上级目录。同时请注意，符号链接文件的长度为 6，即该字符串的字符数，而不是它所指向的文件长度。

在创建符号链接时，你可以使用绝对路径，如下所示：

```
[me@linux playground]$ ls -s /home/me/playground/fun dir1/fun-sym
```

除了普通文件外，符号链接还可以引用目录。

```
[me@linux playground]$ ls -d dir1-dir-sym
[me@linux playground]$ ls -l
total 16
drwxr-xr-x 2 me 4096 2018-01-15 15:17 dir1
-lrwxrwxr-x 1 me 4096 2018-01-16 14:45 dir1-sym -> dir2
drwxr-xr-x 2 me 4096 2018-01-15 15:17 dir2
-rw-r--r- 4 me 1650 2018-01-10 16:33 fun
-rw-r--r- 4 me 1650 2018-01-10 16:33 fun-hard
-lrwxrwxr-x 1 me 3 2018-01-15 15:15 fun-sym -> fun
```

# 删除文件和目录

正如我们之前介绍过的，`rm` 命令用于删除文件和目录。我们将使用它来稍微清理一下我们的实验场。让我们删除其中一个硬链接。

```
[me@linux playground]$ rm fun-hard
[me@linux playground]$ ls -l
total 12
drwxr-xr-x 2 me 4096 2018-01-15 15:17 dir1
-lrwxrwxr-x 1 me 4096 2018-01-16 14:45 dir1-sym -> dir2
drwxr-xr-x 2 me 4096 2018-01-15 15:17 dir2
-rw-r--r- 3 me 1650 2018-01-10 16:33 fun
-lrwxrwxr-x 1 me 3 2018-01-15 15:15 fun-sym -> fun
```

该操作符合预期。文件 `fun-hard` 已经消失，`fun` 显示的 `fun` 链接计数也从四个减少到了三个，正如目录列表的第二个字段所示。接下来，我们将删除 `fun` 文件以消遣无事，并会包含 `-i` 选项来展示它的作用。

```
[me@linux playground]$ rm -i fun
rm: remove regular file 'fun'?
```

在提示符处按回车，文件就会被删除。但让我们看看 `ls` 的输出。注意 `fun-sym` 发生了什么？因为它是指向一个不存在文件的符号链接，所以该链接已损坏。

```
[me@linux playground]$ ls -l
total 8
drwxr-xr-x 2 me 4096 2018-01-15 15:17 dir1
drwxr-xr-x 1 me 4 2018-01-16 14:45 dir-sym -> dir
drwxr-xr-x 2 me 4096 2018-01-15 15:17 dir2
drwxr-xr-x 1 me 3 2018-01-15 15:15 fun-sym -> fun
```

大多数 Linux 发行版都配置为删除断开的链接。断开链接本身并不危险，但它显得很凌乱。如果我们尝试使用断开的链接，将会看到这些：

```
[me@linux playground]$ less fun-sym
fun-sym: No such file or directory
```

让我们清理一下。我们在这里删除这些符号链接：

```
[me@linux playground]$ rm fun-sym dir1-sym
[me@linux playground]$ ls -l
total 8
drwxr-xr-x 2 me 4096 2018-01-15 15:17 dir1
drwxr-xr-x 2 me 4096 2018-01-15 15:17 dir2
```

关于符号链接需要记住的一点是，文件操作是在链接上进行的，而不是目标上。`rm` 是一个例外。当你删除一个链接时，删除的是链接本身，而不是目标。

最后，我们将删除实验场。为此，我们将返回主目录并使用带有递归选项 `-r` 的 `rm` 命令删除 `playground` 及其所有内容，包括它的子目录。

```
[me@linux playground]$ cd
[me@linux ~]$ rm -r playground
```

# 使用 GUI 创建符号链接

GNOME 和 KDE 的文件管理器提供了创建符号链接以便方法。在 GNOME 中，按住 `Shift` 键拖动文件即可。在 KDE 中，同样如此。

## 总结

我们已经涵盖了什么是命令，以及如何操作命令。

# 命令是什么

## 获取命令文档

有了这些命令的知识，我们现在可以搜索每个命令对应的文档。

## help——获取内置命令的帮助

`bash` 为每个 shell 内置命令提供了帮助。要使用它，输入 `help` 后跟 shell 内置命令。例如：

```
[me@linux ~]$ help cd
cd: cd [-L[-P [-e]]] [[@]] [dir]
切换当前目录到 DIR。
```

切换当前目录到 DIR。默认 DIR 是 `HOME` 的值。

变量 `CDPATH` 定义了包含 DIR 的搜索路径。`CDPATH` 中的替代目录名用冒号分隔。空目录名等于当前目录。如果 DIR 以斜杠 `/` 开头，则不使用 `CDPATH`。

如果找不到目录并且设置了 shell 选项 `cdable`，则该单词被假设为变量名。如果该变量有值，则使用该值作为 DIR。

选项：

- `L` 跟踪符号链接：在处理 DIR 实例后解析符号链接

- `P` 使用物理目录结构而不跟踪符号链接：在处理 DIR 实例前解析符号链接

- `e` 如果提供了 `-P` 选项，且无法成功确定当前目录，则以非零状态退出 @ 在支持扩展属性的系统上，将具有扩展属性的文件作为包含文件属性的目录展示

默认遵循符号链接，就像指定了 `-L` 一样。

`..` 通过移除紧邻的上一个路径组件直到遇到斜杠或 DIR 的开头来处理。

退出状态：

如果目录切换成功，且在使用 `-P` 时 `$PWD` 设置成功，则返回 0；否则返回非零。

关于符号的说明：当命令描述中出现方括号时，它们表示可选项目。竖线字符 `|` 表示互斥的项目。在上述 `cd` 命令的中：

```
cd [-l|[-P[-e]]]
```

这种符号表示命令后面可以可选地接 `-l` 或 `-P`，此外，如果指定了 `-P` 选项，可选参数 `dir` 还可以包含 `-e` 选项。

`cd` 命令的帮助输出简洁且准确，它绝不是教程，而且我们所见，它似乎提到了许多我们还没有讨论过的内容！别担心，我们会学到的。

## --help—显示用法信息

许多可执行程序都支持 `--help` 选项，用于显示命令支持的语法和选项的描述。例如：

```
me@linuxbox~$ mkdir --help
Usage: mkdir [OPTION]... DIRECTORY...
Create the DIRECTORY(ies), if they do not already exist.
```

- 长选项的强制参数对于短选项也是强制的。

- `-Z`, `--context=CONTEXT` (Linux) 将安全上下文设置为 `CONTEXT`

- `-m`, `--mode=MODE` 设置文件模式（在 `chmod` 中），等同于 `rwx` `umask`

- `-p`, `--parents` 如果已存在则不报错，根据需要创建目录

- `-v`, `--verbose` 为每个创建的目录打印消息

- `--help` 显示此帮助并退出

- `--version` 输出版本信息并退出

如需报告漏洞（bug），请向 `bug-coreutils@gnu.org` 提交报告。
