
Yes; use the `p` command. If you have cut or yanked only a partial line, the text in the buffer will be placed in the current line, after the current cursor position. Use `P` to place the text before the current line or position.

## How can I cut a word into the buffer?

Use `dw`. Actually, this is the simplest example of the more general rule. Use `decursormovement` or `ycursormovement` to cut or copy text into the buffer. The cursor movement keys are the same as for the change command of Table 4.1.

## How can I give my text the right look?

Editors are very personal things. What works for some people may not work for others. So, a good editor lets you change the way it behaves and looks to the point where you can be comfortable with it. In `vi`, there are three basic commands to change the look and feel of your editor, and all are external mode commands. The first is the `:set` command. Use this to set all sorts of options. The list may vary slightly, depending on your particular implementation of `vi`, but Table 4-2 shows some of the most common.

| Option | Description |
|---|---|
| `ai` | Autoindent—new lines start lined up with the indent from the previous line. |
| `noai` | Autoindent off (the default). |
| `aw` | Autowrite—current buffer contents are written when escaping to the shell, or using `:n` to go to the next file. |
| `noaw` | Autowrite off (the default). |
| `flash` | Flash screen on an error instead of beeping (the default). |
| `noflash` | Use a beep instead of a flash. |
| `ic` | Ignore case on searches or pattern matching. |

Table 4-2 vi options

| Option | Description |
|---|---|
| `noic` | 不要忽略大小写（默认值）。 |
| `lisp` | 设置自动缩进以在编辑 lisp 程序时更好地对齐。 |
| `nolist` | 自动缩进与上一行的开头对齐（默认值）。 |
| `magic` | 在进行模式匹配时使用完整的元字符集（默认值）。 |
| `nomagic` | 将元字符限制为仅 `^` 和 `$`。 |
| `mesg` | 允许其他用户向你的终端写入（默认值）。 |
| `nomesg` | 禁用对你的屏幕的写权限。 |
| `nu` | 在屏幕左侧边缘显示行号。 |
| `nonu` | 不显示行号（默认值）。 |
| `ro` | 只读；防止文件被更改，除非通过 `:w!` 显式覆盖该设置。 |
| `noro` | 正常读写模式（默认值）。 |
| `remap` | 允许宏定义直接链接到已映射的命令（默认值）。 |
| `noremap` | 使宏定义显式化。 |
| `showmatch` | 当输入闭合 `)` 或 `]` 时，短暂高亮匹配的 `(` 或 `[`。 |
| `noshowmatch` | 不高亮匹配的分隔符（默认值）。 |
| `showmode` | 在文本输入模式时，在底行显示高亮的模式指示器。 |
| `noshowmode` | 不指示当前模式（默认值）。 |
| `ts=n` | 将制表符间距设置为 `n` 个字符。默认值为 8。 |
| `warn` | 在文本自上次写命令以来被修改时，在 shell 转义前发出警告（默认值）。 |
| `nowarn` | 在 shell 转义前不发出警告，直接执行。 |
| `ws` | 搜索会在文件开头处换行并继续（默认值）。 |
| `nows` | 在搜索到达文件末尾时不换行。 |
| `wm=n` | 换行——当设置为非零时，当当前单词会超出边距时自动插入新行。从显示器右边缘到边距的字符数，即 `wm=8` 将 80 列显示器的右边缘设在第 72 列。 |

**表 4-2** *vi 选项（续）*

现在你知道了 `vi` 中的选项，这里有一些免费建议：

- **将 `showmode` 设置为开启。** 突然发现你只是因为不小心按错键而开始插入文本，这很麻烦。这个简单的改动可以避免这个问题，在你处于文本插入模式时给予温和的提醒。只需输入 `:set showmode` 即可开启。
- **在编写 shell 脚本或程序代码时使用自动缩进，以使你的文件更易读。** 这样，当你编写 `if` 或 `case` 语句或其他编程结构时，更容易将其分开以便清晰。
- **使用 `showmatch` 来帮助在编写程序代码时找到匹配的括号。** 这可以更轻松地判断你正在关闭哪个括号或方括号，因为光标会跳转到对应的起始括号或方括号一秒钟，然后返回。当你不是在编写代码，只是在输入字母或简单文本文件时，这可能是一个小麻烦，因此使用 `:set noshowmode` 将其关闭。
- **将所有你的“正常”设置放在主目录中的 `.exrc` 文件里。** 除非当前目录中有同名文件，否则每次启动 `vi` 时都会自动加载此文件。
- **如果你在 `vi` 中对不同任务有不同的设置，为每个任务创建目录特定的 `.exrc` 文件。** 如果你使用 `vi` 在处理事情时做笔记，将所有这些笔记保存在同一目录中。很容易为记笔记的目录设置一个更合适的特殊 `.exrc` 文件。例如，你可能希望为此目录设置 `wrapmargin=72`，而你的 shell 脚本目录的 `.exrc` 则关闭换行并开启自动缩进。
- **在 `.exrc` 文件中使用注释以使其更易于理解。** 以双引号 (`"`) 开头的任何行在 `vi` 启动时都会被忽略。启动时可能多花一点时间，但如果你在输入时加上注释，就更容易记住为什么设置了某个选项

在文本插入模式下输入时。你可以直接在 `vi` 的命令模式下输入这些命令，或将它们包含在你的 `.exrc` 文件中。我们发现为每个项目准备不同的设置集，并在每个项目的主目录中包含一个单独的 `.exrc` 文件很有帮助。

## 如何自动化从命令模式开始的常用序列？

使用 `:map` 命令。语法是

```
:map key replacement
```

`key` 可以是键盘上几乎任何键，但如果是功能键或控制键，你必须先输入 `CTRL-V` 来“转义”其含义。例如，要将 `CTRL-F1` 映射为运行 UNIX 的拼写检查器，并将结果放在当前缓冲区（文件）的底部，命令是

```
:map ^V G:w!^M:r !spell $^M
```

此序列中的 `ENTER` 键会导致映射终止，因此你必须使用键序列 "`CTRL-V`, `CTRL-F1`, 空格, `G:w!`, `CTRL-V`, `ENTER`, `:r`, 空格, `!spell`, 空格, `%`, `CTRL-V`, `ENTER`"。`ENTER` 键必须先用 `CTRL-V` “转义”。它们在命令中显示为 `^M` 或 `CTRL-M`，这当然就是 `ENTER` 键的实际含义。那么这个命令做了什么？首先它移动到缓冲区的底部，“`G`”；然后它无条件地将缓冲区当前内容写入磁盘文件，“`:w! Enter`”。然后它将运行对当前文件进行拼写检查命令的结果读入缓冲区，“`:r !spell % Enter`”。

大多数版本的 `vi` 在任何时候可以定义的 `:map` 和 `:map!` 命令总数为 32，且总共不能超过 512 个字符。这对于几乎所有目的来说应该足够了，特别是如果你将它们拆分为每个任务的单独 `.exrc` 文件，这才是最有意义的。

## 是否有办法自动化在文本插入模式下开始的频繁任务？
