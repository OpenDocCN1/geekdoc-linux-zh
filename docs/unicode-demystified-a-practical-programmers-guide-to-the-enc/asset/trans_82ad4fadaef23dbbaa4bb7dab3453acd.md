
# 讨论

当 aspell 发现拼写错误的单词时，如果动词为 `list`，会将单词写入标准输出。当动词为 `check` 时，aspell 会显示一个信息屏幕并等待你的指令。此屏幕允许你控制 aspell 对该单词进行的操作，并包含帮助你的信息。屏幕顶行显示可能拼写错误的单词。如果字典中有相似的单词，它们将以编号列表的形式给出。你可以输入其中一个数字来选择列表中的单词，或者输入另一个命令。交互模式下可用的命令如表 III-1 所示。

| 命令 | 表 III-1 描述 |
| --- | --- |
| SPACE | 不执行并并到下一个拼写错误的单词。 |
| number | 选择建议的单词编号以替换拼写错误的单词。 |
| r or R | 将拼写错误的单词替换为你在屏幕底部输入的单词。R 替换该单词的所有出现处，而 r 仅替换当前处。 |
| a | 将单词添加到你的个人字典中。 |
| i or l | 忽略该单词：与 SPACE 相同。I 忽略该单词的所有出现处，而 i 仅忽略当前处。 |
| x | 保存目前已修正的文件并退出 aspell。 |

表 III-1 中的项目显示在屏幕底部的菜单中。屏幕中间是输入行，包含可能拼写错误的单词（高亮显示）以及几行上下文。请参见“示例”。

# 注意事项

aspell 工具并不是寻找拼写错误的万无一失的方法。它也不会检查使用不当但拼写正确的单词（例如用 `red` 替替 `read`）。

# 示例

以下示例使用 aspell 修正 memo.txt 文件中的拼写：

```
$ cat memo.txt
Here's a document for teh aspell utilitey
to check. It obviously needs proofing
quiet badly.
```

第一个示例使用了带有 `check` 动作且不带选项的 aspell。显示了第一个拼写错误单词 `teh` 的屏幕界面。屏幕底部是此时可以提供的命令菜单。九个编号单词都与拼写错误的单词略有不同：

$ aspell check memo.txt
Here's a document for teh aspell util utily
to check. It obviously needs proofing
quiet badly.

+   1) the 6) th
2) Te 7) tea
3) tech 8) tee
4) Th 9) Ted
5) eh 0) tel
i) Ignore I Ignore all
r) Replace R) Replace all
a) Add x) Exit

?
下一个示例使用了 `list` 动作来显示拼写错误的单词列表。`quiet` 一词不在列表中——它使用不当，但拼写是正确的：

$ aspell list < memo.txt
teh
aspell
utilitey
obviously

最后一个示例也使用了 `list` 动作。它展示了通过单个命令检查一个或两个单词拼写的快速方法。用户给出 `aspell list` 命令，然后在 aspell 的输入（键盘）中输入单独 `seperate temperature`。在用户输入 RETURN 和 CONTROL-D（标记文件结束）后，aspell 将拼写错误的单词写入标准输出（屏幕）：

$ aspell list
seperate temperature
CONTROL-D
seperate

# at

在你指定的时间执行 shell 脚本

-   at [options] time [date] [+increment]
atq
atrm job-list
batch [options] [time]

该工具将从标准输入接收的命令作为 shell 脚本在你指定的时刻的工作目录下执行。当 `at` 取消命令时，它通过电子邮件将产生的输出和标准错误发送给你。你可以重定向输出以避免获取邮件。

`atq` 工具显示你队列的任务列表。通常，`atq` 显示你在系统上调度的所有任务。当你以超级用户运行 `atq` 时，它会显示所有用户调度的 `at` 任务。`atrm` 工具取消你队列的任务。`batch` 工具调度任务，使其在系统 CPU 负载较低时（即系统不忙时）运行。

# 参数

时间是你想要执行任务的当天时间。你可以将时间指定为一位、两位或四位数字。一位和二位的数字指定小时，四位数指定小时和分钟。你也可以以 `hh:mm` 的形式给出时间。该工具假设使用 24 小制，除非你在数字后立即加上 `am` 或 `pm`，或者用 `midnight`（午夜）、`noon`（正午）或 `teatime`（下午 4:00）代替时间。

日期是你想要执行任务的星期几或月份中的日期。当你没有指定日期时，如果你指定的小时大于当前小时，`at` 将在今天执行任务。如果小时小于当前小时，`at` 将在明天执行任务。

通过拼出全称或缩写为三个字母来指定星期。你也可以使用 `today` 和 `tomorrow` 单词。

使用月份名称后跟该月的数字来指定日期。你可以在月份和日期后加上年份。

增量是一个数字后跟以下之一（单数或复数均可）：minutes, hours, days, 或 weeks。工具会将增量添加到你指定的时间上。如果你已经给了日期，则不能给出增量。

使用 `atrm` 时，`job-list` 是一个或多个任务编号列表。你可以通过 `-l` 选项或使用 `atq` 来识别任务编号。

# 选项

`-l` 和 `-d` 选项不是用于 `at` 启动任务时。你可以使用它们确定任务状态或取消任务。`-f` 和 `-m` 选项与 `at batch` 配合，但不适用于 `atq` 或 `atrm`。

-   -d 删除你之前通过 `at` 提交的任务。`job-list` 参数是你想要取消的任务的一个或多个任务编号列表。如果你不记得任务编号，使用 `-l` 选项列出你的任务和编号。在 `at` 使用此选项与运行 `atrm` 相同。

-   -f file 在键盘上输入 `at` 命令是有风险的，因为很难纠正错误。此选项提供一个文件名，该文件包含你想在指定时间执行的 shell 脚本。

-   -l list 显示你通过 `at` 提交的所有任务列表。在 `at` 使用此选项与运行 `atq` 相同。

-   -m mail 在任务运行后发送邮件，即使没有内容发送到标准输出或标准错误。
