

## 12.1.1 查找单词的正确拼写

如果你不确定是否使用了单词的正确拼写，可以使用 `spell` 来查询。`spell` 从标准输入读取并输出系统中字典中找不到的任何单词——因此如果一个单词拼写错误，你在输入后它会被回显到屏幕上。

- 例如，要检查单词 `occurance` 是否拼写错误，输入：

```
$ spell RET
occurance RET
occurance
C-d
$
```

在示例中，`spell` 回显了单词 `occurance`，意味着该单词不在系统字典中，因此很可能是一个拼写错误。然后输入 C-d 以退出 `spell`。

## 12.1.2 列出文本中的拼写错误

要输出文件中拼写错误的单词列表，将要检查的文件名作为参数传递给 `spell`。文件中任何拼写错误的单词都会被输出，每个单词独占一行，并按其在文件中的出现顺序排列。

- 要拼写检查文件 `fall-lecture.draft`，输入：

```
$ spell fall-lecture.draft RET
occurance
willl
occurance
$
```

在此示例中，输出了三个单词：`occurance`、`willl` 和再次出现的 `occurance`，意味着这三个单词按此顺序出现在 `fall-lecture.draft` 中，并且不在系统字典中（因此很可能拼写错误）。请注意，拼写错误 `occurance` 在文件中出现了两次。

要纠正拼写错误，你可以随后在首选文本编辑器中打开文件并编辑它。本节后面我将描述一个交互式拼写检查器，允许你在发现拼写错误时立即纠正它。另一个选择是使用内置拼写检查功能的文本编辑器，例如 Emacs。

- 要拼写检查文件 `fall-lecture.draft`，并将可能拼写错误的单词输出到文件 `fall-lecture.spelling`，输入：

```
$ spell fall-lecture.draft > fall-lecture.spelling RET
```

在此示例中，使用了标准输出重定向字符 `>` 将输出重定向到文件（参见章节 Redirecting Output to a File）。

要输出拼写错误单词的字母顺序列表，将输出通过管道传递给 sort；然后将排序后的输出通过管道传递给 uniq 过滤器，以从列表中删除重复项（uniq 从其输入中删除重复的相邻行，输出“唯一”的行）。

- 要输出文件中 `fall-lecture.draft` 的拼写错误单词的排序列表，输入：

```
$ spell fall-lecture.draft | sort | uniq RET
```

## 12.1.3 维护拼写词表

随 Linux 系统安装的标准美式英语词典包含超过 45,000 个单词。尽管这个数字看起来很大，但不可避免地会遗漏很多单词——包括俚语、行话以及一些专有名词。

你可以像查看任何其他文本文件一样查看系统词典，但用户永远不会编辑此文件以添加单词到其中。(19) 相反，你将新单词添加到自己的个人词典中，一个格式与系统词典相同的文件，但保存在你的主目录中，文件名为 `~/.ispell_default`。

用户可以拥有自己的个人词典；本章讨论的拼写命令会自动使用你的个人词典（如果你有的话），除系统词典外。

你使用 ispell 的 i 和 u 选项构建个人词典，这些选项将单词插入到个人词典中。使用这些选项时，可以使用独立工具或各种 ispell Emacs 函数（参见 Interactive Spell Checking and Spell Checking in Emacs）。

NOTE: 你也可以通过使用文本编辑器手动编辑文件来添加（或删除）单词，但要小心保持列表按字母顺序排列！

随着时间的推移，个人词典开始看起来非常个人化，反映其所有者；Gregory Cosmo Haun 通过拍摄十二位用户的肖像并叠加其个人词典的列表制作了一件艺术品（可在网上访问 http://www.reed.edu/~cosmo/art/DictPort.html）。

## 12.1.4 交互式拼写检查

使用 ispell 交互式地拼写检查文件，这样每次发现拼写错误时，你就有机会立即替换它。

- 要交互式拼写检查 `fall-lecture.notes`，输入：

```
$ ispell fall-lecture.notes RET
```

当你输入此命令时，ispell 开始检查文件。它在找到的第一个拼写错误处停止：

```
lecutres          File: fall-lecture.notes

The focus of my series of lecutres this fall are the aspects of the novel.

0: lectures
```

```
[SP] <number> R)epl A)ccept I)nsert L)ookup U)ncap Q)uit e(X)it or ? for help
```

在屏幕顶行，ispell 显示拼写错误的单词，后跟文件名。其下是出现拼写错误的句子，其中相关单词被高亮显示。随后是建议单词的列表，每个单词前面都有一个数字——在此示例中，ispell 只有一个建议：`lectures`。

要将拼写错误替换为建议的单词，输入对应于建议单词的数字（在此示例中，你将输入 0 以将拼写错误替换为 `lectures`）。你只需输入选择的数字——不需要按 RET。

你也可以自行输入更正：这在 ispell 没有提供建议，或提供了建议但你想要的单词不在其中时很有用。要做到这一点，输入 x（表示“替换”），然后输入替换单词，后跟 RET。

有时，ispell 会质疑你可能不想计为拼写错误的单词，例如专有名词等——这些单词不会出现在系统词典中。在这种情况下，你可以做以下几件事。

