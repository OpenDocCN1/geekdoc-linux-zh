

## 任务 12.4：Emacs 中的搜索与替换

由于 emacs 会保留屏幕最后一行用于其系统提示，因此搜索和替换比在 vi 中更容易。此外，系统会提示输入字段并针对每个出现的位置询问是否更改。另一方面，该命令并不是一两个简单的按键；它是一个命名 emacs 命令的示例。命名 emacs 命令是指需要你输入其名称的命令，例如 query-replace，而不是一两个命令键。

向前搜索模式是通过按下 C-s 完成的，向后搜索则使用 C-r 进行（助记符为 search forward 和 reverse search）。当你找到想要的内容时，按下 Escape 即可退出搜索，要取消搜索并返回起始位置，请使用 C-g。

### 注意

不幸的是，你可能会发现按下 C-s 会对系统造成非常奇怪的影响。事实上，^S 和 ^Q 通常用作终端的流量控制，按下 C-s 时，你实际上是在告诉终端模拟器停止发送信息，直到看到 C-q 为止。流量控制是计算机和终端在数据传输期间确保彼此不会超越对方所使用的协议。如果这种情况发生在你身上，你需要关闭 XON/XOFF 流量控制。请向系统管理员寻求帮助或检查你的终端或 telnet 应用的设置。

查询替换实际上是 emacs 中的一个全新功能。要开始查询替换，请使用 M-x query-replace。emacs 会提示下一步该做什么。当匹配项显示时，你可以输入各种命令来影响其行为：y 执行更改；n 保持匹配序列不变但移动到下一个匹配项；Escape 或 q 退出替换模式；! 自动替换模式的所有出现位置而不进行进一步提示。

- 1. 我仍然在查看 dickens.note 文件，并且已使用 M-< 将光标移动到左上角。文件中的某个地方有单词 Revolution，但我不确定在哪里。更糟糕的是，每次我按下 C-s 时，由于流量控制问题，终端都会冻结，直到我按下 C-q。
-   
- 相反，我将向后搜索，首先使用 M-> 将光标移动到文件底部，然后按下 C-r：

Click here to view code image

```
--Emacs: dickens.note          (Fundamental)--Bot-----
I-search backward:
```

当我输入模式 Revolution 的每个字符时，光标会向后跳动，随着模式越来越长而匹配，直到 emacs 找到我想要的单词：

Click here to view code image

```
Whenever any reference (however slight) is made here to the condition
```

> of the French people before or during the Revolution, it is truly made, on the faith of the most trustworthy witnesses. It has been one of my hopes to add something to the popular and picturesque means of understanding that terrible time, though no one can hope to add anything to the philosophy of Mr Carlyle's wonderful book.

```
--Emacs: dickens.note
I-search backward: Revol
```

### 2. 现在尝试查询替换功能。首先，我使用 M-< 移到文件顶部，然后按下 M-x，这会导致在底部状态行显示提示：

然后我输入单词 query-replace 并按下 Return。emacs 理解我想要查找所有模式出现的位置并将其替换为另一个。emacs 将提示更改为：

```
Query replace: _
```

现在我输入想要替换的单词。为了在文件中制造混乱，我想把 French 改为 Danish，因为也许《双城记》真的发生在伦敦和哥本哈根。为了做到这一点，我输入 French 并按下 Return。提示更改为：

```
Query replace French with: _
```

我输入 Danish 并再次按下 Return。

```
as that I have certainly done and suffered it all myself.
Whenever any reference (however slight) is made here to the condition of the French people before or during the Revolution, it is truly made, on the faith of the most trustworthy witnesses. It has been one of my hopes to add
```

Whenever any reference (however slight) is made here to the condition of the French people before or during the Revolution, it is truly made, on the faith of the most trustworthy witnesses. It has been one of my hopes to add

