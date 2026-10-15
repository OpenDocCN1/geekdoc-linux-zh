

## 表 3.14 交互式搜索和替换

| 搜索和替换操作 | 按键 |
|---|---|
| 向前搜索 | <Ctrl+S> |
| 向后搜索 | <Ctrl+R> |
| 正则表达式搜索 | <Ctrl+Alt+S> |
| 反向正则表达式搜索 | <Ctrl+Alt+R> |
| 选择上一个搜索字符串 | <Alt+P> |
| 选择下一个后续搜索字符串 | <Alt+N> |
| 退出增量搜索 | <Enter> |
| 撤销上一个字符的效果 | <Del> |
| 中止当前搜索 | <Ctrl+G> |
| 交互式替换文本字符串 | <Alt+%> |
| 使用正则表达式 | <Alt+X> query-replace-regexp |
| 替换此项，继续下一个 | <Space> 或 y |
| 替换此项，不移动 | , |
| 跳过下一个不替换 | <Del> 或 n |
| 替换所有剩余匹配项 | ! |
| 回到上一个匹配项 | ^ |
| 退出查询替换 | <Enter> |
| 进入递归编辑（<Ctrl+Alt+C> 退出） | <Ctrl+R> |

![](img/02e070097d401d3bf7de4bf1c470b267_148_0.png)

## 图 3.9 第 21 步后的显示。

### 3.3.6.1 练习 3.10

步骤 1：在 shell 提示符下，输入 emacs osfile 然后按 <Enter>。

步骤 2：输入 Windows is the operating system of choice for everyone.

步骤 3：按 <Ctrl+@>。标记现在设置在你在步骤 2 中输入的行末尾。用图形光标和鼠标左键高亮整行第一行。这将定义将被放入 Kill Ring 的区域。

步骤 4：按 <Esc+W>。此操作将区域复制到 Kill Ring。

步骤 5：按 <Enter> 在缓冲区中开始新行，应为空。光标应位于此新行的开头。

步骤 6：按 <Ctrl+Y>。第一行文本现在从 Kill Ring 粘贴到下一空白行。

步骤 7：重复步骤 5 和 6 再六次，使缓冲区中现在有八行文本，都包含文本 Windows is the operating system of choice for everyone.

步骤 8：将光标定位在缓冲区第一行中 Windows 的 W 上。

步骤 9：此时保存缓冲区 <Ctrl+X> <Ctrl+S>。

步骤 10：按 <Esc+X>。然后输入 query-replace 并按 <Enter>。这些操作开始交互式搜索和替换。提示 Query replace: 出现。

步骤 11：输入 everyone 然后按 <Enter>。提示 with: 出现。

步骤 12：输入 students 然后按 <Enter>。提示 Query replacing everyone with students: (? for help) 出现。

步骤 13：在键盘上按 <Space> 将第一行中的单词 everyone 替换为单词 students，并且提示 Query replacing everyone with students: (? for help) 再次出现。

步骤 14：按 <Enter>。提示 Replaced 1 occurrence 出现。

步骤 15：将光标定位在缓冲区第二行中单词 everyone 的 e 上。

步骤 16：重复步骤 10–14，每次交互式地将单词 everyone 替换为单词 computer scientists、engineers、system administrators、web servers、scientists、networking 和 mathematicians，分别在缓冲区第 2–8 行。

确保你在执行步骤 16 的第二次到第八次时，始终将光标定位在你想要替换文本的当前行的上一行！

步骤 17：将光标定位在缓冲区第一行中 Windows 的 W 上。

步骤 18：按 <Esc+X>。然后输入 replace-string 并按 <Enter>。这些操作开始无条件搜索和替换。提示 replace string: 出现。

步骤 19：输入 Windows 然后按 <Enter>。提示 Replace string Windows with: 出现。

步骤 20：输入 UNIX 然后按 <Enter>。提示 Replaced 8 occurrences 出现。正确？

步骤 21：使用 <Ctrl+X><Ctrl+S> 保存缓冲区，使用你计算机系统上可用的设施打印它，并使用 <Ctrl+X> <Ctrl+C> 退出 emacs。你的屏幕显示应如 图 3.9 所示。

以下章节练习要求你应用你在之前的练习中学习到的一些操作：

## 练习 3.8

运行 emacs 并定义键盘宏命令，自动删除

- a. 一行中未指定长度的每隔一个词，
- b. 一个未指定长度的文件中的每隔一行，
- c. 一个未指定长度的文件中未指定长度的行中的每隔一个词和每隔一行。

## 练习 3.9

编写一个键盘宏，如第 3.3.5 节所示，完成练习 3.10 中步骤 10–14 所示的所有操作。

为了进一步练习 emacs，请完成本章末尾的问题 16。

## 3.3.7 如何使用 GNU Emacs 进行纯图形编辑

到目前为止，在我们的工作中，可以在单个基于文本的终端窗口中使用 emacs 并获得所示结果。如果你通过第 2 章中描述的方法之一连接到 UNIX，你很可能通过一个称为 X Window System 的中介与操作系统交互，这将允许你在图形环境中完成所有 emacs 工作。我们将在第 22 章中介绍有关 X Window System 及其一些设施的更多信息（例如 GUI 的特定功能）。就学习 emacs 而言——如果你使用的是 UNIX 和 X Window System——你可能能够在屏幕显示上以自己的框架运行 emacs，或者可能同时在屏幕显示上的多个框架中运行。请注意，在我们的基础 UNIX 系统 PC-BSD 和 Solaris 中，GNU 图形 emacs 的最新版本可通过这些系统中第 23 章所述的软件包管理设施获得。

## 3.3.8 编辑数据文件

以下练习演示了使用图形 GNU emacs 对在练习 3.9 中创建的数据文件进行进一步编辑。在 PC-BSD 和 Solaris 中，使用 X Window System 在 KDE 或 Gnome 桌面默认窗口环境下运行的 GNU emacs 的外观和感觉非常类似于在任何其他具有 GUI 的操作系统（如 Windows 10 或 Mac OS X）下运行的文字处理器或桌面出版应用程序。在以下练习中，我们使用的是 GNU emacs 24.3.1。

### 3.3.8.1 练习 3.11

步骤 1：在终端或控制台窗口中，在 shell 提示符下，输入 emacs datafile 然后按 <Enter>。你的屏幕显示应类似于 图 3.8 所示。

