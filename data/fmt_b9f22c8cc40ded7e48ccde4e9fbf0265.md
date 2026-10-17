
# 处理命令行

当你使用 `--help` 参数调用 GNU 工具时，它们会显示一条（有时是非常详细的）帮助信息。由 GNU 项目开发的所有工具都接受此选项。示例所示。

```
$ bzip2 --help
bzip2, b-sorting file compressor. Version 1.0.2, 30-Dec-2001.

usage: bzip2 [flags and input files in any order]

-h --help print this message
-d --decompress force decompression
-z --compress force compression
-k --keep keep (don't delete) input files
-f --force overwrite existing output files
-t --test test compressed file integrity
-c --stdout output to standard out
-q --quiet suppress noncritical error messages
-v --verbose be verbose (a 2nd -v gives more)
```

当你输入命令行时，tty 设备驱动程序（Linux 操作系统内核的一部分）会检查每个字符，以查看其是否需要立即采取操作。当你按下 `CONTROL-H`（删除一个字符）或 `CONTROL-U`（删除整行）时，设备驱动程序会根据需要立即调整命令行；shell 永远看不到你删除的字符或你删的行。当你按下 `CONTROL-W`（删除一个单词）时，也会发生类似的调整。当输入的字符不需要立即操作时，设备驱动程序会将命令存储在缓冲区中并等待额外的字符。当你按下 `RETURN` 时，驱动程序将命令行传递给 shell 处理。

当 shell 处理命令行时，它将该行视为整体并将其解析（拆分）为各个组成部分。接下来，shell 查找命令名称，它是参数（参数 0）之后的第一个项目。shell 获取命令行上从开始到第一个空白（制表符或空格）的字符，并查找具有该名称的命令。命令名称（第一个标记）可以通过文件名或路径名的形式在命令行上指定。例如，你可以通过以下两种方式之一调用 `ls` 命令：

```
$ ls
$ /bin/ls
```

## 可选的 shell

shell 并不要求程序名称必须出现在命令行的开头。因此，你可以按照如下构造命令行：

```
$ >bb <aa cat
```

此命令执行时，标准输入来自名为 `aa` 的文件，标准输出指向名为 `bb` 的文件。当 shell 识别出重定向符号时——它识别并处理这些符号，并在找到命令行正在调用的程序名称之前完成处理。这是一个结构正确的——尽管较少遇到且可能令人困惑——命令行。

## 绝对文件名与相对文件名

当你在命令行上给出绝对路径或不是简单文件名的相对路径名（即包含至少一个斜杠的任何路径名）时，shell 会查找指定的目录（对于 `/bin/ls` 命令来说为 `/bin`）或名为 `ls` 且你具有执行权限的文件。当你给出一个简单的文件名时，shell 会在目录列表中搜索与指定名称匹配且你具有执行权限的文件。shell 不会遍历所有目录，而只遍历名为 `PATH` 的变量指定的目录。有关 `PATH` 的更多信息请参见第 302 页。另请参见第 164 页关于 `which` 和 `whereis` 工具的讨论。

## 命令未找到

当找不到可执行文件时，Bourne Again Shell (bash) 会显示如下消息：

```
$ abc
bash: abc: command not found
```

shell 可能无法找到可执行文件的原因是它不在你的 `PATH` 目录中。在 bash 下，以下命令会将工作目录（`.`）临时添加到你的 `PATH` 中：

```
$ export PATH=$PATH:.
```

出于安全考虑，你可能不想将工作目录永久添加到 `PATH` 中。

## 尝试通过 ./command 提供命令

你始终可以通过在文件名名前加上 `./` 来执行工作目录中的一个可执行文件。例如，如果 `myprog` 是工作目录中的一个可执行文件，无论 `PATH` 如何设置，你都可以通过以下命令执行它：

```
$ ./myprog
```

当 shell 找到程序但无法执行它（如果你没有包含程序的文件的执行权限）时，它会显示类似下面的消息：

```
$ ./def
bash: ./def: Permission denied
```

请参见第 199 页的“ls -l: Displays Permissions”获取有关显示文件访问权限的信息，并参见第 200 页的“chmod: Changes Access Permissions”获取如何更改文件访问权限的说明。

## 执行命令行

如果你执行一个与命令同名的可执行文件，shell 会启动一个新进程。进程是 Linux 对命令的执行。shell 使每个命令行参数（包括选项和命令名称）对被调用的程序可用。在命令执行期间，shell 等待进程完成。当程序结束时，它会将退出状态传递给 shell。shell 返回活动状态，发出提示符并等待另一个命令。

## 编辑命令行

你可以重复并编辑命令行。更多信息请参见第 139 和 314 页。

# 标准输入与标准输出

**标准输出**是程序可以发送信息（如文本）的地方。程序不知道它发送要去哪里。信息可以去打印机、普通文件或屏幕。接下来的章节显示默认情况下 shell 将命令的标准输出定向到屏幕，并描述如何使用 shell 将此输出重定向到另一个文件。

