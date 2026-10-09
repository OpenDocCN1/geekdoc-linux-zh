

请注意，shell 提示符紧随文件文本之后，位于同一行。虽然这并非主要问题，但它往往会掩盖多行文件的第一行。在某些系统或某些 shell 环境中，shell 提示符会包含你的用户 ID 和工作目录。如果在此处出现这种情况，那么执行 `cat tempfile1` 将会产生你在图 6-3 中看到的结果。

```
[userid dir1]$ cat tempfile1
This is tempfile1.[userid dir1]$ 
```

图 6-3 扩展 Shell 提示符位于 tempfile1 文本旁边

你可以看出，可能需要额外的一两秒时间来区分文件文本和 shell 提示符。使用 `<Enter>` 键消除这种小麻烦是一件轻而易举的事。请记住，`<Enter>` 会将光标移至下一行。

- 6. 创建第二个临时文件。
  - a. 输入 `cat > tempfile2`
  - b. 按下 `<Enter>` 以让系统响应上述命令行。
  - c. 输入：`This is tempfile2.`
  - d. 按下 `<Enter>` 将光标移至下一行。
  - e. 按下 `<Ctrl-D>`

此练习中的额外步骤是在按下 `<Ctrl-D>` 之前按下 `<Enter>`。

- 7. 现在你将使用 `cat` 读取 `tempfile2`。
  - a. 输入 `cat tempfile2`
  - b. 按下 `<Enter>`

你的屏幕将与图 6-4 相似。

```
[userid dir1]$ cat tempfile2
This is tempfile2.
 [userid dir1]$ 
```

图 6-4 Shell 提示符位于 tempfile2 文本下方一行

这样好多了。现在更容易区分 shell 提示符和我们试图读取的文本。如果我们能清晰地将此文本与上方的 shell 提示符和下方的 shell 提示符分离开来，那就更好了。我们可以通过连续两次按下 `<Enter>` 键来实现这一点。

- 8. 创建文件 `tempfile3`。
  - a. 输入 `cat > tempfile3`
  - b. 按下 `<Enter>` 以让系统响应上述命令行。
  - c. 按下 `<Enter>` 在文件开头创建一个空行。
  - d. 输入：`This is tempfile3`.
  - e. 按下 `<Enter>` 将光标移至下一行。
  - f. 按下 `<Enter>` 在文件末尾创建一个空行。
  - g. 按下 `<Ctrl-D>`

- 9. 读取 `tempfile3`。
  - a. 输入 `cat tempfile3`
  - b. 按下 `<Enter>`

你的屏幕将与图 6-5 相似。

![](img/cc8b9fd5970716027fba0d0a45c13900_102_0.png)

**图 6-5** `tempfile3` 的文本与 Shell 提示符清晰分离

你可以看到 `tempfile3` 的文本与我们扩展的 shell 提示符清晰分离。

在某些系统中，在你发出创建或保存文件的命令和系统实际将文件存储到磁盘之间可能存在延迟。虽然这通常不是你需要担心的事情，但毫无疑问，会有这样的时候：你创建了一个非常重要的文件，并希望确定该文件已存储在磁盘上。在那一刻，你将希望使用 `sync` 命令。

- 10. 使用 `sync` 确保文件写入磁盘。
  - a. 输入 `sync`
  - b. 按下 `<Enter>`
  - 无论是出于必要、习惯还是迷信，Linux 用户都养成了至少执行两次 `sync` 命令的习惯。
  - c. 输入 `sync`
  - d. 按下 `<Enter>`
  - 如果你在一台独立系统上工作，当你按下 `<Enter>` 时，你会看到硬盘指示灯闪烁。在多用户系统上，当你按下 `<Enter>` 时，可能看不到任何反应。

我们不会再使用这些临时文件了；我们可以删除它们。这将让我们有机会练习 `rm` 的一些选项。在 `dir1` 中有一些额外的文件会有帮助。我们将使用 `cp` 来实现这一点。

- 11. 创建三个新文件。
  - a. 输入 `cp tempfile1 tempfile4`
  - b. 按下 `<Enter>`
  - c. 输入 `cp tempfile1 tempfile5`
  - d. 按下 `<Enter>`
  - e. 输入 `cp tempfile1 tempfile6`
  - f. 按下 `<Enter>`
  - g. 输入 `ls`
  - h. 按下 `<Enter>`

你的屏幕应与图 6-6 相似。

```
$ ls
tempfile1 tempfile2 tempfile3 tempfile4
tempfile5 tempfile6
$ 
```

图 6-6 显示了六个临时文件

- 12. 删除 **tempfile1**。
  - a. 输入 `rm tempfile1`
  - b. 按下 `<Enter>`

