
```
Header Line#
@
Data Line #1
Data Line #2#
@
End of Data Lines#
@
$
sed -n '
>N
>s/^\n@//
>P
>D
> ' corruptData.txt
Header Line
Data Line #1
Data Line #2
End of Data Lines
$
```

该数据文件在某些行末尾被损坏，增加了#号，并在下一行添加了@符号。要修复此问题，使用 `sed` 将“Header Line#”行加载到模式空间，然后多行 `next (n)` 命令将第二行（@）加载到模式空间，并追加到第一行之后。替换命令（`s`）通过用空值替换非法数据（#\n@）来移除这些字符。接下来，打印命令（`p`）仅打印模式空间中现在已清理好的第一行。删除命令（`d`）将此第一行从空间移除，并返回脚本开头，此时下一个 `n` 命令将第三行文本（Data Line #1）读入模式空间，编辑循环继续。

## 保持空间

模式空间是 `sed` 编辑器在处理命令时用于存储被检查文本的主动缓冲区。然而，它并不是 `sed` 编辑器中用于存储文本的唯一空间。

`sed` 编辑器利用了另一个称为*保持空间*（hold space）的缓冲区。你可以使用保持空间在模式空间中处理其他行时，暂时存放文本行。与操作保持空间相关的五个命令在表 21.1 中展示。

### 表 21.1 `sed` 编辑器保持空间命令

| 命令 | 描述 |
| :--- | :--- |
| h | 将模式空间复制到保持空间 |
| H | 将模式空间追加到保持空间 |
| g | 将保持空间复制到模式空间 |
| G | 将保持空间追加到模式空间 |
| x | 交换模式空间和保持空间的内容 |

这些命令允许你将文本从模式空间复制到保持空间。这释放了模式空间以加载另一个字符串进行处理。

通常，在使用 `h` 或 `H` 命令将字符串移动到保持空间后，最终你会希望使用 `g`、`G` 或 `x` 命令将存储的字符串移回模式空间（否则，你一开始也不会关心保存它们）。

有了两个缓冲区，试图确定哪一行文本在哪个缓冲区中有时会变得令人困惑。下面是一个简短的示例，演示如何使用 `h` 和 `g` 命令在 `sed` 编辑器缓冲区之间来回移动数据：

```
$ cat data2.txt
Header Line
First Data Line
Second Data Line
End of Data Lines
$
$ sed -n '/First/ {
> h ; p ;
> n ; p ;
> g ; p ;}
> ' data2.txt
First Data Line
Second Data Line
First Data Line
$
```

让我们逐步查看前面的代码示例：

- 1. `sed` 脚本在地址中使用正则表达式来筛选包含单词 First 的行。
- 2. 当包含单词 First 的行出现时，`{}` 中的初始命令 `h` 将模式空间中的行复制到保持空间。此时，模式空间和保持空间拥有相同的数据。
- 3. 然后，`p` 命令打印模式空间的内容（First Data Line），它仍然是被复制到保持空间的那一行。
- 4. `n` 命令获取数据流中的下一行（Second Data Line）并将其放入模式空间。现在模式空间拥有与保持空间*不同*的数据。
- 5. `p` 命令打印模式空间的内容（Second Data Line）。
- 6. `g` 命令将保持空间的内容（First Data Line）放回模式空间，替换当前文本。模式空间和保持空间现在再次拥有相同的数据。
- 7. `p` 命令打印模式空间的当前内容（First Data Line）。

通过使用保持空间重新排列文本行，我们可以强制 First Data Line 在输出中出现在 Second Data Line 之后。如果我们只是去掉第一个 `p` 命令，就可以以相反顺序输出这两行：

```
$ sed -n '/First/ {
> h ;
> n ; p
> g ; p }
> '
 data2.txt
Second Data Line
First Data Line
$
```

这是某项有用功能的开端。你可以使用这种技术创建一个 `sed` 脚本，反转整个文本文件中的数据！然而，要做到这一点，你需要了解 `sed` 编辑器的否定功能，这也是下一节的主要内容。

## 否定命令

第 19 章表明，`sed` 编辑器将命令应用于数据流中的每一行文本，或者应用于由单个地址或地址范围特定指示的行。你还可以配置命令，使其不应用于数据流中的特定地址或地址范围。

感叹号（!）命令用于否定一个命令。这意味着在命令通常会被激活的情况下，它不会被执行。下面是一个演示此功能的示例：

```
$ sed -n '/Header/!p' data2.txt
First Data Line
Second Data Line
End of Data Lines
$
```

正常的 `p` 命令本应只打印 data2 文件中包含单词 Header 的行。通过添加感叹号，情况正好相反——除了包含单词 Header 的那一行外，文件中的所有行都会被打印。

在几种应用场景中使用感叹号非常有帮助。回想一下，本章前部的“导航 Next 命令”部分展示了一种情况，其中 `sed` 编辑器命令不会在数据流中的最后一行文本上操作，因为它后面没有行。你可以使用感叹点来修复该问题：

```
$ cat data4.txt
On Tuesday, the Linux System
Admin group meeting will be held.
All System Admins should attend.
$
$ sed 'N;
> s/System\nAdmin/DevOps\nEngineer/
> s/System Admin/DevOps Engineer/
> ' data4.txt
On Tuesday, the Linux DevOps
Engineer group meeting will be held.
All System Admins should attend.
$
$ sed '!IN;
> s/System\nAdmin/DevOps\nEngineer/
> s/System Admin/DevOps Engineer/
> ' data4.txt
On Tuesday, the Linux DevOps
Engineer group meeting will be held.
All DevOps Engineers should attend.
$
```

此示例展示了感叹号与 `N` 命令一起使用，以及美元符号（$）特殊地址。美元符号代表数据流中的最后一行文本，因此当 `sed` 编辑器到达最后一行时，它不会执行 `N` 命令。然而，对于其他所有行，它都会执行该命令。

使用这种技术，你可以反转数据流中文本行的顺序。要反转文本流中出现的行顺序（先显示最后一行，最后显示第一行），你需要使用保持空间进行一些巧妙的操作。

为了完成此任务，使用 `sed` 进行以下操作：

- 1. 将一行文本放入模式空间。
- 2. 将模式空间中的行复制到保持空间。
- 3. 将下一行文本放入模式空间。
- 4. 将保持空间追加到模式空间。
- 5. 将模式空间中的所有内容复制到保持空间。
- 6. 重复步骤 3 到 5，直到将所有行以相反顺序放入保持空间。
- 7. 检索行，并打印它们。

图 21-1 详细说明了这一过程。

![](img/a5025f22e05b92f409563a958cac7312_772_0.png)

### 图 21-1 使用保持空间反转文本文件顺序

使用此技术时，你不希望在处理过程中打印行。这意味着对 `sed` 使用 `-n` 命令行选项。接下来需要确定如何将保持空间文本追加到模式空间文本。这是通过使用 `g` 命令完成的。唯一的问题是，你不希望将保持空间追加到处理的第一行文本。这很容易通过使用感叹号命令来解决：

```
1!G
```

下一步是将新的模式空间（带有追加的反向行的文本行）复制到保持空间。这很简单；只需使用 `h` 命令。

当你已将整个数据流以相反顺序放入模式空间时，你只需打印结果。当你到达数据流中的最后一行时，你就知道整个数据流都在模式空间中。要打印结果，只需使用以下命令：

```
Sp
```

这些是我们创建行反转 `sed` 编辑器所需的组成部分

