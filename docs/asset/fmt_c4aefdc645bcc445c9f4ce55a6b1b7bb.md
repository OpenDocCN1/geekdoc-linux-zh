
图 10-3 显示编辑 `wisdom` 文件并使用 `vi + wisdom` 命令将光标置于文件的最后一行。

```
vi wisdom
Act without doing;
work without effort.
Think of the small as
large and the few as many.
Confront the difficult
while it is still easy;
accomplish the great task
by a series of small acts.
~
~
"wisdom" 8 lines, 189 characters
```

图 10-3 编辑文件 `wisdom` 并使用 `vi + wisdom` 将光标置于最后一行

图 10-4 显示编辑 `wisdom` 文件并使用 `vi+/task wisdom` 将光标置于包含 `task` 的行。

![](img/3ab707b472189378db808b8f9502ab8c_951_0.png)

图 10-4 编辑文件 `wisdom` 并使用 `vi+/task wisdom` 将光标置于包含 `task` 的行

## 光标控制命令

在 `vi` 中需要的一项关键技能是将光标移动到目标位置。你可以在命令模式下实现这一点。你有多种方法在屏幕上移动光标。表 10-2 总结了一些更常用的光标移动方法。

### 表 10-2 vi 中的光标控制命令

| 命令 | 光标移动 |
| --- | --- |
| `h` 或 `^h` | 向左移动一个字符。 |
| `j` 或 `^j` 或 `^n` | 向下移动一行。 |
| `k` 或 `^p` | 向上移动一行。 |
| `l` 或 `space` | 向右移动一个字符。 |

### 表 10-2 vi 中的光标控制命令

| 命令 | 光标移动 |
| --- | --- |
| `n G` | 转到文件的最后一行。 |
| `nG` | 转到第 `n` 行。 |
| `G$` | 转文件的最后一个最后一个。 |
| `IG` | 转到文件的第一行。 |
| `w` | 转到下一个单词的开头。 |
| `W` | 转到下一个单词的开头，忽略标点。 |
| `b` | 转到上一个单词的开头。 |
| `B` | 转到上一个单词的开头，忽略标点。 |
| `L` | 转到屏幕的最后一行。 |
| `M` | 转到屏幕的中间行。 |
| `H` | 转到屏幕的第一行。 |
| `e` | 移动到下一个单词的末尾。 |
| `E` | 移动到下一个单词的末尾，忽略标点。 |
| `(` | 转到句子的开头。 |
| `)` | 转到句子的末尾。 |
| `{` | 转到段落的开头。 |
| `}` | 转到下一个段落的开头。 |
| `0` 或 `|` | 转到当前行的第一列。 |
| `n` | 转到当前行的第 `n` 列。 |
| `^` (脱字符) | 转到当前行的第一个非空字符。 |
| `$` | 转到当前行的最后一个字符。 |
| `+` 或 `return` | 转到下一行的第一个字符。 |
| `-` | 转到上一行的第一个非空字符。 |

我知道，必须记住这些命令才能将光标移动到目标位置初初看起来可能有点奇怪，但这就是 `vi` 的方式。让我们用 `wisdom` 来展示这些移动操作。就像所有的后续示例一样，命令位于左侧，执行后的结果位于右侧。命令出现在中间。后续示例使用了 `escape` 键。

## vi 编辑

图 10-5 `vi` 中的光标移动 (`h`, `j`, `k`, 和 `l`)

### 第10 章 vi 编辑

| `vi wisdom` | `h` | `vi wisdom` | `G` | 转到最后一行 |
| --- | --- | --- | --- | --- |
| Act without doing; work without effort. Think of the small as large and the few as many. Confront the difficult while it is still easy; accomplish the great task by a series of small acts. | 向左移动一个 | Act without doing; work without effort. Think of the small as large and the few as many. Confront the difficult while it is still easy; accomplish the great task by a series of small acts. |
| `"wisdom" 8 lines, 189 characters` | | | | |
| `vi wisdom` | `j` | `vi wisdom` | `W` | 转到下一个单词的开头 |
| --- | --- | --- | --- | --- |
| Act without doing; work without effort. Think of the small as large and the few as many. Confront the difficult while it is still easy; accomplish the great task by a series of small acts. | 向下移动一行 | Act without doing; work without effort. Think of the small as large and the few as many. Confront the difficult while it is still easy; accomplish the great task by a series of small acts. |
| `"wisdom" 8 lines, 189 characters` | | | | |
| `vi wisdom` | `k` | `vi wisdom` | `b` | 转到上一个单词的开头 |
| --- | --- | --- | --- | --- |
| Act without doing; work without effort. Think of the small as large and the few as many. Confront the difficult while it is still easy; accomplish the great task by a series of small acts. | 向上移动一行 | Act without doing; work without effort. Think of the small as large and the few as many. Confront the difficult while it is still easy; accomplish the great task by a series of small acts. |
| `"wisdom" 8 lines, 189 characters` | | | | |
| `vi wisdom` | `l` | `vi wisdom` | `e` | 转到下一个单词的末尾 |
| --- | --- | --- | --- | --- |
| Act without doing; work without effort. Think of the small as large and the few as many. Confront the difficult while it is still easy; accomplish the great task by a series of small acts. | 向右移动一个 | Act without doing; work without effort. Think of the small as large and the few as many. Confront the difficult while it is still easy; accomplish the great task by a series of small acts. |
| `"wisdom" 8 lines, 189 characters` | | | | |

# 在 vi 中添加文本

现在我们已经知道了如何移动光标，让我们对光标进行一些操作吧。你首先需要学习光标移动，因为添加文本的命令是相对于光标所在的位置执行的。表 10-3 汇总了一些添加文本的命令。

| 命令 | 插入动作 |
|---|---|
| `a` | 在光标后追加新文本。 |
| `A` | 在当前行末尾追加新文本。 |
| `i` | 在光标前插入新文本。 |
| `I` | 在当前行开头插入新文本。 |
| `o` | 在当前行下方打开新行并插入。 |
| `O` | 在当前行上方打开新行并插入。 |
| `:r file` | 读取文件并在当前行后插入。 |
| `:nr file` | 读取文件并在第 `n` 行后插入。 |
| `escape` | 回到命令模式。 |
| `^v char` | 插入时忽略字符的特殊含义。这用于插入特殊字符。 |
