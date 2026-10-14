

## Completion

shell 帮助你的另一种方式是通过一种称为 *completion* 的机制。completion 在你输入命令时按下 TAB 键时发生。让我们看看它是如何工作的。假设主目录看起来像这样：

```
[me@linuxbox ~]$ ls
Desktop  ls-output.txt  Pictures  Templates  Videos
Documents  Music  Public
```

尝试输入以下内容，但 *不要按* ENTER：

```
[me@linuxbox ~]$ ls l
```

现在按下 TAB。

```
[me@linuxbox ~]$ ls ls-output.txt
```

看到 shell 如何为你补全这一行了吗？再试一个。同样，不要按 ENTER。

```
[me@linuxbox ~]$ ls D
```

按下 TAB。

```
[me@linuxbox ~]$ ls D
```

没有补全，什么都没有。这是因为 D 与目录中的多个条目匹配。要使补全成功，你提供的“线索”必须是不含糊的。如果我们再进一步，如下：

```
[me@linuxbox ~]$ ls Do
```

然后按下 TAB：

```
[me@linuxbox ~]$ ls Documents
```

补全就成功了。

虽然这个例子展示了路径名的补全，这是它最常见的用途，但补全也适用于变量（如果单词以 $ 开头）、用户名（如果单词以 ~ 开头）、命令（如果单词是该行的第一个词）以及主机名（如果单词以 @ 开头）。主机名补全仅适用于 /etc/hosts 中列出的主机名。

许多控制键和 meta 键序列与补全相关联，如表 8-4 所列。

### Table 8-4: Completion Commands

| Key | Action |
|---|---|
| ALT-? | 显示可能的补全列表。在大多数系统上，你也可以通过第二次按下 TAB 键来实现，这要容易得多。 |
| ALT-* | 插入所有可能的补全。这在你想要使用多个可能匹配项时很有用。 |

还有相当多的其他补全方式，比较晦涩。列表出现在 bash 手册页的“READLINE”下。

### PROGRAMMABLE COMPLETION

bash 的最新版本提供了一种称为可编程补全的功能。可编程补全允许你（或更可能的是你的发行版提供商）添加更多补全规则。通常这是为了为特定应用程序添加支持。例如，可以为命令的选项列表添加补全，或匹配应用程序支持的特定文件类型。Ubuntu 默认定义了相当多的补全。可编程补全由 shell 函数实现，这是一种我们将在后面章节中介绍的迷你 shell 脚本。如果你好奇，可以尝试以下操作：

```
set | less
```

现在看看你是否能找到它们。并非所有发行版默认都包含它们。

## Using History

正如我们在第 1 章中发现的，bash 维护着已输入命令的历史记录。这个命令列表保存在你的主目录中，文件名为 bash_history。历史记录功能是减少你需要输入量的有用资源，尤其是在与命令行编辑结合使用时。

### Searching History

在任何时候，我们都可以通过以下方式查看命令历史列表的内容：

```
[me@linuxbox ~]$ history | less
```

默认情况下，bash 存储我们输入的最后 500 条命令，尽管大多数现代发行版将此值设置为 1,000。我们将在第 11 章中看到如何调整此值。假设我们想要找到我们用来列出 /usr/bin 的命令。这是一种方法：

```
[me@linuxbox ~]$ history | grep /usr/bin
```

假设在我们的结果中我们得到了一行包含有趣命令的内容，像这样：

```
88  ls -l /usr/bin > ls-output.txt
```

88 是该命令在历史列表中的行号。我们可以使用另一种称为历史扩展的扩展立即使用它。要使用我们发现的行，我们可以这样做：

```
[me@linuxbox ~]$ !88
```

bash 会将 !88 扩展为历史列表中第 88 行的内容。我们将在下一节介绍其他形式的 history expansion。

bash 还提供了增量搜索历史列表的能力。这意味着我们可以告诉 bash 在我们输入字符时搜索历史列表，每输入一个额外字符就会进一步细化我们的搜索。要开始增量搜索，按 CTRL-R 然后输入你要查找的文本。当你找到它时，你可以按 ENTER 执行命令，或按 CTRL-J 将该行从历史列表复制到当前命令行。要查找文本的下一个出现位置（向上移动历史列表），再次按 CTRL-R。要退出搜索，按 CTRL-G 或 CTRL-C。这里我们看到它的实际操作：

```
[me@linuxbox ~]$
```

首先按 CTRL-R。

```
(reverse-i-search)`':
```

提示符发生变化，表示我们正在执行反向增量搜索。它是“反向”因为我们是从“现在”搜索到过去。接下来，我们开始输入搜索文本。在此示例中，我们正在搜索 /usr/bin：

```
(reverse-i-search)`/usr/bin': ls -l /usr/bin > ls-output.txt
```

立即，搜索返回了我们的结果。有了结果，我们可以通过按 ENTER 执行命令，或者通过按 CTRL-J 将命令复制到当前命令行以便进一步编辑。让我们复制它。按 CTRL-J。

```
[me@linuxbox ~]$ ls -l /usr/bin > ls-output.txt
```

我们的 shell 提示符返回，命令行已加载并准备就绪！