**标准输入**是程序获取信息的地方。与标准输出一样，程序不知道信息来自哪里。接下来的章节还解释了如何重定向标准输入使其来自普通文件而不是键盘（默认值）。

除了标准输入、标准输出外，程序通常还有一个发送错误消息的地方：*标准错误*。有关处理标准错误的更多信息请参见第 280 页。

## 作为文件的屏幕

第 6 章介绍了普通文件、目录文件以及硬/软链接。Linux 有另一种类型的文件：设备文件。设备文件位于 Linux 结构中，通常在 `/dev` 目录中，代表外围设备，如终端模拟窗口、屏幕、打印机或磁盘驱动器。

`who` 工具显示的用户名对应的设备名称是屏幕的文件。例如，当 `who` 显示设备名为 `pts/4` 时，屏幕的路径名为 `/dev/pts/4`。当你使用多个窗口时，每个窗口都有自己的设备名称。你也可以使用 `tty` 工具显示你执行命令的设备名称。尽管通常不需要这样做，但你可以像处理文本文件一样对其进行读写。写入它会在屏幕上显示内容；读取它会读取你在键盘上输入的内容。

> **注意** 本书中使用的“屏幕”指的是屏幕、终端模拟窗口或工作站。“屏幕”指的是你看到提示符和消息显示的设备。

## chsh: 更改你的登录 shell

**提示** 设置你账户的人决定了你首次登录系统或在 GUI 环境下打开终端模拟器窗口时将使用的 shell。登录后，你可以运行任何你喜欢的 shell。输入你想要使用的 shell 名称（`bash`、`tsh` 或其他）并按回车键（`RETURN`）；下一个提示符将是新 shell 的提示符。输入退出命令可以返回到上一个 shell。由于 shell 是嵌套的（一个运行在另一个之上），你将只能从原始 shell 注销。当你嵌套了多个 shell 时，请继续输入 `exit`（退出）命令，直到回到原始 shell。此时，你就可以注销系统了。

当你想要永久更改登录 shell 时，请使用 `chsh` 工具。首先输入命令 `chsh`。在提示符的响应中，输入用户名和想要使用的 shell 的绝对路径（`/bin/bash`、`/bin/tsch` 或另一个 shell 的路径）。当你在 GUI 环境下使用终端模拟器通过这种方式更改登录 shell 时，在注销系统并重新登录之前，终端模拟器窗口不会反映该变化。

## 键盘和屏幕作为标准输入和标准输出

当你首次登录时，shell 将你的命令的标准输出重定向到代表屏幕的设备文件。通过这种方式重定向输出会使其出现在你的屏幕上。shell 还将标准输入重定向来自同一个文件，因此你的命令将接收你在键盘上输入的任何内容作为输入。

`cat` 工具提供了一个键盘和屏幕分别作为标准输入和标准输出功能的良好示例。当你使用 `cat` 时，它会将一个文件复制到标准输出。由于 shell 将标准输出重定向到屏幕，`cat` 将文件显示在屏幕上。

```
$ cat
This is a line of text.
This is a line of text.
Cat keeps copying lines of text
Cat keeps copying lines of text
until you press CONTROL-D at the beginning
until you press CONTROL-D at the beginning
of a line.
of a line.
$
```

到此为止，`cat` 一直从你在命令行上指定的文件名（参数）获取输入。当你没有给 `cat` 提供参数时（即在输入命令后紧接着按回车键），`cat` 将从标准输入获取输入。因此，在没有参数的情况下，`cat` 逐行将标准输入复制到标准输出。

要查看 `cat` 如何工作，请在 shell 提示符处输入 `cat` 并按回车键。什么都没有发生。输入一行文本并按回车键。相同的行内容会出现在你输入的内容的下方。`cat` 正在工作，因为 shell 将 `cat` 的输入与键盘关联，并将 `cat` 的标准输出与屏幕关联；当你输入一行文本时，`cat` 将文本从标准输入（键盘）复制到标准输出（屏幕）。

`cat` 会一直复制文本，直到你在单独的一行中输入 `CONTROL-D`。发送 `CONTROL-D` 会向 `cat` 发送一个 EOF（文件结束）信号，指示它已到达标准输入的末尾，没有更多文本供其复制。然后 `cat` 将完成执行并将控制权还给 shell，shell 将显示提示符。

### 重定向

“重定向”（redirection）一词涵盖了你可以使用 shell 重定向命令标准输入来源和标准输出去向的各种方法。默认情况下，如前所述，shell 将命令的标准输入和标准输出与键盘和屏幕关联。你可以通过将输入或输出与代表键盘或屏幕的设备文件以外的命令或文件关联，使用 shell 重定向任何命令的标准输入或标准输出。本节演示了如何将输入和输出重定向到文本文件工具。