接下来你将删除 **tempfile2**、**tempfile3** 和 **tempfile5**。你可以三次输入命令行 `rm tempfile2`，每次替换为相应的编号。诚然，这并不费力。但假设现在你的目录中有十个文件——或者二十个。突然，你面临着繁重的打字任务。你可以使用 `rm -i *` 有选择地删除文件。通配符 * 表示“所有”。因此，这条命令行实际上意味着：“删除所有文件，但让我逐个确认每个文件的删除。”

- 13. 使用 `rm -i *` 有选择地删除 **tempfile2**、**tempfile3** 和 **tempfile5**。
  - a. 输入 `rm -i *`
  - b. 按下 `<Enter>`

系统会做出类似 `rm: remove 'tempfile2'?` 的响应

  - c. 按下字母 “y” 进行确认。
  - d. 按下 `<Enter>`

系统会做出类似 `rm: remove 'tempfile3'?` 的响应

  - e. 按下字母 “y” 进行确认。
  - f. 按下 `<Enter>`

系统会做出类似 `rm: remove 'tempfile4'?` 的响应

  - g. 按下字母 “n” 以拒绝此删除操作。
  - h. 按下 `<Enter>`

系统会做出类似 `rm: remove 'tempfile5'?` 的响应

  - i. 按下字母 “y” 进行确认。
  - j. 按下 `<Enter>`

系统会做出类似 `rm: remove 'tempfile6'?` 的响应

  - k. 按下 `Ctrl-C` 以取消 `rm` 进程。

在步骤 k 中，你也可以输入字母 "n" 来拒绝删除 `tempfile6`。我们让你使用 `Ctrl-C` 只是为了提醒你，你可以使用 `Ctrl-C` 来取消许多正在进行的 Linux 进程。

剩下的是 `tempfile4` 和 `tempfile6`。你可以使用 `rm *` 将它们都删除。

- 14. 删除剩余的两个临时文件。
  - a. 输入 `rm *`
  - b. 按下 `Enter`

- 15. 一切都消失了吗？检查一下。
  - a. 输入 `ls`
  - b. 按下 `Enter`

你的屏幕应如图 6-7 所示。Linux 返回 shell 提示符，这意味着该目录为空。

```
$ ls
$ 
```

![](img/cc8b9fd5970716027fba0d0a45c13900_105_0.png)

随着前期准备工作就绪，我们将进一步创建六个短文件，我们将在后续练习中使用这些文件来探索你在本节中学到的一些内容。由于你的工作目录是 `dir1`，所有文件都将存储在此目录中。

我们希望你能扮演 Robert Anderson 的实习生角色。Robert 是 Diamond Office Supply 的 NASR（北阿拉斯加销售区域）经理。在这种角色下，你将帮助 Robert 创建和管理一些库存文件。

在你将创建的第一个文件 `supply1` 中，单词 "markers"、"pencils" 和 "pens" 后面都有句号。你将创建的其他“supply”文件在任何条目后都不会有句号。这些句号的目的是为本书 *《vi 教程》* 部分的 "Try It Live!"（实时尝试）部分使用此文件做准备。请确保添加这些句号。没有它们，后续使用此文件的活动将无法正常工作。

这提醒我们，在基于字符的用户界面中，你输入的每个字符都很重要。请仔细输入。

如果你意识到在按下 **<Ctrl-D>** 创建以下练习中的某个文件后犯了一个错误，请查看练习 36 之后的提示，以获取如何纠正错误的建议。

- 16. 创建文件 **supply1**。确保输入句号。
  - a. 输入 `cat > supply1`
  - b. 按下 **<Enter>**
  - c. 按下 **<Enter>** 在文件顶部创建一个空行。
  - d. 输入 `writing -- markers.`
  - e. 按下 **<Enter>** 将光标移至下一行。
  - f. 输入 `writing -- pencils.`
  - g. 按下 **<Enter>** 将光标移至下一行。
  - h. 输入 `writing -- pens.`
  - i. 按下 **<Enter>** 将光标移至下一行。
  - j. 按下 **<Enter>** 将光标移至下一行并在文件底部创建一个空行。
  - k. 按下 **<Ctrl-D>** 创建文件。

- 17. 创建文件 **supply3**。
  - a. 输入 `cat > supply3`
  - b. 按下 **<Enter>**
  - c. 按下 **<Enter>** 在文件顶部创建一个空行。
  - d. 输入 `correction fluid`
  - e. 按下 **<Enter>** 将光标移至下一行。
  - f. 输入 `correction pens`
  - g. 按下 **<Enter>** 将光标移至下一行。
  - h. 输入 `correction tape`
  - i. 按下 **<Enter>**
  - j. 按下 **<Enter>** 将光标移至下一行并在文件底部创建一个空行。
  - k. 按下 **<Ctrl-D>** 创建文件。

