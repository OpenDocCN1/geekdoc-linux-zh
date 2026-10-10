
您指定的。但其优势在于，如果您处于 C shell 环境中，它还会检查 `.cshrc` 文件（如果存在）中的别名。其语法如下（参见示例 8.9）：

```
$ which commandname<Enter>
```

### 示例 8.9 which

我们无畏的桑丘继续对 `grep` 命令进行初步调查，尝试使用 `which`。这将至少向他展示可执行文件 `grep` 的一个位置。他输入以下内容：

```
$ which find<Enter>
/bin/grep
```

### whereis

`whereis` 命令与 `whatis` 略有不同。您可以使用 `whereis` 查找命令、命令源代码和手册页。此命令搜索一个标准内置目录列表（包括 `/bin`、`/etc`、`/usr/bin` 和 `/usr/local/bin` 等），以查找并打印指定命令名称的所有匹配项。然而，`whereis` 不会搜索您自己的搜索路径（即，如您的 `PATH` 变量中定义的那样），因此，如果您的个人 shell 脚本位于您的本地系统目录或您自己的 `$HOME/bin` 目录中（假设您已创建了该目录），它可能无法找到它们。其语法为

```
$ whereis commandname<Enter>
```

我们在示例 8.9 中使用的方式，`whereis` 命令相比于您在信息源中找到的语法是简化的。它们还会告诉您可以指定要查找的文件类型、查找位置等。因此，您可以看出 `whereis` 并不像 `whatis` 那么简单。一如既往，请参阅您的信息源以获取更多细节。参见示例 8.10。

### 示例 8.10 whereis

桑丘通过使用 `whereis` 查找 `grep` 的可执行文件及其手册页，完成了他对 `grep` 的调查：

```
$ whereis grep<Enter>
grep: /bin/grep /usr/share/man/man1/grep.1.gz
```

`whereis` 也证实了 `which` 搜索的结果。桑丘正确地认识到只有一个可执行的 `grep`，它既被普通用户使用，也被 root 用户使用。

## 定位文件内的数据：grep 命令

您可以单独使用 `grep`（全局正则表达式解析）命令，也可以与其他命令一起使用。我们在第 7 章“Shell 基础”中提到过这个命令，当时讨论了用作其他命令过滤器的命令。`grep` 基本使用的语法看起来与任何命令的语法非常相似：

```
$ grep [选项] 正则表达式 [文件名1 文件名2 ... 文件名N]
<Enter>
```

对于 `grep` 与其他命令配合使用的场合，还有另一种 `grep` 语法。该语法如下：

```
$ 命令名 [选项] | grep [选项] | 命令名 [选项]<Enter>
```

或者

```
$ 命令名 [选项] | grep [选项]<Enter>
> | 命令名 [选项]<Enter>
```

我们之前展示过这种串联命令，通常是这样输入的：分两行。当您输入三个或更多命令时，您可能已经决定将它们拆分（在主提示符处输入命令结构的一部分，在次提示符处输入其余部分）。

通常，`grep` 命令在指定文件中搜索正则表达式、指定的文本模式、逻辑结构和/或元字符（代表特殊含义的模式或通配符符号）。如果找到此类表达式，`grep` 会从文件中获取一个或多个切片（包含正则表达式的文本文件中的每一行都是一个切片），并将这些切片写入 stdout。

`grep` 使用的元字符符号可能与 shell 使用的某些符号相同，但对 `grep` 而言可能意味着不同的含义。因此，有时某些符号应该用单引号（首选）或双引号包围。与此同时，`grep` 命令的元字符将在下一节中讨论。

您通常使用 `grep` 指定文件名。如果您不指定，`grep` 将在 stdin 中搜索其输入。修改 stdin 以适应这种情况是可以接受的（即，您可以使用第 7 章中的技术为 `grep` 指定要搜索的文件或目录）。

如果您没有修改 stdin，shell 会将您带到屏幕上的下一行，并留给您一个闪烁的光标（甚至没有提示符），等待您输入。请记住，对于 `grep` 来说，终端是默认的 stdin。如果您执行 `grep` 并希望这样做，那很好。当您输入一个与指定搜索文本模式匹配的文本模式时，`grep` 会将该文本模式回显到屏幕上。要停止回显，请按 Ctrl-C。该过程终止并返回提示符。

