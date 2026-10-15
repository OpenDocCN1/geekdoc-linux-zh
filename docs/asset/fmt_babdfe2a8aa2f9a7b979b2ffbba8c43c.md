
### Note

令人困惑的是，光标仍停留在文件顶部，但 `emacs` 提醒我已按下 `C-x`，并且在我决定要做什么之后需要输入第二个命令。我现在按下 `C-c` 并立即退出 `emacs`。

你已经可以看到 `emacs` 与 `vi` 之间存在一些显著差异。如果你习惯于使用 `C-x C-c` 等多键序列来退出，我想你会喜欢学习 `emacs`。如果不习惯，也请坚持下去。即使你在本课的示例之后再也不使用 `emacs`，了解一点关于它也是有益的。

### Note

为什么要学习一个你不会使用的工具？因为当你从一个系统切换到另一个系统时，你永远不知道可能有哪些图形界面、窗口管理器，甚至编辑器包可用。精通 `emacs` 或 `vi` 意味着即使在最糟糕的、非常简陋的安装环境下，你也能编辑文件并继续进行项目。所以答案确实是，学习是明智的，因为拥有选择是明智的。

## Task 12.2: Moving Around in a File

文件由字符、单词、行、句子和段落组成，而 `emacs` 提供了帮助你在其中移动的命令。大多数系统都启用了方向键，这有助于你不必担心某些键序列，但最好还是全部了解。

最基本的移动是 `C-f` 和 `C-b`，分别用于将光标向前和向后移动一个字符。将它们切换为 `Meta` 命令等价项，光标将按单词移动：`M-f` 将光标向前移动一个单词，`M-b` 将其向后移动一个单词。按下 `C-n` 将光标移动到下一行，`C-p` 移动到上一行，`C-a` 移动到行首，`C-e` 移动到行尾。（`vi` 中所有这些的等价项为 `l`、`h`、`w` 和 `b` 用于向前和向后移动一个字符或单词；`j` 和 `k` 用于向上或向下移动一行；`0` 或 `$` 用于移动到当前行的开头或结尾。你觉得哪种更有意义？）

要向前移动一个句子，可以使用 `M-e`，它实际上将光标移动到句子的末尾。按下 `M-a` 将其移动到句子的开头。注意 `Control` 和 `Meta` 命令之间的相似之处：`C-a` 将光标移动到行的开头，而 `M-a` 将其移动到句子的开头。

command.

+   1. 退回 `emacs` 并定位光标。它应该在屏幕顶部：

Click here to view code image

```
A Tale of Two Cities

Preface

When I was acting, with my children and friends, in Mr Wilkie Collins’s

drama of The Frozen Deep, I first conceived the main idea of this

story. A strong desire was upon me then, to

embody it in my own person;

and I traced out in my fancy, the state of mind of which it would

necessitate the presentation

to an observant spectator, with particular

care and interest.

As the idea became familiar to me, it gradually shaped itself into

its present form. Throughout its execution, it has had complete

possession of me; I have so far verified what

is done and suffered in these pages,

as that I have certainly done and suffered it all myself.

Whenever any reference (however slight) is made here to the condition

of the French people before or during the Revolution, it is truly

made, on the faith of the most trustworthy

witnesses. It has been one of my hopes to add

--Emacs: dickens.note          (Fundamental)--Top-----
```

使用 `C-n` 四次向下移动四行。你的光标现在应该停在 `drama` 的 `d` 上：

Click here to view code image

```
Preface

When I was acting, with my children and friends, in Mr Wilkie Collins’s

drama of The Frozen Deep, I first conceived the main idea of this

story. A strong desire was upon me then, to

embody it in my own person;

and I traced out in my fancy, the state of mind of which it would
```

+   2. 接下来，使用 `M-e` 命令移动到该句子的末尾（`emacs` 要求用两个空格分隔句子）：

Click here to view code image

```
story. I fought the impulse to write this novel vociferously, but, dear reader,\
I felt
the injustice of the situation too strongly in my breast to deny_ A

strong

des\

ire was upon me then, to

embody it in my own person;

and I traced out in my fancy, the state of mind of which it would

necessitate the presentation
```

你可以看到当行变得太长时 `emacs` 会换行（在 `felt` 和 `the` 之间），并且由于行仍然太长无法显示，其中几行以反斜杠结尾。反斜杠并不是文件的一部分；借助它，`emacs` 在表示这些行比能显示的更长。

### 3. 现在尝试通过按 `Backspace` 向后移动几个字符。

糟糕！如果你的系统和我一样，`Backspace` 键根本不会将光标向后移动一个字符。相反，它会启动 `emacs` 帮助系统，你会突然面对一个看起来像这样的屏幕：

Click here to view code image

```
You have typed C-h, the help character. Type a Help option:

A command-apropos. Give a substring, and see a list of commands

(functions interactively callable) that contain

that substring. See also the apropos command.

B describe-bindings. Display table of all key bindings.

C describe-key-briefly. Type a command key sequence;

it prints the function name that sequence runs.

F describe-function. Type a function name and get documentation of it.

I info. The info documentation reader.

K describe-key. Type a command key sequence;

it displays the full documentation.

L view-lossage. Shows last 100 characters you typed.

M describe-mode. Print documentation of current major mode,

which describes the commands peculiar to it.

N view-emacs-news. Shows emacs news file.

S describe-syntax. Display contents of syntax table, plus explanations

T help-with-tutorial. Select the Emacs learn-by-doing tutorial.

V describe-variable. Type name of a variable;

it displays the variable’s documentation and value.
```
