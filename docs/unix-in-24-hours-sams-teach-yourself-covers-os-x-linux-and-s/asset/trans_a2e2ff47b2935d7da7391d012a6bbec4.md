

GNU emacs。要查看你是否拥有此版本，请在命令行中输入 emacs 或 gnumacs。

仍然找不到系统上的 emacs？请向系统管理员咨询，或在 Google 上搜索你特定操作系统的名称和单词 emacs，看看能查到什么信息。最坏的情况下，你可以前往 GNU 项目网站下载一份副本：http://www.gnu.org/software/emacs/。

+   2. 与其从空白屏幕开始，先退出程序（C-x C-c）并使用其中一个较早的测试文件 dickens.note 重新启动 emacs：

Click here to view code image

```
% gnumacs dickens.note
A Tale of Two Cities          Preface
When I was acting, with my children and friends, in Mr Wilkie Collins’s drama of The Frozen Deep, I first conceived the main idea of this story. A strong desire was upon me then, to embody it in my own person; and I traced out in my fancy, the state of mind of which it would necessitate the presentation to an observant spectator, with particular care and interest.
As the idea became familiar to me, it gradually shaped itself into its present form. Throughout its execution, it has had complete possession of me; I have so far verified what is done and suffered in these pages, as that I have certainly done and suffered it all myself.
Whenever any reference (however slight) is made here to the condition of the French people before or during the Revolution, it is truly made, on the faith of the most trustworthy witnesses. It has been one of my hopes to add --Emacs: dickens.note      (Fundamental)--Top-----
```

正如你所见，这与 vi 启动时的显示完全不同。显示底部状态栏在你编辑文件不同位置时提供有用信息，并且始终提醒你文件名称，这在令人惊讶的情况下非常有帮助。emacs 可以处理不同类型的文件，这里状态栏中的单词 Fundamental 表示 emacs 已准备好处理常规文本文件。如果你正在编程，emacs 可以为你的特定语言提供定制特殊功能。

+   3. 使用 C-x C-c 序列退出 emacs，但在按下 C-x 后等待几秒钟，观察会发生什么。当我按下 C-x 时，屏幕底部突然变为这样：

Click here to view code image

```
on the faith of the most trustworthy witnesses. It has been one of my hopes to add --Emacs: dickens.note      (Fundamental)--Top----- C-x-
```

## Note

令人困惑的是，光标仍停留在文件顶部，但 emacs 提醒我已按下 C-x，并且在我决定要做什么之后需要输入第二个命令。我现在按下 C-c 并立即退出 emacs。

你已经可以看到 emacs 与 vi 之间存在一些显著差异。如果你习惯于使用 C-x C-c 等多键序列来退出，我想你会喜欢学习 emacs。如果不习惯，也请坚持下去。即使你在本课的示例之后再也不使用 emacs，了解一点关于它也是有益的。

## Note

为什么要学习一个你不会使用的工具？因为当你从一个系统切换到另一个系统时，你永远不知道可能有哪些图形界面、窗口管理器，甚至编辑器包可用。精通 emacs 或 vi 意味着即使在最糟糕的、非常简陋的安装环境下，你也能编辑文件并继续进行项目。所以答案确实是，学习是明智的，因为拥有选择是明智的。

## Task 12.2: Moving Around in a File

文件由字符、单词、行、句子和段落组成，而 emacs 提供了帮助你在其中移动的命令。大多数系统都启用了方向键，这有助于你不必担心某些键序列，但最好还是全部了解。

最基本的移动是 C-f 和 C-b，分别用于将光标向前和向后移动一个字符。将它们切换为 Meta 命令等价项，光标将按单词移动：M-f 将光标向前移动一个单词，M-b 将其向后移动一个单词。按下 C-n 将光标移动到下一行，C-p 移动到上一行，C-a 移动到行首，C-e 移动到行尾。（vi 中所有这些的等价项为 l、h、w 和 b 用于向前和向后移动一个字符或单词；j 和 k 用于向上或向下移动一行；0 或 $ 用于移动到当前行的开头或结尾。你觉得哪种更有意义？）

要向前移动一个句子，可以使用 M-e，它实际上将光标移动到句子的末尾。按下 M-a 将其移动到句子的开头。注意 Control 和 Meta 命令之间的相似之处：C-a 将光标移动到行的开头，而 M-a 将其移动到句子的开头。

