

31. 重做**查找**练习，使用方括号在搜索中包含大小写“s”。

- a. 输入 `find . -name '[Ss]upply*' -print`
- b. 按 <Enter>

你的屏幕应如图 6-15 所示。

```
$ find . -name '[Ss]upply*' -print
./supply10
./supply3
./supply7
./supply6
./supply9
./Supply1
```

图 6-15 在 find 的文件名中使用方括号

我们在练习 24 中使用了方括号来移动一组文件。从这些结果中可以看出，方括号可以和各种命令一起使用。

32. 将 **Supply1** 改回为 **supply1**。

- a. 输入 `mv Supply1 supply1`
- b. 按 <Enter>

旁白部分 2，使用 `?` 通配符：

33. 在这个练习中，你将使用 `?` 通配符列出 **catalog** 中的文件。

- a. 输入 `ls supply?`
- b. 按 <Enter>

你的屏幕将类似于图 6-16。

```
$ ls supply?
supply1 supply3 supply6 supply7 supply9
$
```

图 6-16 使用带 ? 通配符的 ls

请记住，`?` 通配符意味着“恰好一个字符”。语法 `supply?` 的意思是“所有以字符 'supply' 开头且后面紧跟一个且仅一个字符的文件”。文件 `supp.ly` 未出现在图 6-16 中，因为 `supply` 后面跟随的是两个字符。

### 旁白部分 3

在继续之前，你应该通过备份来保护你的工作。正如我们在 CBT 课程中指出的那样，`tar` 和 `cpio` 是用于备份文件的标准 Linux 实用工具。这两个实用工具的使用准则因系统而异。

其他备份选项包括某种外部设备，例如软盘、磁带、ZIP 或 CD-RW 驱动器。我们必须假设这些设备都没有可供你使用，因此你将为此目的在你的账户中创建一个子目录。

34. 创建一个名为 **backup** 的目录。（请记住，你的工作目录是 *catalog*，位于 *practice* 的下一级。）
- a. 输入 `mkdir ../backup`
- b. 按 <Enter>

这个新的子目录 **backup** 是 *practice* 的子目录——而不是 *catalog* 的子目录。

让我们逐步解析步骤 a 中的语法。

你的工作目录是 *catalog*。双点 `..` 指的是父目录 *practice*。斜杠是必需的，它告诉系统你正在创建要存储在父目录中的内容。你本可以先切换到目录 *practice* 然后创建该目录。但那会多出一个步骤。

35. 将你创建的文件复制到这个安全港湾 **backup**。
- a. 输入 `cp * ../backup`
- b. 按 <Enter>

此示例中的语法含义如下：“将一切（`*`）复制（`cp`）到目录 `../backup`，该目录是我的（*catalog*）父目录（*practice*）的一个子目录。”（请记住，父目录由简写双点表示。）

我们的旁白部分到此结束。

现在，你已经把 Robert 的所有供应文件集中在一个地方并进行了备份，他要求你查找文件中的特定信息。例如，哪个文件包含关于文件的信息？文件夹？磁带？为此，你将使用 **grep**，它代表“**g**lobally search for a regular expression and **p**rint it”（全局搜索正则表达式并**p**rint it/打印它）。

36. 哪些文件包含关于笔的信息？
- a. 输入 `grep pens *`
- b. 按 <Enter>

**grep** 命令行需要两个参数：(1) 要搜索的文本和 (2) 要搜索的文件。星号意味着“所有文件”。

你的搜索结果应类似于图 6-17。

```
$ grep pens *
supply1:writing -- pens.
supply3:correction pens
$
```

![](img/cc8b9fd5970716027fba0d0a45c13900_116_0.png)

如果你的结果与你在图 6-17 中看到的不匹配，也许你的输入没有你预期的那么仔细。如果图 6-17 中列出的某个文件未出现在你的屏幕上，请使用 **cat** 读取该文件。如果发现错误，请使用 **cat > filename** 重新创建该文件。（你将用文件的实际名称替换 **filename**。）

在某些 shell 中，当你输入 **cat > filename** 时，如果文件名已存在，你会收到错误信息，类似于：**cat > filename: file exists**。系统不会让你覆盖已存在的文件。在这种情况下，你必须先用 **rm** 删除该文件，然后再重新创建它。

37. 哪些文件包含关于特殊物品的信息？
- a. 输入 `grep specialty *`
- b. 按 <Enter>

你的搜索结果应类似于图 6-18。

```
$ grep specialty *
supply6:staplers -- specialty
supply7:tape -- specialty
supply9:folders -- specialty file
```

