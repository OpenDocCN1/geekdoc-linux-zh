
你可以使用 `TAB` 键来完成你在命令行上输入的单词。这种功能称为补全，它在 `vi` 和 `emacs` 编辑模式下均有效。可以进行几种类型的补全，取决于你在按下 `TAB` 时输入的命令行部分部分。

# 命令补全

如果你正在输入命令名称（通常是命令行上的第一个单词），按下 `TAB` 会启动命令补全，`bash` 会列出包含你已输入部分的命令。如果没有命令是以你输入的字符开头的，`bash` 会发出蜂声。如果只有一个这样的命令，`bash` 会补全命令名称。如果有多个这样的命令，`bash` 在普通模式下什么都不做并发出蜂声。再次按下 `TAB` 会导致 `bash` 显示以你输入的前缀开头的命令列表，并允许你继续输入命令名称。

在接下来的示例中，用户输入 `bz` 并按下 `TAB`。`bash` 发出蜂声（如果用户处于 `emacs` 模式），表示有多个命令以字母 `bz` 开头。用户输入另一个 `TAB` 导致 `bash` 显示以 `bz` 开头的命令列表，随后跟上用户到目前为止输入的命令行：

```
$ bz →TAB (蜂声) → TAB
bzcat bdiff bless
bzcmp bzip2 bzero
bzgrep bziprecover bmore
$ bca → t → ■
```

接下来，用户输入 `c` 并按下两次 `TAB`。`shell` 显示两个以 `bzc` 开头的命令。用户按下 `TAB`。如果此时 `shell` 补全了命令，是因为只有一个命令以 `bca` 开头。

```
$ bzc → (蜂声) → TAB
bzcat bcmp
$ bca → t → ■
```

# 路径补全

路径补全也使用 `TAB`，允许你输入路径的一部分，如果你输入的路径部分足以确定一个唯一的路径，`bash` 会显示该路径。如果有多个路径匹配它，`bash` 会将路径补全到有选择点为止，以便你输入更多内容。

当你输入路径时（包括简单的文件名）并按下 `TAB` 时，`shell` 会发出蜂声（如果 `shell` 处于 `emacs` 模式——在 `vi` 模式下没有蜂声）。它随后会尽可能地扩展命令行。

```
$ cat films/dar →TAB (蜂声) cat films/dark_
```

在 `films` 目录中，每个以 `dar` 开头的文件接下来的字符都是 `k_`，因此 `bash` 无法在对文件之间做出选择的情况下进一步扩展该行。`shell` 将光标留在该字符之后。此时，你可以继续输入路径或按下两次 `TAB`。在后的情况下，`bash` 会发出蜂声，显示你的选择，重新显示命令行，并再次将光标留在字符之后。

```
$ cat films/dark_ →TAB (蜂声) →TAB
$ cat films/dark_victory
```

当你添加足够的信息来区分两个可能的文件并按下时，`bash` 会显示唯一的路径。如果你在字符后按下 `TAB` 然后输入 `p`，`shell` 将补全命令行：

由于没有歧义，`shell` 会添加一个空格，以便你完成行的输入，或直接按 `TAB` 执行命令。如果补全的路径是一个目录，`bash` 会添加一个斜杠 (`/`) 来代替空格。

# 变量补全

当你正在输入变量名时，按下 `TAB` 会导致变量补全，`bash` 会尝试补全变量名称。如果存在歧义，按下两次 `TAB` 会显示选择列表：

```
$ echo →TAB
$ HOME
```

# 变量补全

当你正在输入变量名时，按下 `TAB` 会导致变量补全，`bash` 会尝试补全变量名称。如果存在歧义，按下两次 `TAB` 会显示选择列表：

```
$ echo →TAB
$ HOME
```

# 变量补全

当你正在输入变量名时，按下 `TAB` 会导致变量补全，`bash` 会尝试补全变量名称。如果存在歧义，按下两次 `TAB` 会显示选择列表：

```
$ echo →TAB
$ HOME
```

# .inputrc: 配置 READLINE 库

# 变量补全

历史 343

# 第9 章 再次 Bash (BOURNE AGAIN SHELL)

### 表 9-11 Readline 变量