## 重定向标准输出

重定向输出符号（`>`）指示 shell 将命令的输出重定向到指定的文件而不是屏幕。重定向输出的命令行格式为：

```
command [arguments] > filename
```

其中 `command` 是任何可执行程序（如应用程序或工具），`arguments` 是可选参数，而 `filename` 是 shell 重定向输出的普通文件名称。

图示使用 `cat` 来演示输出重定向。在图中，标准输入来自键盘。命令行上的重定向输出符号导致 shell 将 `cat` 的标准输出与命令行指定的 `sample.txt` 文件关联。

在输入命令并输入如下所示的文本后，`sample.txt` 文件包含了你输入的文本。你可以使用带有 `sample.txt` 参数的 `cat` 来显示此文件。

```
$ cat > sample.txt
This text is being entered at the keyboard and
cat is copying it to a file.
Press CONTROL-D to indicate the
end of file.
CONTROL-D
$
```

### 重定向输出可能会破坏文件

**注意** 当你将输出重定向到文件时请务小心。如果文件已存在，shell 将覆盖它并破坏其内容。

上述示例显示了在不使用编辑器的情况下通过输入 `cat` 创建文件。其缺点是，当你输入一行并按回车键时，无法编辑文本。这种方法对于创建短文件非常有用。

```
$ cat stationery
2000 sheets letterhead ordered: 10/05
$ cat tape
1 box masking tape ordered: 14/05
5 boxes filament tape ordered: 28/05
$ cat pens
12 doz. black pens ordered: 10/05
```

```
$ cat stationery tape pens > supply_orders
$ cat supply_orders
2000 sheets letterhead ordered: 10/05
1 box masking tape ordered: 14/05
5 boxes filament tape ordered: 28/05
12 doz. black pens ordered: 10/05
$
```

上述示例展示了如何使用 `cat` 和重定向输出符号将多个文件合并（一个接一个——`cat` 工具名称的词源）到一个较大的文件中。前三个命令显示了 `stationery`、`tape` 和 `pens` 文件的内容。下一个命令显示了带有三个文件作为参数的 `cat`。当你调用它时传递多个文件名，`cat` 会逐个将文件复制到标准输出。在这种情况下，标准输出被重定向到文件 `supply_orders`。最后一个 `cat` 命令显示 `supply_orders` 包含了所有文件的内容。

## 重定向标准输入

就像重定向标准输出一样，你也可以重定向标准输入。重定向输入符号（`<`）指示 shell 将命令的输入来源改为指定的文件而不是键盘。

```
command [arguments] < filename
```

其中 `command` 是任何可执行程序（如应用程序或工具），`arguments` 是可选参数，`filename` 是 shell 重定向输入的源文件名称。

下例显示了 `cat` 的输入从 `supply_orders` 文件重定向，而标准输出指向屏幕。这种设置使用 `cat` 在屏幕上显示示例文件。系统会在普通文件的末尾自动发送一个 EOF（文件结束）信号。

```
$ cat < supply_orders
2000 sheets letterhead ordered: 10/05
1 box masking tape ordered: 14/05
5 boxes filament tape ordered: 28/05
12 doz. black pens ordered: 10/05
```

## 从文件或标准输入获取输入的工具

从文件重定向输入 `cat` 命令与将文件名作为参数提供 `cat` 命令具有相同的结果。`cat` 工具是这种方式运行的 Linux 工具类的一员。该类工具的其他成员包括 `lp`、`sort` 和 `grep`。这些工具首先检查命令行上使用的参数。如果你在命令行上包含一个文件名，实用程序将从你指定的文件获取输入。如果你没有指定文件名，实用程序将从标准输入获取输入。以这种方式运行的是工具或程序——而不是 shell 或操作系统。

## noclobber: 避免覆盖文件

shell 提供了一个名为 *noclobber*（禁止覆盖）的功能，它可以防止你无意中通过重定向覆盖已存在的文件。当你通过设置 `noclobber` 变量来启用此功能，并尝试将输出重定向到一个已存在的文件时，shell 会显示错误信息且不执行命令。以下示例设置了 `noclobber`，尝试将 `echo` 的输出重定向到一个已存在的文件，然后取消设置 `noclobber`：

```
$ set -o noclobber
$ echo "hi there" > tmp
bash: tmp: Cannot overwrite existing file
$ set +o noclobber
$ echo "hi there" > tmp
```

你可以通过在重定向输出的符号（`>`）之后加上管道符号（`|`）来覆盖 `noclobber`。

在下面的示例中，用户首先通过将输出重定向到 `date` 创建一个名为 `a` 的文件。下一个用户设置了 `noclobber` 变量并尝试再次将输出重定向到 `a`。shell 返回了错误信息。

```
$ date > a
$ set -o noclobber
$ date > a
bash: a: Cannot overwrite existing file
$ date >| a
```
