
这里是`s`如何使用选项 `h` 以人类可读的格式显示输出，以及使用 `s` 显示此目录的所有磁盘占用情况。虽然我们指定了工作目录（`.`），但可以给定任何目录。

### 文件命令

#### 创建空文件

有时，创建一个空文件作为未来内容的占位符是有用的。可以使用 `touch` 命令在不带任何选项的情况下创建一个空文件，如下：

```
$ touch /home/tclark/touch1.fil
$ touch touch2.fil
$ ls -l
total 6
drwxr-xr-x 2 tclark tclark 4096 Jan 13 17:48 examples
-rw-rw-r-- 1 tclark tclark 0 Jan 13 19:13 touch1.fil
-rw-rw-r-- 1 tclark tclark 0 Jan 13 19:14 touch2.fil
```

`touch` 命令还有一个选项，允许使用 `-t` 选项更改现有文件的时间戳信息。在接下来的示例中，上述 `touch1.fil` 的时间戳将被更改为 1 月 10 日 12:00。该选项的日期格式是一个数字字符串，月、日、小时（24 小时制）和分钟各占两位，因此 1 月 10 日 12:00 的字符串将是 `01101200`。例如，用户可能希望更改目录中的一组文件以指示特定日期。

```
$ touch -t 01101200 touch1.fil
$ ls -l
total 4
drwxr-xr-x 2 tclark tclark 4096 Jan 13 17:48 examples
-rw-rw-r-- 1 tclark tclark 0 Jan 10 12:00 touch1.fil
-rw-rw-r-- 1 tclark tclark 0 Jan 13 19:14 touch2.fil
```

#### 关于通配符的简单讨论

许多常用的文件和目录操作命令（包括本章中提到的大多数命令）都允许你使用部分文件名并用通配符字符替换其余。这些通配符可以节省大量的打字时间，但也可能留下模糊的结果，从而导致意外删除！两个最常用的通配符字符是星号 (`*`) 和问号 (`?`)。`*` 通常称为星号，它将匹配文件名中的任意数量的字符，即使没有字符也是如此。`?` 将匹配文件名中的任何单个字符。这里有几个示例，可以让通配符变得有点清晰：

```
$ cd ~/examples
ls declaration.txt preamble.txt
$ ls touch*
$ ls touch?
$ ls
```

#### 删除文件

可以使用 `rm`（删除）命令来删除文件；通过绝对路径或相对路径引用文件。可以使用 `*` 和 `?` 等通配符符号删除名称相似的文件。使用 `rm` 命令时要小心，特别是 Linux 倾向于直接删除你请求的内容！以下是 `rm` 命令的一些示例：

```
$ rm /home/tclark/touch1.fil
$ ls examples
$ rm touch2.fil
$ ls
```

`rm` 命令可以配合 `-r`（递归）选项来删除目录及其内容。`rm` 命令与其他影响多个文件的命令一样应该谨慎使用。

```
$ mkdir -p new_dir
$ ls new_dir
rm -r new_dir
$ ls
```

#### 防止意外删除

一些 Linux 用户喜欢实现的一种防止意外删除的小技巧是通过使用别名（`alias`）。别名类似于变量，可以在会话中设置，也可以通过 `.bash_profile` 文件设置。通过添加此别名，用户将在删除每个文件之前收到提示；否则，它像像 Windows 那样直接删除符合条件的文件！

```
$ alias rm='rm -i'
$ touch touch1.fil touch2.fil touch3.fil
$ rm touch*
rm: remove regular file 'touch1.fil'?
rm: remove regular file 'touch2.fil'?
rm: remove regular file 'touch3.fil'?
```

```
$ cd -
/home/tclark
$ mv /tmp/templ1.fil /tmp/templ.xxx
$ cd -
/tmp
$ ls temp*
templ1.xxx temp2.fil
```

此示例演示了如何通过使用绝对路径对非当前工作目录的目录执行命令。

- 将当前工作目录下的 `example2.fil` 重命名为 `example2.xxx`：

```
$ ls
examples
$ touch example1.fil example2.fil
$ ls
example1.fil example2.fil examples
$ mv example1.fil example2.xxx
$ ls
example1.fil example2.xxx examples
```