假设您输入了一个搜索文本模式和单个要搜索的文件名，并且 `grep` 在该文件中找到了您的文本模式一次或多次。它将那些行的副本返回到您的屏幕上，但不显示与文本模式不匹配的任何行。然而，如果您输入了多个文件名进行搜索，并且 `grep` 在多个文件中找到了您的文本模式，它会返回它找到的每一行，并在每一行前面加上找到该文本模式的文件名。（示例 8.11 说明了这种类型的响应。）

### 示例 8.11 grep

如果您回顾以下文件，示例 8.11 和 8.12 将更有意义，这些文件是为示例 7.1、7.2 和 7.3 创建的：

- 文件名：/home/gutieju/admin/phone#s/RFL_Tel1
- 文件名：/home/gutieju/admin/phone#s/RFL_Tel2
- 文件名：/home/gutieju/admin/phone#s/RFL_Tel3

此外，如果您事先花时间使用 vi 等文本编辑器创建以下额外文件，这些示例将更有意义：

- 文件名：/home/gutieju/admin/Feed

```
Roxinante, Dapple -

hay (alfalfa, timothy, etc) .8
oats .3
chop .2
vegetables (fresh) .65
vegetables (old, rotten) .6
fruits .4
supplements .1
nachos/salsa .15

Dogs, Cats -

dog food .5
dog treats .55
cat food .7
catnip .75
```

**文件名：** /home/gutieju/admin/lnnfile

- file<空格键>Inn No. 4
- file<空格键>Inn No. 7
- file<Tab>Inn No. 8
- file<Tab>Inn No. 1
- file<空格键>Inn No. 8

> **注意** 在 *lnnfile* 文件中，`<空格键>` 表示您应该在单词 *file* 的结尾（例如）和短语 *Inn No. x* 的开头之间按下空格键。同样，`<Tab>` 表示您应该在单词 *file* 的结尾（例如）和短语 *Inn No. x* 的开头之间按下 Tab 键。此外，实际上有两个 *Inn No. 8* 条目；没有拼写错误。

Lady Dulciea 很好奇有多少员工在拉曼查（La Mancha）和埃尔托博索（El Toboso）附近安家。她让 Juana 检查她的 *RFL_Tel\** 电话号码文件。Juana 知道只有两个文件（即 *RFL_Tel1* 和 *RFL_Tel2*）包含此类信息。她使用带有地区区号 **958** 的 **grep** 如下：

```
$ grep 958 RFL_Tel1 RFL_Tel2<Enter>
RFL_Tel1: La Mancha Field Office (Noble Deeds) – +34 958 55 34 56
RFL_Tel1: El Toboso Field Office (Executive Suites) – +34 958 55 56 78
RFL_Tel2: Casa: +34 958 55 19 01
RFL_Tel2: Casa: +34 958 55 01 03
RFL_Tel2: Casa: +34 958 55 13 15
RFL_Tel2: Casa: +34 958 55 13 15
RFL_Tel2: Casa: +34 958 55 15 17
RFL_Tel2: Casa: +34 958 55 17 19
```

### 示例 8.12 使用 grep 提取数据

Juana 记得她为 Rueful Figures, Inc. 编译了三份电话列表，并将它们存储在 phone\#s 子目录中。以下是她如何检查该数字：

```
$ cd<br>
$ cd admin/phone\#<br>
$ ls | grep "R" | wc -l<br>
3
```

在示例 8.12 中的命令中，Juana 首先移动到她的家目录，然后更改目录到她的 /home/admin/phone\#s 子目录。然后，她列出了该子目录中的所有文件，grep 了所有文件名以 R 开头的文件，然后计算该 grep 命令输出中的行数。因为 grep 找到了三个文件 RFI\_Tel1、RFI\_Tel2 和 RFI\_Tel3（参见示例 8.11 中的文件列表作为参考），其输出将有三行。wc 命令计算那些 grep 输出行，并向终端屏幕报告 3，这是默认的 stdout（标准输出设备）。grep 命令最常以此功能使用，从 stdin 中提取某些指定信息以供进一步处理。

在下一节中，我们将检查 grep 在其正则表达式中使用的元字符。

诚然，Juana 本可以只是对同一目录执行 ls 列表并统计文件名以 R 开头的文件数量。然而，如果她不得不通过几个子目录检查长长的文件列表，那么简单的列表将是不够的。

## grep：带有元字符的正则表达式

再看一下示例 8.11。您也可以通过输入以下内容获得相同的结果：

```
$ grep 958 RFI*
```

对于 Juana 的文件结构，星号通配符将指向这三个文件。但是，如果她有超过三个以 RFI 开头的文件，而她只想检查那三个文件怎么办？她如何限制搜索范围？除了明确列出这三个文件外，您能想到任何其他

