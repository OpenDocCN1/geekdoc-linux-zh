
如果你认为通过反复按 `h` 和 `l` 来移动光标很慢，你是对的。
`h` 和 `l` 命令前可以跟一个数字，指定光标移动的空格数。

```
$ mary had a little lambda Esc $ mary had a little lambda
$ mary had a little lambda 10h $ mary had a little lambda
$ mary had a little lambda 13h $ mary had a little lambda
$ mary had a little lambda 5x $ had a little lambda
```

如你所示，`x` 命令前也可以跟一个数字，告诉它要删除多少字符。

你可以通过输入 `$` 命令移动到行尾：

```
$ had a little lambda $ $ had a little lambda
```

要移动到行首，请使用 `$ 0`（那是数字零）命令：

```
$ had a little lambda 0 $ had a little lambda
```

另外两个有命令是 `w` 和 `b`。`w` 命令将光标移动到下一个单词的开头，单词是指由字母、数字、下划线组成的字符串，并由空格或标点符号分隔。`e` 命令将光标向后移动到上一个单词的开头。这些命令前也可以跟一个数字，指定向前或向后移动的单词数。

```
$ had a little lambda w $ had a little lambda
$ had a little lambda 2w $ had a little lambda
$ had a little lambda 3b $ had a little lambda
```

你可以随时按下回车键（Enter），当前行将作为命令执行。

```
$ had a little lambda Hit Enter
ksh: had: not found
$_
```

执行命令后，你将回到输入模式。

## 从历史记录中访问命令

到目前，你已经学习了如何编辑命令行。但 vi 模式还有其他之处，因为你可以使用 vi 命令 `k` 和 `j` 从历史记录中检索命令。`k` 命令会将之前输入的命令放置在终端的当前行，并将光标置于行首。假设刚刚输入了以下命令：

```
$ pwd
/users/pat
$ cd /tmp
$ echo this is a test
this is a test
$_
```

## vi 行编辑模式 295

进入命令模式 (Esc) 并使用 `k` 访问命令历史记录中之前的命令：

```
$ Esc k $ echo this is a test
```

每当使用 `k` 时，当前行就会被历史记录中的上一行替换，你可以一直回溯到任何深度，但受前面讨论过的 `HISTSIZE` 设置的限制。

```
$ echo this is a test k $ cd /tmp
$ cd /tmp $ pwd
```

要执行显示的命令，只需按下回车键即可。

```
$ pwd Hit Enter
/tmp
$_
```

`j` 命令是 `k` 命令的反向，用于显示历史记录中下一个最近的命令。换句话说，`k` 在时间上“向后”移动，而 `j` 在时间上“向前”移动。尝试几次，你会立即明白我们的意思。

`/` 命令会在命令历史中搜索包含指定字符串的命令。如果 `/` 后面跟着一个字符串，shell 将向后搜索历史，找到包含该字符串的最近执行的命令。该命令将被显示。

如果历史记录中没有一行包含指定的字符串，shell 会发出“哔”的一声表示错误。当输入 `/` 时，当前行将被替换为 `/`。

```
/tmp Esc /test /test_
```

按下回车键时将开始搜索。

```
/test_ Enter $ echo this is a test
```

要执行搜索结果得到的命令，必须再次按下回车键。

```
$ echo this is a test Hit Enter again
this is a test
$
```

如果显示的命令不是你寻找的那个，继续输入 `/` 而不带模式并按回车。shell 足够聪明，会使用你上次执行该命令时输入的字符串，并从命令列表中更靠后的位置继续匹配。

当你从历史记录中找到命令后（通过 `k`、`j` 或 `/`），可以使用我们已经讨论过的 vi 命令对命令进行编辑。注意的是，通过这些更改并不会实际更改历史记录中的命令。当你编辑副本时，按下回车键 shell 将执行修改后的版本。

下表总结了编辑历史记录的命令：

## 基本编辑命令

| 命令 | 含义 |
| :--- | :--- |
| h | 向左移动一个字符 |
| l | 向右移动一个字符 |
| b | 向后移动一个单词 |
| w | 向前移动一个单词 |
| 0 | 移动到行首 |
| $ | 移动到行尾 |
| x | 删除当前字符 |
| dw | 删除单词 |
| c | 修改光标处的字符 |
| i | 在光标前插入文本 |
| k | 获取历史记录中的上一个命令 |
| j | 获取历史记录中的下一个命令 |
| / | 在历史记录中搜索字符串 |
