

4. 在这个练习中，你将使用 <k> 来统计 *nowtime* 中逻辑行的数量。

- a. 按 <k> 直到光标位于屏幕顶行。

你按了两次 <k>。这告诉你，除了你开始所在的那一行（“ow” 是时间之外），还有两个逻辑行。你*看到*四个或更多屏幕行（包括最后一行文本上方的空白行），但只有三个逻辑行。

5. 在这个练习中，你将练习 2 中创建的那一个长逻辑行拆分成独立的逻辑行。

- a. 按 <w> 直到光标停留在屏幕第一行最后一个单词（或部分单词）的第一个字母上。
- b. 按 <i> 使 vi 进入输入模式。
- c. 按 <Enter>
- d. 按 <Esc> 使 vi 进入命令模式。

光标将停留在第二屏幕行的第一个字符上。

- e. 按 <k>，然后按 <j> 以移动光标到顶部两个逻辑行之间。

如果你的终端将 *nowtime* 的前两个句子显示在超过两个屏幕行上，请重复此过程以将剩余的屏幕行分离成独立的逻辑行。（如果你的终端将 *nowtime* 的前两个句子显示在两个屏幕行上，请跳过此练习的其余部分。）

- f. 按 <w> 将光标移动到屏幕行的最后一个单词的第一个字母，该行是你打算拆分成两个逻辑行的行。
- g. 按 <i> 使 vi 进入输入模式。
- h. 按 <Enter>
- i. 按 <Esc>
- j. 按 <k> 直到光标位于顶行。你的光标位置应如你在图 12-4 中所见的那样。

![](img/cc8b9fd5970716027fba0d0a45c13900_217_0.png)

图 12-4 *nowtime* 的前两行

6. 在这个练习中，你将追加文本。（确保你的光标位置如你在图 12-4 中所见的那样。）

- a. 按 <3j> 或 <4j> 将光标移动到最后一行的字母 “o” 处。如果你有四行，按 <3j> 向下移动三行。如果你有五行，按 <4j>。你的光标位置应如你在图 12-5 中所见的那样。

```text
Now is the time for all good men to come to the aid of their country. Now is the time for all good women to come to the aid of their country, too.
^Ow is the time.
```

![](img/cc8b9fd5970716027fba0d0a45c13900_218_0.png)

- b. 按 <$> 将光标移动到行尾，如你在图 12-6 中所见的那样。

```text
good women to come to the aid of their country, too.
^Ow is the time.
```

![](img/cc8b9fd5970716027fba0d0a45c13900_218_1.png)

- c. 按 <a> 以追加文本。
  注意，当你按 <a> 时，光标向右移动一个字符。
- d. 按两次 <空格键>。（记住 vi 需要两个空格来标记句子的结束。）
- e. 输入 The time is now.
- f. 按 <Esc> 返回到命令模式。
你的光标位置应如你在图 12-7 中所见的那样。

![](img/cc8b9fd5970716027fba0d0a45c13900_219_0.png)

图 12-7 添加新文本后的光标位置

7. 在这个练习中，你将使用 <I> 和 <A>。

- a. 按 <I>。（注意这是大写 “I”，vi 处于输入模式。光标位于字母 “o” 下方，如你在图 12-8 中所见。）

![](img/cc8b9fd5970716027fba0d0a45c13900_219_1.png)

图 12-8 光标位于字母 “o” 下方

- b. 输入 Sn 以创建单词 “Snow。”
- c. 按 <Esc> 返回到命令模式。
- d. 按 <A>。（注意这是大写 “A”，vi 处于输入模式。光标位于单词 “now” 后句号的右侧。）
- e. 按两次 <空格键>。
- f. 输入 Is it time yet?
- g. 按 <Esc>

你的屏幕应如 图 12-9 所示。

![](img/cc8b9fd5970716027fba0d0a45c13900_219_2.png)

图 12-9 使用 <I> 和 <A> 命令添加的文本

8. 在这个练习中，你将使用 <o> 和 <O> 来创建空白行。

- a. 按 <o> 使 vi 进入输入模式并在当前行下方添加一个空白行。
- b. 按 <Enter> 添加另一个空白行。

当 vi 处于命令模式时，你必须使用 <o> 或 <O> 来创建空白行。一旦 vi 处于输入模式（如在你按 <o> 之后），你可以使用 <Enter> 来创建额外的空白行。

