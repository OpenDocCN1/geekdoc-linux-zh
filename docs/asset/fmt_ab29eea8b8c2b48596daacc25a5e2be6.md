
```
#!/bin/bash
echo Enter a filename to process:
read THEFILE
echo The number of lines in $THEFILE:
wc -l $THEFILE
echo The number of words in $THEFILE:
echo -w $THEFILE
echo End of processing for $THEFILE
```

此脚本使用了名为`变量`（variable）的编程概念。变量是一个内存位置，程序可以在其中存储完成任务所需的值。通常情况下，通过向你选择的变量名赋值来定义一个变量。例如，在脚本中包含此行定义了一个新变量 `MYFILE`，并为其赋值了值 `index.html`。

```
MYFILE="index.html"
```

定义变量的另一种方法是使用 `read` 命令后跟一个变量名。该命令会导致脚本暂停并等待键盘输入。你在键盘上输入的文本被赋值为 `read` 命令中给变量的值。你可以在之前的脚本中看到这个示例，其中第三行包含 `read THEFILE`。该命令会导致脚本暂停，等待输入。运行脚本的用户输入的任何数据都会被赋值给名为 `THEFILE` 的变量的值。

一旦使用上述两种方法之一（直接赋值或使用 `read` 命令）为变量赋值后，脚本就可以在任何其他命令中使用该变量。在刚才提到的示例脚本中，脚本在执行 `wc` 命令时引用了变量 `THEFILE`。

如果上述脚本存储在名为 `filesize` 的文件中，任何对该文件具有执行权限的用户可以使用此命令启动脚本：

`./filesize`

`filesize` 脚本的输出显示在此。脚本在显示此输出的第一行后会暂停，以便用户输入文件名。显示的显示名（report.txt）将由运行脚本的用户输入。

```
Enter a filename to process:
report.txt
The number of lines in report.txt is:
453
The number of words in report.txt is:
3215
End of processing for report.txt
```

虽然 `read` 命令对于收集用户输入很有用，但你应该确保你的脚本能够测试用户输入数值的有效性。例如，如果运行 `filesize` 脚本的用户输入了一个系统中不存在的文件名，脚本中的其他命令（此例中的 `wc` 命令）将产生错误信息。在本章的稍后部分，你将学习如何创建测试用户输入值的脚本。

## 第 12 章 创建脚本和自动化过程

由于脚本使用标准的 Linux 命令将信息写入屏幕，因此它们也可以使用 Linux 重定向操作符来更改命令的信息流。正如你在第 7 章中学习的那样，你可以使用重定向操作符来改变对任何命令的输入和标准输出的处理方式。例如，假设你使用以下命令启动 `filesize` 脚本：

```
./filesize > /tmp/output
```

由于 `>` 重定向操作符的作用，通常情况下写入屏幕的所有数据将改为写入文件 `/tmp/output` 中。当你使用以下命令查看 `/tmp/output` 文件的内容时，你看到的和你运行不带重定向操作符的 `filesize` 命令时在屏幕上看到的完全相同。

```
cat /tmp/output
```

在运行任何 shell 脚本时，可以使用任何 Linux 重定向操作符（`<`, `>`, `|`）。通过使用这些操作符，你可以像处理任何普通 Linux 命令一样处理 shell 脚本，使用管道将脚本与其他脚本连接等。你将在本章稍后部分看到重定向操作符的其他示例。

## 在脚本中使用变量

上一节中显示的 `filesize` 脚本使用变量来存储用户输入的信息。shell 脚本中使用的变量有时被称为 `shell 变量`（shell variable）。因此，shell 变量是在 shell 脚本内部使用的用于存储脚本所需信息的变量。你可以以相同的方式处理 shell 变量和环境变量（你在之前的章节中学习过环境变量），尽管 shell 变量通常是由编写新 shell 脚本的人定义的，而环境变量则是由 Linux 操作系统脚本或运行在 Linux 上的程序预定义的。

当你编写 shell 脚本时，你可能会引用许多变量（你通过在 shell 脚本中进行赋值来定义它们）和环境变量（shell 在执行 shell 脚本之前通过为它们赋值来定义它们）。例如，你脚本中的某个命令可能需要将文件复制到运行脚本的用户家目录。为了实现这一点，你可以引用 `HOME` 环境变量。以下示例将 `report.txt` 文件复制到用户的家目录：

```
cp /tmp/report.txt $HOME
```

如果你没有使用 `HOME` 环境变量，而是使用脚本中的命令，但这种类型的命令只有在 `nwells` 运行脚本时才有效。

```
cp /tmp/report.txt /home/nwells/
```

通过使用 `HOME` 环境变量，你可以确保脚本对任何启动它的用户都有效。作为系统管理员，你使用此类技术创建尽可能灵活的 shell 脚本。这允许不同的系统管理员和其他用户安全地使用脚本。然而，并非所有用户都能执行每个脚本。某些脚本访问只有 root 用户才能访问系统部分。如果另一个用户运行此类脚本，就会出错。

shell 脚本经常使用称为`位置变量`（positional variables）的特殊变量。位置变量并不是在脚本内部赋值，而是根据用户在命令行中包含的信息（连同命令行）来获取值。

### 编写 Shell 脚本

shell 脚本经常使用称为`位置变量`的特殊变量。位置变量并不是在脚本内部赋值，而是根据用户在命令行中包含的信息（连同命令行）来获取值。

正如你可能猜的那样，“位置变量”一词是指命令行上项的位置决定了它们被赋值的名称。

当你处理位置变量时，了解用户在命令行中包含了多少项通常非常有帮助。例如，你可能想在脚本继续执行之前，包含命令来验证命令行中包含的项目数量。每当你执行脚本时，shell 都会定义一个特殊变量 `$#`，包含命令行中项的数量。稍后你将学习如何让脚本测试 `$#` 变量的值，以确定用户在命令行提供了多少项。例如，假设创建了以下脚本来输出命令行输入的几个文件名的信息：

```
#!/bin/bash
echo The script you are running $0
echo The number of parameters you provided $$
echo The number of lines in file $1 is:
wc -l $1
echo The number of lines in file $2 is:
wc -l $2
echo The number of lines in file $3 is:
wc -l $3
echo The number of lines in file $4 is:
wc -l $4
```

如果上述脚本存储在名为 `info` 的文件中，你可以这样启动它，命令行包含四个数据文件名：

`./info data1 data2 data3 data4`

shell 将脚本名称（命令行上的第一个项）分配给位置变量 `$0`。shell 还将命令行上的文件名分别分配给位置变量 `$1`、`$2`、`$3` 和 `$4`。最后，由于执行此脚本的命令行除了脚本名称外包含四项，shell 将值 `4` 分配给变量 `$#`（你在脚本第三行看到的变量）。因此，当运行此脚本时执行的命令如下：

取决于 `myreport` 的大小，脚本的输出可能如下所示：

The number of lines in myreport is:

452

The number of words in myreport is:

3419

End of processing for myreport

```
echo The script you are running is info
echo The number of parameters you provided to process is 4
echo The number of lines in file data1:
wc -l data1
echo The number of lines in file data2 is:
wc -l data2
echo The number of lines in file data3 is:
wc -l data3
echo The number of lines in file data4 is:
wc -l data4
```

脚本的输出可能如下（取决于数据文件的大小）：

The script you are running is info

The number of parameters you provided to process is 4

The number of lines in file data1 is:

123
