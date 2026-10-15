

```text
Whenever any reference (however slight) is made here to the condition
of the French people before or during the Revolution, it is truly
made, on the faith of the most trustworthy
witnesses. It has been one of my hopes to add
something to the popular and picturesque means of
understanding that terrible time, though no one can hope
to add anything to the philosophy of Mr Carlyle’s wonderful book.

Tavistock House
November 1859
---
--*-Emacs: dickens.note          (Fundamental)--Bot-----
```

5. 修改查尔斯·狄更斯的文字很有趣，所以保存这些更改并退出。如果尝试使用 C-x C-c 退出程序，emacs 会提醒你有未保存的更改：

   ```text
   --*-Emacs: dickens.note          (Fundamental)--Bot-----
   Save file /users/taylor/dickens.note? (y or n) _
   ```

   输入 y 会保存更改；n 则在不保存更改的情况下退出；如果你改为决定返回编辑会话，Escape 将完全取消该操作。输入 n 会得到第二次提醒，如果不保存更改，更改将会丢失：

   ```text
   --*-Emacs: dickens.note          (Fundamental)--Bot-----
   Modified buffers exist; exit anyway? (yes or no) _
   ```

   这次输入 yes（emacs 如果你只输入 y 会抱怨！），最后，你将回到命令行。

在 emacs 中输入文本非常容易。就像编辑器始终处于插入模式一样。然而，你为此付出的代价是，几乎所有其他操作都需要 Control 或 Meta 序列。甚至 Backspace 键也做了与你想要的不同事情。

运动命令总结在表 12.1 中。

## TABLE 12.1 emacs Motion Commands

| Command | Meaning |
|---|---|
| M-> | Move to the end of the file. |
| M-< | Move to the beginning of the file. |
| C-v | Move forward a screen. |
| M-v | Move backward a screen. |
| C-x ] | Move forward a page. |
| C-x [ | Move backward a page. |
| C-n | Move to the next line. |
| C-p | Move to the previous line. |
| C-a | Move to the beginning of the line. |
| C-e | Move to the end of the line. |
| M-e | Move to the end of the sentence. |
| M-a | Move to the beginning of the sentence. |
| C-f | Move forward a character. |
| C-b | Move backward a character. |
| M-f | Move forward a word. |
| M-b | Move backward a word. |

## Task 12.3: Deleting Characters and Words

在 emacs 缓冲区中插入文本很简单，而且一旦你掌握了方法，在文件中移动也不算太糟糕。如何删除文本呢？使你能够在 emacs 中插入文本的一系列 Control 和 Meta 命令是 emacs 中所有命令的前奏，因此不足为奇的是 C-d 删除当前字符，M-d 删除下一个词，M-k 删除当前句子的剩余部分，而 C-k 删除当前行的剩余部分。如果你键盘上有标有 DEL、RUBOUT 或 Delete 的键，那你就幸运了，因为 Delete 删除前一个字符，M-Delete 删除前一个词，而 C-x Delete 删除前一个句子。

不幸的是，虽然我有 Delete 键，但它在我的系统上绑定到 Backspace 功能，所以每次我按下它时，它实际上发送的是 C-h 序列，而不是 DEL 序列给系统。结果是我无法使用任何这些向后删除命令。

1. 使用 dickens.note 文件重新启动 emacs 并将光标移动到第五行的中间。 （记住 C-n 移动到下一行，C-f 向前移动一个字符。）它应该看起来像这样：

   ```text
   Preface
   When I was acting, with my children and friends, in Mr Wilkie Collins’s drama of The Frozen Deep, I first conceived the main idea of this
   story. A strong desire was upon me then, to
   embody it in my own person;
   and I traced out in my fancy, the state of mind of which it would
   necessarily be the presentation
   to an observant spectator, with particular
   ```

   注意我的光标在这里位于第五行的 w in was 上。

2. 按 C-d C-d C-d 删除单词 was。现在输入 came 来稍微修改句子。屏幕现在应该看起来像这样：

   ```text
   Preface
   When I was acting, with my children and friends, in Mr Wilkie Collins’s
   drama of The Frozen Deep, I first conceived the main idea of this
   story. A strong desire came upon me then, to
   embody it in my own person;
   and I traced out in my fancy, the state of mind of which it would
   necessarily be the presentation
   to an observant spectator, with particular
   ```

   现在按一次 Delete 删除新单词的最后一个字母，然后输入 e 重新插入它。代替一次向后退一个字符，我将使用 M-Delete（Meta 加 Delete 键）来删除刚刚添加的单词。单词被删除了，但单词两侧的空格被保留：

   ```text
   Preface
   When I was acting, with my children and friends, in Mr Wilkie Collins’s
   drama of The Frozen Deep, I first conceived the main idea of this
   story. A strong desire upon me then, to
   embody it in my own person;
   and I traced out in my fancy, the state of mind of which it would
   necessarily be the presentation
   to an observant spectator, with particular
   ```

   再试一个词，看看你能否让这个句子读起来有趣。输入 crept 看看读起来如何。

3. 当然，用《双城记》这样的经典故事来修改可能不是好的写作运气，所以删除整个句子。如果你按 C-x Delete，这是一个 emacs 中多键击命令的例子，它会做正确的事情吗？回想一下 C-x Delete 删除前一个句子。当你按 C-x Delete 时，结果是有帮助的，如果不是完全你想要实现的那样：

### Note

emacs 也需要一些多键击命令，你可能会按一个 Control 序列然后跟随第二个键击。虽然这使你能够用许多命令来控制你的文本，但这也意味着你需要知道许多命令。

```text
Preface
```