- c. 输入 I don't know. But the sun is shining.（你正在创建一个文件，稍后的练习中你将对其进行更正。）
- d. 按 <Esc>

你的屏幕应如 图 12-10 所示。

![](img/cc8b9fd5970716027fba0d0a45c13900_220_0.png)

图 12-10 使用 <o> 添加空白行后的 nowtime

- e. 按 <O> 使 vi 进入输入模式并在当前行上方创建一个空白行。
- f. 输入 What time is it?
- g. 按 <Esc>

你的屏幕应如 图 12-11 所示。

![](img/cc8b9fd5970716027fba0d0a45c13900_220_1.png)

图 12-11 添加新文本后的 nowtime

- h. 按 `:w` 以准备 vi 保存你的文件。
- i. 按 <Enter> 以保存文件。

你的屏幕应如 图 12-12 所示。

```text
good women to come to the aid of their country, too.
Snow is the time. The time is now. Is it time yet?
What time is it?
I don't know. But the sun is shining.

"nowtime" 7 lines, 262 characters written
```

图 12-12 vi 确认文件已保存

要以当前文件名保存文件，只需使用步骤 h 和 i 中所示的命令序列。

9. 在这个练习中，你将更正我们在 nowtime 中让你犯的“错误”。

- a. 按 <2k> 将光标向上移动两行。你的屏幕应如 图 12-13 所示。

```text
good women to come to the aid of their country, too.
Snow is the time. The time is now. Is it time yet?
What time is it?
I don't know. But the sun is shining.

"nowtime" 7 lines, 262 characters written
```

图 12-13 命令 <2k> 后的光标位置

- b. 按 <3b>（向后移动三个小单词）将光标移动到 “is” 的第一个字母。
- c. 按 <4n>（光标向左移动四个字符）将光标向左移动四个字符到 “Snow” 中的字母 “n”。
- d. 按 <X> 以删除光标左侧的字符，即大写的 “S”。
- e. 按 <r> 告诉 vi 准备替换一个字符，然后返回命令模式。
- f. 输入 N 以将 “now” 更改为 “Now”。
- g. 按 <3j> 将光标向下移动三行到 “I don't know”。
- h. 缓慢按 <w> 直到光标停留在 “noknow” 的第一个字母 “n” 上。
- i. 按 <xx>（删除光标下的字符）两次以移除字母 “n” 和 “o”。
- j. 按 <Ctrl->> 以清除状态行。你的屏幕应如 图 12-14 所示。

```text
good women to come to the aid of their country, too.
Now is the time. The time is now. Is it time yet?
What time is it?
I don't know. But the sun is shining.
```

![](img/cc8b9fd5970716027fba0d0a45c13900_222_0.png)

10. 在这个练习中，你将使用 <R>、<u> 和 <U>。

- a. 按 <3W>（向前移动三个大单词）将光标移动到单词 “sun”。
- b. 按 <R>。（注意这是大写的 “R”。）
- c. 输入 **moon is bright tonight.**
- d. 按 <Esc>

你的屏幕应如 图 12-15 所示。

```text
Now is the time. The time is now. Is it time yet?

What time is it?
I don't know. But the moon is bright tonight.
```

![](img/cc8b9fd5970716027fba0d0a45c13900_223_0.png)

- e. 保存文件。
- f. 按 <u> 以撤销。

你最近的更改被反转了。你的屏幕应如 图 12-16 所示。

```text
Now is the time. The time is now. Is it time yet?

What time is it?
I don't know. But the sun is shining.
```

![](img/cc8b9fd5970716027fba0d0a45c13900_223_1.png)

- g. 按 <U>。这将撤销对当前行的所有更改。你将再次看到文本 “I don't know. But the sun is shining。”
- h. 按 <q> 并按 *Enter* 以退出 *vi* 且不保存文件。（注意 “q” 后面有一个感叹号。）

不同版本的 *vi* 以不同方式实现撤销功能。在某些版本的 *vi* 中，撤销会保留你最后的 *n* 个操作。（你可以设置 *n* 的值。）第一次按 <u> 会撤销最近的操作，第二次 <u> 会撤销倒数第二近的操作，依此类推。这是现代文字处理器处理撤销的方式。在其他版本的 *vi* 中，反复按 <u> 或 <U> 会在两个版本的文本之间来回切换。你需要通过实验你版本的 *vi* 来确定它是如何实现撤销功能的。

