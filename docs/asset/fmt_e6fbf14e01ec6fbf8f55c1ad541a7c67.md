
搞定！这正是你所希望，对吧？现在文件已经按第二列的数字排序了。`sort` 有许多选项供你通过 `man` 页面自行探索，但你应该看到它是如何用于排序存储在不同格式中的各种数据的。

## 切分文件：`split`

假设你需要给一个朋友发送一个巨大的文件，但他或她的邮件系统不支持按你想要的方式接收消息。是时候写一个特殊的分割工具了吗？不用；它已经为你做好了。`split` 命令可以根据文件的行数或字节数将文件切割成你喜欢的长度分段。要使用 `split`

## 第 9 课

- 1. 选择你的输入文件。在本例中，我使用的是 `sort` 命令中的 `kiwi.txt`。
- 2. 确定你想在每个输出文件中存储的行数。你将使用 `-l <行数>` 作为 `sort` 命令的选项来指定。如果你喜欢使用 K 或 MB 的数量，可以使用带有 `k` 或 `m` 的 `-b` 选项。例如，`-l 3` 将文件分成每个段三行的部分。使用 `-b 10k` 则返回大小为 10K 的段。最后，`-b 10m` 创建 10MB 的段。
- 3. 为结果选择一个基础输出文件名。
- 4. 使用语法 `split <segmentoptions> <inputfile> <outputfile>` 调用 `sort`。

例如

```
>split -l 3 kiwi.txt kiwisplit
>more kiwisplit*
```

```
::::::::::::
kiwisplitaa
::::::::::::
Joan 92
Will 78
John 21
::::::::::::
kiwisplitab
::::::::::::
Kim 99
Kama 05
Jack 07
```

上一个示例中的 `kiwi.txt` 文件已经通过了 `split`，并分为两个每个三行的文件：`kiwisplitaa` 和 `kiwisplitab`。我使用 `more` 命令显示了文件内容，因为 `split` 不提供完成后的反馈。

在你的文件被分成合理的大小后，你可以将它们传输到讨厌的邮件服务器或你想去的任何其他地方。这只是另一个内置工具的例子，它会在你最意想不到的时候派上用场。

要重新组合文件，请这样使用 `cat` 命令：`cat <filename>* > <fullfile>`。这将提取所有基础名为 `filename` 的文件并将它们重新拼接到 `fullfile` 中。

> 处理输出文件 最好是将输出文件命名为如 `complete.file` 这样的名称——与 `<basename>` 完全不同，然后将它们移动到目的地或最终文件名。这避免了在那些你希望最终文件名只是 `<basename>` 的情况下可能产生的混淆。

## 差异与补丁：`diff` `patch`

你可能习惯于创建文档并发送修订版本。遗憾的是，大多数时候，当只有这里几个单词发生了变化时，你可能必须发送新文件的副本。在 Linux 社区中，有大量的信息交换，源代码不断地来回。人们并不总是发送完整文件，而是依靠 `diff` 和 `patch` 命令仅传输文件之间发生任何信息。

### 使用 `diff`

`diff` 函数接受两个文件，一个原始模板文件和一个更新后的文件，并生成一个输出文件，该文件包含足够的信息，仅需补丁文件和模板文件即可重建更新后的文件。假设我有原始文件 `templatefile.txt`，其内容如下：

Now is the time for all good kiwis to come to the aid of puppies.

我已将此文件分给了我的所有同事。（这只是一个例子，朋友们！）然而几天后，我将我的文件更新为名为 `updatedfile.txt` 的新文件，如下所示：

Now is the time for all good and bad kiwis to come to the aid of puppies and children.

与其向所有人重新发布新文件 `updatedfile.txt`，我可以创建一个包含原始文件和新文件之间所有更改的补丁。要做到这一点，我使用带有以下语法的 `diff` 命令：`diff <template file> <updated file> > <patch file>`。补丁文件可以是你喜欢的文件名。

> 重定向输出 此示例中独立的 `>` 用于将输出重定向到特定的文件，由你命名该文件。你将在第 12 课“输入与输出”中学习更多内容。

例如

```
>diff templatefile.txt updatedfile.txt > patchfile.txt
```

`diff` 会产生输出，如果你对补丁包含的内容感兴趣，可以使用 `cat` 查看。`diff` 也适用于你想知道两个文件是否相同的时候。

### 使用 `patch`

现在，`patch` 程序派上用场。你通过提供要补丁的文件，后面跟上补丁文件名来调用它。

例如

```
>patch templatefile.txt patchfile.txt
```

这就是全部。如果你查看了补丁文件，可能会发现它和 `updatedfile.txt` 大小相同，你可以通过 `cat` 来验证这一点。

```
>cat templatefile.txt
```