到目前为止，我们已经讨论了操纵文件和目录的几种方法。由于这些命令非常强大，你可能会发现自己在进行某些更改之前想要进行备份。我们将在下一节中查看如何实现这一点。

### 归档目录和文件

有几个原因你可能想要创建一个文件或目录的归档。以下是一些最常见的原因：

- 归档并压缩未使用的目录以节省磁盘空间
- 在升级之前创建目录和文件的归档，以便在出现问题时恢复原始内容
- 在进行任何重大更改之前归档目录
- 创建归档将多个文件和文件夹作为一个整体移动到另一个系统
- 创建归档作为软件分发的手段

归档一组文件和目录最实用的工具之一是 `tar`。`tar` 名称是 Tape ARchiver（磁带归档器）的缩写，因为 `tar` 最初是为了将数据写入磁带备份设备。

以下是将目录归档为 `tar` 归档文件并将该归档提取到其原始结构的简单示例。

```
$ tar -cvf examples.tar examples
examples/
examples/declaration.txt
examples/gettysburg.txt
examples/preamble.txt
$ rm -r examples
$ ls
examples.tar
$ tar -xvf examples.tar
examples/
examples/declaration.txt
examples/gettysburg.txt
examples/preamble.txt
$ ls
examples examples.tar
```

在这个示例中，我们演示了创建新归档的两种最常用的用法。第一个 `tar` 命令结合了 `-c`（创建）选项、`-v`（详细）选项以列出正在归档的文件和目录，以及 `-f` 选项将其写入文件而非磁带。记住，`tar` 最初是为磁带驱动器设计的，如果不使用 `-f` 选项，它仍然默认使用磁带。

此 `tar` 命令的两个参数是目标文件（在示例中为 `examples.tar`）和要添加到该文件的文件。这可能会让人困惑，因为大多数其他 Linux 命令在目标参数之前接收源参数。`tar` 接收参数的顺序是先目标后源，你可以列出多个要归档到单个文件中的源文件。另外注意，如果我们希望新归档具有扩展名，则必须指定文件扩展名（`.tar`）。你可以为 `tar` 归档（通常称为 tarball）命名任何名称，但 `.tar` 扩展是一个被广泛接受的习惯。

在第二个 `tar` 命令中，`-v` 和 `-f` 选项的效果相同，而 `-x`（提取）选项告诉 `tar` 我们想要提取 `tar` 文件的内容而不是创建一个。我们给 `tar` 要提取的归档名称，它就会开始工作恢复我们的文件。

#### 关于 tar 中相对路径和绝对路径的警告

与其他命令一样，`tar` 可以配合相对路径或绝对路径使用。在指定要创建或提取的 `tar` 文件时，这两种方法之间区别不大；然而，如果你在列出要归档的文件时使用绝对路径，当你提取它们时可能会感到意外！

如果使用绝对路径来告诉 `tar` 要归档哪些文件（如下所示命令所示），归档将记录绝对路径并将这些文件恢复到该路径，无论从何处运行 `tar` 或 `tar` 文件位于何处。

```
$ tar -cf examples.tar /home/tclark/examples
```

如果不指定绝对路径，归档的文件将提取到（运行 `tar` 命令时的）当前工作目录。

### 合并文件

有时，可能需要合并或连接多个文件。`cat` 命令（`concatenate` 的缩写）是完成此任务的一种简单方法。`cat` 命令可以接受多个文件名作为参数并将它们输出。

默认情况下，`cat` 会按列出的顺序输出文件。在这个示例中，我们使用 `cat` 将 `file1.dat` 和 `file2.dat` 合并到一个文件。

```
$ cat file1.dat file2.dat > combined
```

在下一节中，我们将看到 `cat` 命令除了合并文件之外还有什么用。

### 显示内容

有趣的是，`cat` 命令也用于显示文件的内容。为了在屏幕上一次显示较大的文件，可以使用 `more` 或 `less` 命令。`more` 命令已经过时，并在很大程度上被 `less` 命令取代了。`less` 命令实际上具有更多选项，例如导航到文件的特定行。要退出 `less` 显示，只需输入 `q`。
