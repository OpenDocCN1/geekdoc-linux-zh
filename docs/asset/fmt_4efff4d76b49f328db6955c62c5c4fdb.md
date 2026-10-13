
当我和我的孩子们、朋友们在威尔基·柯林斯先生的戏剧《冰冻深渊》（The Frozen Deep）中表演时，我首先构思了这个故事的主旨。那时，我有一种强烈的欲望，将其化到我的身上；and I traced out in my fancy, the state of mind of which it would

- 下一步，使用 `M-e` 命令移动到句子的末尾（emacs 期望用两个空格分隔句子）：

当我和我的孩子们、朋友们在威尔基·柯林斯先生的戏剧《冰冻深渊》（The Frozen Deep）中表演时，我首先构思了这个故事的主旨。那时，我有一种强烈的欲望，将其化到我的身上；and I traced out in my fancy, the state of mind of which it would

你可以看到行发生了换行（行很长）。

完成后不要按 Return 或 Escape。屏幕现在应该像这样：

```
When I was acting, with my children and friends, in Mr Wilkie Collins' drama of The Frozen Deep, I first conceived the main idea of this story. A strong desire was upon me then, to embed it in my own person;
and traced out in my fancy, the state of mind of which it would
necessitate the presentation
```

- 3. 现在尝试通过 Backspace 向后移动几个字符。

噢不！如果你的系统和我一样，Backspace 键完全不会移动光标。相反，它启动了帮助系统，你面对的是一个这样的屏幕：

```
You have typed C-h, the help. Type a Help option:
```

- A command-apropos. 输入子字符串，查看包含该字符串的命令（可交互的函数）列表。另见 apropos 命令。

B describe-bindings. 显示按键绑定表。

C describe-briefly. 输入命令序列；它打印运行该序列的函数名。

F describe-function. 输入函数名称以获取它的文档。

I info. 信息阅读器。

K describe-key. 输入命令序列；它显示完整文档。

L view-loss. 显示最后使用的 100 个字符。

M describe-mode. 输出当前主模式的文档，描述该模式特有的命令。

V view-emacs. 显示 emacs 新闻。

S describe-syntax. 显示表格加解释。

T help-with-tutorial. 选择通过实践学习。

V describe-variable. 输入变量名称；它显示变量的文档和值。

W where-is. 输入命令名即可打印调用该命令的快捷键。

```
***-Emacs: "Help* (Fundamental)---Top----
A B C F I K L N S T V W C-h-d
```

要退出帮助（你将在下一小时学习更多），按下 Escape，屏幕将恢复。状态行显示了你正在查看的文件，但那并不是你想要操作的文件。

移动光标几个字符的正确键是 `C-b`。使用它返回，并使用 `C-f` 回到原始位置。

- 4. 使用 emacs 移动到文件末尾命令 `M->` 检查文件的最后几行是否发生变化。（通过反射来记忆文件移动命令。）现在屏幕看起来这样：

Whenever any reference (however slight) is made here to the condition

of the French people before or during the Revolution, it is truly

made,  on the faith of the most trustworthy

witnesses. It has been one of my hopes to add

something to the popular and picturesque means of

understanding that terrible time, though no one can

to add anything to the philosophy of Mr Carlyle's wonderful book.

## 第 12 小节：emacs 编辑器概览

塔维斯托住宅

1859年11月

```
...**Emacs: dickens.note (Fundamental)---Bot---
```

5. 修改查尔斯·狄克的文字很有趣，所以保存这些更改并退出。如果你尝试用 `C-x C-c` 退出程序，emacs 会提醒你还有有未保存的更改：

```
...**Emacs: dickens.note (Fundamental)---Bot---
Save file /users/taylor/dickens.note? (y or n)
```

输入 `y` 保存更改；输入 `n` 则不保存更改；如果你决定返回编辑会话，按下 `Escape` 将完全取消该操作。输入 `n` 会第二次提醒你，如果不保存，这些更改将会丢失。

```
...**Emacs: dickens.note (Fundamental)---Bot---
Modified buffers exist; exit anyway? (yes or no) ---
```

这次输入 `yes`（如果你只输入 `y`，它会抱怨的！），最后，你回到了命令行。

在 emacs 中输入文本极其简单。就好像编辑器始终处于插入模式一样。然而，为此付出的代价是任何其他操作都需要 `Control` 或 `Meta` 组合键。甚至退格键的作用也与你的预期不符。

移动命令总结在表 12.1 中。

## 表 12.1 emacs 移动命令

| 命令 | 含义 |
|---|---|
| `M->` | 移动到文件末尾。 |
| `M-<` | 移动到文件开头。 |
| `C-v` | 向上移动一屏。 |
| `M-v` | 向移动一屏。 |
| `C-x ]` |向前翻页。 |
| `C-x [` | 向后翻页。 |
| `C-n` | 移动到下一行。 |

## 另一个流行的编辑器：emacs

## 表 12.1 续

| 命令 | 含义 |
|---|---|
| `C-p` | 移动到上一行。 |
| `C-a` | 移动到行首。 |
| `C-e` | 移动到行尾。 |
| `M-e` | 移动到句末。 |
| `M-a` | 移动到句首。 |
| `C-f` | 前移动一个字符。 |
| `C-b` | 向后移动一个字符。 |
| `M-f` | 前移动一个单词。 |
| `M-b` | 向后移动一个单词。 |

## 任务 12.3：如何删除字符和单词

在 emacs 中插入文本非常简单，在你掌握之后，在文件中移动其实也不难。那么删除文本呢？允许你插入文本的一系列 Control 和 Meta 命令都是 emacs 中的命令，因此也不意外 `C-d` 删除当前字符的前驱字符，`M-d` 删除当前句的剩余部分，而 `C-k` 删除当前行的剩余部分。如果你键盘上有标记为 `DEL`、`RUBOUT` 或 `Delete` 的键，那你就幸运了，因为 Delete 删除前一个字符，M-Delete 删除前一个单词，而 C-x 删除前一个句子。

遗憾的是，尽管你有一个 Delete 键，但在我的系统上它被绑定到了 Backspace 功能，每当你按下它时，它实际上向系统发送了 `C-h` 序列，而不是 `DEL` 序列。结果就是我无法使用这些任何后退删除命令。

- 1. 使用 `dickens.note` 文件重启 emacs，并将光标移动到第五行的中间，`C-f` 移动到下一行，`C-f` 向移动（一个字符）。它看起来应该是这样的：

## 引言

当我与孩子们和朋友在威尔基·柯林斯的剧作《冰冻深渊》（The Frozen Deep）中表演时，我首先构思了这个故事的核心思想。那时我有一种强烈的渴望，将其融入我自身；

并在脑海中勾勒出这种状态对于一个敏锐的观察者所需要的心理，特别是

注意我的光标在这里位于第五行 `on` 的 `w` 上。

2. 按下 `C-d C-d C-d` 移除单词 `was`。现在输入 `came to` 来稍微修改一下句子。屏幕现在应该像这样：

## 引言

当我与孩子们和朋友在威尔基·柯林斯的剧作《冰冻深渊》（The Frozen Deep）中表演时，我首先构思了这个故事的核心思想。那时我有一种强烈的渴望，

融入我自身；

并在脑海中勾勒出这种状态对于一个敏锐的观察者所需要的心理，特别是

现在按下 `Delete` 移除新单词的最后一个字母，然后重新插入。我不是一次一个字符地退格，而是将使用 `M-Delete` 来删除刚刚添加的单词。单词被删除了，但单词两侧的空格被保留：

## 引言