| 变量 | 影响 |
| :--- | :--- |
| `editing-mode` | 设置为 `vi` 使 Readline 进入 vi 模式。设置为 `emacs` 使 Readline 进入 emacs 模式（默认）。 |
| `horizontal-scroll-mode` | 设置为 `on` 使行超出显示区域。 |
| `mark-directories` | 设置为 `off` 使 Readline 不在目录末尾添加斜杠 (`/`)。默认值为 `on`。 |
| `mark-modified-lines` | 设置为 `on` 使 Readline 为修改行加上星号。 |

# 变量

`kill-line` 在 `emacs` 模式可用，删除当前行。在 `.inputrc` 中放入以下内容，将 `kill-line` 命令（默认未绑定）绑定到按键序列 `control-k`：

```
control-k:kill-line
```

# 键绑定

你可以指定将按键序列映射到 Readline 命令的绑定以便更改或扩展绑定。像 `emacs` 编辑器一样，Readline 包含许多未绑定到按键序列的命令。要使用未定义的命令，你必须使用以下格式之一：

- `keyname:command_name`
- `*keystroke_sequence = command_name`

在第一种格式中，你指定描述序列的字符串。例如，`CONTROL-U` 写为 `control-u`。这种格式适用于将命令绑定到序列。

在第二种格式中，你指定绑定到命令的字符串。你可以使用 `emacs` 风格的反斜杠序列来表示特殊键 `CONTROL (C)`、`META (M)` 和 `ESCAPE (e)`。通过另一个反斜杠转义反斜杠：`\\`。同样，双引号或单引号可以使用反斜杠转义：`\"` 或 `\\'`.

执行 `bind -p` 命令显示所有 Readline 命令列表。如果命令绑定了按键序列，则会显示该序列。你在 `vi` 模式下使用的命令以 `vi` 开头。例如 `vi-next-word` 和 `vi-prev-word` 分别将光标移动到下一个和上一个单词的开头。不以 `vi` 开头的命令通常在 `emacs` 模式下可用。

使用 `bind -q` 来确定哪个按键序列绑定到了命令：

```
$ bind -q kill-whole-line
kill-whole-line 可以通过 "\C-r" 调用。
```

你也可以通过将文本包含在双引号内来进行绑定（仅限 `emacs` 模式）：

此命令会导致在你输入 `QQ` 时，`bash` 插入字符串 "Linux Operating System"。

# 条件构造

你可以使用 `Sif` 指令有条件地选择 `.inputrc` 文件的部分内容。条件构造的语法如下：

```
Sif test[value]
  commands
else
  commands
EndSif
```

其中 `test` 是模式、终端或 `bash`。如果 `test` 等于 `value`（如果未指定 `value`，则条件为真），该结构将执行第一组命令。如果 `test` 为假（当未指定 `value`），则在存在第二组命令时执行该组命令，或者如果不存在则退出该结构。

`Sif` 指令的强大在于它可以执行的三种测试：

- 1. 你可以测试当前设置的模式。
  `Sif mode=vi`
  如果当前的 Readline 模式为 `vi`，则前面的测试为真，否则为假。你可以测试 `vi` 或 `emacs`。
- 2. 你可以测试终端的类型。
  `Sif term=xterm`
  如果变量 `TERM` 被设置为 `xterm`，则前面的测试为真。你可以测试 `TERM` 的任何值。
- 3. 你可以测试应用程序名称。
  `Sif bash`
  当你运行 `bash` 而不是使用 Readline 库的另一个程序时，前面的测试为真。你可以测试任何应用程序名称。

这些测试根据当前模式、终端类型以及你正在使用的应用程序来定制 Readline 库。当你配合 `bash` 和其他程序使用 Readline 库时，它们为你提供了极强大的灵活性。

`.inputrc` 中的以下命令会导致无论 `bash` 处于 `vi` 还是 `emacs` 模式，`CONTROL-Y` 都会将光标移动到下一行的开头：

```
$ cat ~/.inputrc
set editing-mode vi
if editing-mode=vi;then
    "C-y": vi-word
else
    "C-y": forward-word
fi
```

因为 `bash` 在启动时会读取上述条件构造，所以你必须在 `.inputrc` 中设置编辑模式。使用 `set` 交互式切换模式不会改变 `CONTROL-Y` 的绑定。

关于 Readline 库的更多信息，请打开 `bash` 手页并输入命令 `^READLINE`，这会在行开头搜索单词 `READLINE`。

# 如果 readline 未生效，请注销并重新登录
