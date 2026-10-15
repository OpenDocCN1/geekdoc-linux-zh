

- **Mail** 用于 elm 邮件阅读器的必需存储位置
- *arc* 一个存放我不常需要但又不想删除的物品压缩版本的存放处
- *junk* 不适合放在其他地方的东西

其他子目录会根据正在进行项目的不同而增减。例如，我目前在 docs 目录中有个 UNIXanswers 目录。当本书完成后，整个目录将被压缩成一个单一文件并存入 arc 目录。

那么实际上你的主目录根级会放什么呢？尽可能少的绝对最小值。所有不必放在主目录中的东西都应放在子目录中。UNIX 会运行得更快，因为它非常讨厌目录中文件太多。并且你会在寻找文件时花费更少的时间。

## How can I keep my home directory clean?

基本上，你主目录中唯一的应该存在的文件是控制启动、关闭和环境的“点”文件。像 **.profile**、** .kshrc**、** .login**、** .cshrc**、** .logout**、** .exrc** 和 **.xsession** 这样的文件。我们将在第 5 章中更详细地检查这些文件中的大多数，因为它们对于自动化和控制你的设置至关重要。由于它们以点开头，这些文件通常不可见，因为它们对简单的 ls 命令是隐藏的。

## FINDING LOST FILES

## How can I find a file I’ve changed recently?

试试 `ls -t`。这个小技巧本身就能找到你正在寻找的 85% 的文件。`-t`（据推测代表 time）会按文件最后更改时间排序列出文件，最新的在前。加上 `-u` 开关，排序将按文件最后访问时间，无论是否被更改。将此与 `more` 结合使用以

防止列表从屏幕上滚动出去，你就拥有了一个有用的别名：

```
alias lt="ls -laFtu | more"
```

这将为你提供当前目录中最近被访问过的所有文件的长列表。

## Can I find a file when I know what kind it is but not where it is?

现在是时候请出重量级选手——UNIX find 命令了。这个强大的实用程序将搜索你的整个文件系统，查找匹配一组标准的文件或文件，或整个文件系统的任何子集。此命令语法为

```
find <pathname-list> <operator>
```

其中 pathname-list 可以是一个或多个目录及其子目录，而 operator 可以是以下任意一个：

- -name <filename pattern>
- -perm <file mode>
- -type <filetype>
- -user <username>
- -size <# blocks> (+# blocks means larger than)
- -atime <#days> (accessed time)
- -mtime <#days> (modified time)
- -ctime <#days> (changed time)
- -newer <file> (newer than the designated file)

在这些选项中，最有用的可能是 "-name" 选项。它会接受通配符并执行通常的模式匹配，因此可以相当灵活。

例如，你知道你有一个文件是上个月用于月度进度报告的，你想把它用作模板，但找不到。你确实记得

不过，它的文件名中某个地方有 "Aug"。没问题。只需使用命令

```
find ~/ -name "*Aug*" -print
```

换句话说，从主目录树的顶部开始查找名称中包含 "Aug" 的所有文件，并将结果打印到屏幕上。注意名称周围使用引号。这可以防止 shell 在 find 有机会处理之前就解释通配符。这是 find 命令最基本的形式，所有其他 find 命令都源于此。

## Can I find a file even if I don’t know whether its name begins with an upper- or lowercase letter?

如果你不确定上述报告是 "Aug" 还是 "aug"，你可以轻松地在上述命令的 operator 部分添加第二个参数：

```
find ~/ -name "*Aug*" -o -name "*aug*" -print
```

在此表达式中，我们使用了 "-o"，它表示使用逻辑 OR 进行搜索。名称中包含 "Aug" 或 "aug" 的任何文件都将满足条件。

你也可以使用正则表达式匹配以更简洁的方式执行上述搜索：

```
find ~/ -name "*[Aa]ug*" -print
```

在这里我们说要查找所有文件名中包含以 "A" 或 "a" 开头的字符串 "ug" 的文件——[Aa] 语法表示任一字母都满足正则表达式。

## Why does find keep complaining about a missing conjunction?

find 的一个问题是它试图扩展整个命令行来弄清楚你想要什么。但你需要将特殊字符（“元字符”）隐藏起来，直到 find 准备好处理它们。所以我们要么用引号将特殊字符括起来，要么使用反斜杠字符来转义下一个字符的含义。因此：

```
find ~/ -name [Aa]ug* -print
```

