
要查看系统中可用的文件，请使用 `list` 命令（`ls`）。本节描述了 `ls` 命令以及可用于格式化其显示信息的选项。

## 显示基本列表

最基础形式的 `ls` 命令显示位于当前目录中的文件和目录：

```
$ ls
 Desktop    Downloads   my_script   Public      test_file
 Documents  Music       Pictures    Templates   Videos
$
```

请注意，`ls` 命令生成的列表是按字母顺序排列的（以列而非行显示）。如果你使用的是支持颜色的终端模拟器，`ls` 命令也可能以不同颜色显示不同类型的条目。环境变量 `LS_COLORS` 控制此功能。（环境变量在 **第 6 章** 中有详细说明。不同的 Linux 发行版会根据终端模拟器的功能设置此环境变量。）

如果你没有彩色终端模拟器，可以使用 `-F` 参数与 `ls` 命令结合使用，以便轻松区分文件和目录。使用 `-F` 参数会产生以下输出：

```
$ ls -F
Desktop/   Downloads/  my_script*  Public/    test_file
Documents/ Music/      Pictures/   Templates/ Videos/
$
```

`-F` 参数用正斜杠（`/`）标记目录，以帮助在列表中识别它们。类似地，它用星号（`*`）标记可执行文件（如前面代码中的 `my_script` 文件），帮助你更容易地在系统中找到可以运行的文件。

基本的 `ls` 命令可能会产生一些误导。它显示当前目录中包含的文件和目录，但不一定显示所有文件。Linux 经常使用*隐藏文件*来存储配置信息。在 Linux 中，隐藏文件是文件名以句点（`.`）开头的文件。这些文件不会出现在默认的 `ls` 列表中。因此，它们被称为隐藏文件。

要显示隐藏文件以及普通文件和目录，请使用 `-a` 参数。以下是使用 `-a` 参数与 `ls` 命令的示例：

```
$ ls -a
.  .bash_profile   Desktop  .ICEauthority
.. my_script       Templates  .bashrc   Documents  .local
.bash_history      Pictures test_file   .cache   Downloads  .mozilla   .pki
.bash_logout .config .esd_auth Music
Public
$
```

所有以句点开头的文件，即隐藏文件，现在都显示出来了。请注意，有四个文件以 `.bash` 开头。这些是由 Bash shell 环境使用的隐藏文件，将在第 6 章中详细涵盖。

`-R` 参数是 `ls` 命令可以使用的另一个选项。它被称为递归选项，用于显示当前目录中包含在子目录中的文件。如果你有很多子目录，这个列表可能会非常长。下面是 `-R` 参数产生的简单示例。为了帮助你查看文件类型，附加了 `-F` 选项：

```
$ ls -F -R
 .:
 Desktop/    Downloads/  my_script*  Public/     test_file
 Documents/  Music/      Pictures/   Templates/  Videos/
 
 ./Desktop:
 
 ./Documents:
 
 ./Downloads:
 
 ./Music:
 I LoveLinux.mp3*
 
 ./Pictures:
 
 ./Public:
 
 ./Templates:
 
 ./Videos:
 $
```

请注意，`-R` 参数显示了当前目录的内容，即前面示例中显示的用户主目录中的文件。它还显示了用户主目录中的每个子目录及其内容。唯一包含文件的子目录是 Music 子目录，其中包含可执行文件 `ILoveLinux.mp3`。

> **提示**
> **选项参数不必像前一个示例中那样分开输入：`ls -F -R`。通常可以将它们组合如下：`ls -FR`。**

在上面的示例中，子目录内没有进一步的子目录。如果存在进一步的子目录，`-R` 参数也会继续遍历这些子目录。可以想象，对于大型目录结构，这可能成为一个非常长的列表。

## 显示长列表

在基本列表中，`ls` 命令关于每个文件的信息不多。要列出更多信息，另一个常用参数是 `-l`。`-l` 参数生成长列表格式，提供目录中每个文件的更多信息：

```
$ ls -l
   total 8
   drwxr-xr-x.  2 christine christine     6 Feb 20 14:23 Desktop
   drwxr-xr-x.  2 christine christine     6 Feb 20 14:23 Documents
   drwxr-xr-x.  2 christine christine     6 Feb 20 14:23 Downloads
   drwxr-xr-x.  2 christine christine    28 Feb 29 15:42 Music
   -rwxrw-r--.  1 christine christine   74 Feb 29 15:49 my_script
   drwxr-xr-x.  2 christine christine     6 Feb 20 14:23 Pictures
   drwxr-xr-x.  2 christine christine     6 Feb 20 14:23 Public
   drwxr-xr-x.  2 christine christine     6 Feb 20 14:23 Templates
   -rw-rw-r--.  1 christine christine   74 Feb 29 15:50 test_file
   drwxr-xr-x.  2 christine christine     6 Feb 20 14:23 Videos
   $
```

长列表格式将每个文件和目录列在单独的一行上。除了文件名外，列表还显示其他有用的信息。输出的第一行显示目录内文件分配的总块数（8）。之后，每一行包含关于每个文件（或目录）的以下信息：

- 文件类型 —— 例如目录 `d`、文件 `-`、链接文件 `l`、字符设备 `c` 或块设备 `b`
- 文件权限（参见第 7 章）
- 文件硬链接的数量（参见本章“链接文件”部分）
- 文件所有者的用户名
- 文件的主组名
- 文件字节大小
- 文件最后修改时间
- 文件或目录名称

`-l` 参数是一个强大的工具。配备此参数，你可以看到大多数任何文件或目录所需的信息。

> **提示**
> 
> 如果你只想查看单个文件的长列表，只需将文件名附加到你的 `ls -l` 命令即可。但是，如果你想查看目录的此类列表（而不是其内容），你不仅需要在命令中添加其名称，还需要添加 `-d` 开关，例如：`ls -ld` `Directory-Name`。

`ls` 命令有很多参数，在你进行文件管理时可能会派上用场。如果你在 shell 提示符下输入 `man ls`，你会看到几页可用的参数，供你修改 `ls` 命令的输出使用。

别忘了，你还可以组合许多参数。你通常可以发现一种参数组合，不仅显示期望的输出，而且容易记住，例如 `ls -aIf`。

## 过滤列表输出

正如你在示例中看到的，默认情况下，`ls` 命令列出所有非隐藏目录文件。有时，这可能有点过度，特别是当你只是在寻找几个文件的信息时。

幸运的是，`ls` 命令也提供了一种在命令行上定义过滤器的方法。它使用过滤器来确定应该在输出中显示哪些文件或目录。

在使用过滤器命令之前，让我们通过 `touch` 命令（将在下一节中介绍）创建一些文件来玩玩。如果文件已经存在，该命令不会损坏文件：

```
$ touch my_script my_scrypt my_file
$ touch fall fell fill full
$ ls
Desktop     Downloads   fell      full      my_file     my_script
Public      test_file
Documents   fall        fill      Music     my_scrypt   Pictures
Templates   Videos
$
```

过滤器作为一个简单的文本匹配字符串工作。将你希望使用的任何命令行参数之后包含过滤器：

```
$ ls -l my_script
-rwxrwr-r--. 1 christine christine 74 Feb 29 16:12 my_script
$
```

当你指定特定文件的名称作为过滤器时，`ls` 命令仅显示该文件的信息。有时，你可能不知道确切的文件名你在寻找什么。`ls` 命令还识别标准通配符，并使用它们匹配过滤器内的模式：

- 问号 `?` 代表一个字符
- 星号 `*` 代表任意数量的字符

问号可用于替换过滤器字符串中任何位置的恰好一个字符。例如：