图 6-18 **grep** 搜索 “specialty”

38. 哪些文件包含关于 Post-It® 便签的信息？
- a. 输入 `grep post-it *`（是的，小写。）
- b. 按 <Enter>

你的屏幕将类似于图 6-19。

```
$ grep post-it *
$
```

图 6-19 **grep post-it \*** 的结果

系统只返回 shell 提示符，这意味着 **grep** 未在任何文件中找到目标文本。但这是预期之中的：Linux 区分大小写，而你在创建该特定文件时使用的是“Post-It”——大写的“P”和大写的“I”。你可以通过在命令行中添加 -i 开关来告诉 **grep** 忽略大小写。

39. 使用 **grep -i** 搜索 “Post-It”。
- a. 输入 `grep -i post-it *`
- b. 按 <Enter>

你的屏幕将类似于图 6-20。

```
$ grep post-it -i *
supply10:Post-It -- pads
supply10:Post-It -- pop-up
supply10:Post-It -- printed
$
```

图 6-20 不区分大小写的 grep 搜索

40. Robert 要求你在 Post-It 文件 supply10 中追加一条注释，提醒他在 2 月 27 日重新订购。你将使用 cat 配合双重重定向符号 >>。
- a. 输入 `cat >> supply10`
- b. 按 <Enter>
- c. 输入 `Reorder 2/27`
- d. 按 <Enter> 将光标移至下一行。
- e. 按 <Enter> 在新文本下方添加一个空行。
- f. 按 <Ctrl-D>

41. 现在查看 supply10 的新版本。
- a. 输入 `cat supply10`
- b. 按 <Enter>

你的屏幕应类似于图 6-21。

```
$ cat supply10
Post-It notes -- pads
Post-It notes -- pop-up
Post-It notes -- printed
Reorder 2/27
$
```

图 6-21 添加了追加文本的 supply10

你向 Robert 建议，处理一个稍大一点的文件比处理多个小文件更有效率。Robert 同意了。

42. 将六个供应文件合并为一个。
- a. 输入 `cat supply1 supply3 supply6 supply7 supply9 supply10 > supply`

命令行可能会跨越两行。Linux 可以解释跨越多行屏幕的命令行。

- b. 按 <Enter>

现在读取新文件。

- c. 输入 `cat supply`
- d. 按 <Enter>

下一个合乎逻辑的步骤可能是打印该文件。为此，你会使用 lpr——例如，`lpr supply`。但由于关于打印机使用的准则因系统而异，我们无法在此处包含打印练习。请咨询你的讲师或系统管理员了解有关你系统上打印机使用的信息。

对于最后一组练习，你将是——而不是 Robert 的实习生。要完成这一系列练习，你需要与另一名学生、朋友或同事合作。

你将创建指向另一个用户账户中文本文件的链接。然后你将读取该文本文件。这将要求你能够列出该账户中的目录，并且知道哪些文件是文本文件。

为了演示，我们将假设另一个用户的 `userid` 是 sam4。你的 `userid` 是 ron sm。

43. 列出 sam4 的主账户。
- a. 输入 `ls -l /home/sam4`
- b. 按 <Enter>

你的屏幕将类似于图 6-22。

```
$ ls -l /home/sam4
drwxr-xr- 1 sam4 users 1024.. accounts
drwxr-xr- 1 sam4 users 1024.. practice
drwxr-xr- 1 sam4 users 1024.. webstuff
$
```

![](img/cc8b9fd5970716027fba0d0a45c13900_120_0.png)

在某些系统中，主账户可能位于 **/home** 以外的某个目录中。例如，在你刚刚完成的链接练习中，你可能需要输入 **/accounts/sam4** 或 **/users/sam4** 以反映你系统上正确的用户目录。

我们目前的关注点是文件模式，由图 6-22 中的这些字符表示：**rwxr-xr-**。我们在 CBT 课程的前一个模块 *Linux Directories*（Linux 目录）中提供了文件模式的概述，并将在名为 *Security*（安全）的模块中详细讲解文件模式。

就我们目前的目的而言，我们要指出，当你创建一个文件的链接时，你正在创建指向*位于*某个目录*内*的文件*的*链接。如果你要能够创建链接*并*读取文件，那么文件和目录都需要特定的权限。我们将向你展示权限必须是什么，以及在必要时如何更改它们。但对于文件模式和权限的详细解释，我们将参考 *Linux Made Easy CBT* 中的 *Security* 模块以及本指南中相应的安全章节。

