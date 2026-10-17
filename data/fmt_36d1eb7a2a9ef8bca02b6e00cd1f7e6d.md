
# 搜索

Readline 提供了用于在命令历史（见下文 HISTORY 部分）中搜索包含指定字符串的行的命令。有两种搜索模式：增量式和非增量式。

增量搜索在用户完成输入搜索字符串之前就开始了。随着搜索字符串每个字符的输入，readline 都会显示历史中与目前字符串匹配的下一个条目。增量搜索只需要找到所需的历史条目所需的字符数量。`search-terminators` 变量值中的字符被用于终止增量搜索。如果该变量未赋值，则 `Escape` 和 `Control-J` 字符将终止增量搜索。`Control-G` 将中止增量搜索并恢复原始行。当搜索结束时，包含该搜索内容的历史条目将成为当前行。

要查找历史列表中的其他匹配项，请根据情况输入 `Control-S` 或 `Control-R`。这将在历史中向后或向前搜索与目前字符串匹配的下一个条目。任何其他绑定到 readline 的键序列都将终止搜索并执行该命令。例如，换行将终止搜索并接受该行，从而执行历史列表中的命令。

Readline 会记住上一次的增量搜索字符串。如果在输入两个 `Control-R` 之间没有定义新搜索字符串的中间字符，则使用任何记忆的搜索字符串。

非增量搜索在开始搜索匹配的历史行之前，会读取整个搜索字符串。搜索字符串可以是用户输入的，也可以是当前行内容的一部分。

# Readline 命令名称

以下是命令名称及其默认未绑定的键序列列表。没有附带键序列的命令名称默认均未绑定。在以下描述中，`point` 指代当前光标位置，`mark` 指代由 `set-mark` 命令保存的光标位置。`point` 和 `mark` 之间的文本被称为 `region`（区域）。

# 移动命令

- `beginning-of-line` (`C-a`)
移动到当前行的开头。

- `end-of-line` (`C-e`)
移动到行的末尾。

- `forward-char` (`C-f`)
向前移动一个字符。

- `backward-char` (`C-b`)
向后移动一个字符。

- `forward-word` (`M-f`)
移动到下一个单词的末尾。单词由字母数字字符（字母和数字）组成。

- `backward-word` (`M-b`)
移动到当前或上一个单词的开头。单词由字母数字字符（字母和数字）组成。

- `shell-forward-word`
移动到下一个单词的末尾。单词由未加引号的元字符界定。

- `shell-backward-word`
移动到当前或上一个单词的开头。单词由未加引号的元字符界定。

- `clear-screen` (`C-l`)
清除屏幕，并将当前行留在屏幕顶部。带有参数时，则刷新当前行而不清除屏幕。

- `redraw-current-line`
刷新当前行。

# 历史操作命令

- `accept-line` (`Newline`, `Return`)
无论光标所在何处，均接受该行。如果该行非空，则根据 `HISTCONTROL` 变量的状态添加到历史列表中。如果该行是修改过的历史行，则将历史行恢复到其原始状态。

- `previous-history` (`C-p`)
从历史列表中获取上一个命令，在列表中向后移动。

- `next-history` (`C-n`)
从历史列表中获取下一个命令，在列表中向前移动。

- `beginning-of-history` (`M-<`)
移动到历史中的第一行。

- `end-of-history` (`M->`)
移动到输入历史的末尾，即当前输入的行。

- `reverse-search-history` (`C-r`)
从当前行开始向后搜索，并在历史中必要时向上 `up` 。这是一个增量搜索。

- `forward-search-history` (`C-s`)
从当前行开始向前搜索，并在历史中必要时向下 `down`移动。这是一个增量搜索。

- `non-incremental-reverse-search-history` (`M-p`)
从当前行开始，使用非增量搜索对用户提供的字符串进行历史向后搜索。

- `non-incremental-forward-search-history` (`M-n`)
使用非增量搜索对用户提供的字符串进行历史向前搜索。

- `history-search-forward`
在历史中向前搜索当前行开头与 `point` 之间的字符字符串。这是一个非增量搜索。

- `history-search-backward`
在历史中向后搜索当前行开头与 `point` 之间的字符字符串。这是一个非增量搜索。

- `yank-nth-arg` (`M-y`)
在 `point` 处插入上一个命令的第一个参数（通常是上一行的第二个单词）。带有数字参数 *n* 时，则插入上一个命令的第 *n* 个单词（上一个命令从 0 开始）。负参数插入上一个命令末尾的第 *n* 个单词。一旦参数 *n* 计算完成，由于指定了 `“in”` 历史扩展，该参数将被提取。

- `yank-last-arg` (`M-,` `M_-`)
插入上一个命令的最后一个参数（上一个历史条目的最后一个单词）。带有数字参数时，其行为与 `yank-nth-arg` 完全相同。在历史列表中向后移动，依次插入每行的最后一个单词（或第一次调用时参数指定的单词）。提供给这些连续调用的任何数字参数决定了在历史中移动的方向（向后或向前）。

- `insert-last-arg` (`M-,` `M_-`)
`yank-last-arg` 的别名。

- `operate-and-get-next` (`C-o`)
接受当前行并从历史中相对于当前行获取下一行。任何参数都会被忽略。

- `edit-and-execute-command` (`C-e`)
在当前行上调用编辑器，并执行结果。Bash 尝试按顺序调用 `VISUAL`、`EDITOR` 和 `emacs` 作为编辑器。

# 修改文本命令

- `end-of-file` (usually `C-d`)
指示文件结束的字符，例如通过 “stty” 设置。当行没有字符且 `point` 在行开头时，readline 将其解释为输入结束并返回 EOF。

- `delete-char` (`C-d`)
删除 `point` 处的字符。如果该函数绑定到与 tty 相同的字符（`C-d` 通常如此），请参见上文产生的影响。

- `backward-delete-char` (`Rubout`)
删除光标后的字符。当给定数字参数时，将删除的文本保存到 `kill ring` 中。

- `forward-backward-delete-char`
删除标下的字符，除非光标在行末尾，此时光标后的字符将执行删除。

- `quoted-insert` (`C-v`)
将输入的下一个字符原样添加到行。这是输入字符 `C-q` 的方式。

- `tab-insert` (`C-v TAB`)
插入制表符字符。

- `self-insert` (`a`, `b`, `A`, `1`, ...)
插入输入的字符。

- `transpose-chars` (`C-t`)
将 `point` 之前的字符向前移动到 `point` 处的字符，同时也让 `point` 向前。如果 `point` 在行末尾，将交换 `point` 之前的两个字符。

- `transpose-words` (`M-t`)
将 `point` 之前的单词越过 `point` 之后的单词，同时也让 `point` 越过该单词。如果 `point` 在行末尾，将交换行的最后两个单词。

# `upcase-word` (`M-u`)

将当前（或后续）单词转换为大写。带有负参数时，会将上一个单词转换为大写，但不移动光标。

# `downcase-word` (`M-I`)

将当前（或后续）单词转换为小写。带有负参数时，会将上一个单词转换为小写，但不移动光标。

# `capitalize-word` (`M-c`)

将当前（或后续）单词的首字母大写。带有负参数时，会将上一个单词的首字母大写，但不移动光标。

# `overwrite-mode`

切换覆盖模式。带有显式正数字参数时切换到覆盖模式。带有显式非正数字参数时切换到插入模式。此命令影响 emacs模式；vi 模式的覆盖方式不同。每次调用 `readline()` 都会启动插入模式。在覆盖模式下，绑定到 `self-insert` 的字符将替换光标处的文本而不是向右推文本。绑定到 `backward-delete-char` 的字符将光标前的字符替换为空格。默认情况下，此命令未绑定。

# 剪切与粘贴 (Killing and Yanking)

## `kill-line` (`C-k`)

剪切从光标位置到行尾的文本。

## `backward-kill-line` (`C-x Rubout`)

向后剪切到行首。

## `unix-line-discard` (`C-u`)

从光标位置向后剪切到行首。剪切的文本保存在剪切环（kill-ring）中。

## `kill-whole-line`

剪切当前行的所有字符，无论光标在哪里。

## `kill-word` (`M-d`)

剪切从光标到当前单词结束，或者从单词间隙到下一个单词结束。单词边界与 `forward-word` 使用的相同。

## `backward-kill-word` (`M-Rubout`)

剪切光标之前的单词。单词边界与 `backward-word` 使用的相同。

## `shell-kill-word` (`M-d`)

剪切从光标到当前单词结束，或者从单词间隙到下一个单词结束。单词边界与 `shell-forward-word` 使用的相同。

## `shell-backward-kill-word` (`M-Rubout`)

剪切光标之前的单词。单词边界与 `shell-backward-word` 使用的相同。

## `unix-word-rubout` (`C-w`)

使用空格作为单词边界，剪切光标之前的单词。剪切的文本保存在剪切环中。

## `unix-filename-rubout`

使用空格和斜杠字符作为单词边界，剪切光标之前的单词。剪切的文本保存在剪切环中。

## `delete-horizontal-space` (`M-\`)

删除光标周围所有的空格和制表符。

## `kill-region`

剪切当前区域内的文本。

## `copy-region-as-kill`

将区域内的文本复制到剪切缓冲区中。

## `copy-backward-word`

将光标之前的单词复制到剪切缓冲区。单词边界与 `backward-word` 相同。

## `copy-forward-word`

将光标后的单词复制到剪切缓冲区。单词边界与 `forward-word` 相同。

## `yank` (`C-y`)

将剪切环顶部的内容粘贴到光标所在的缓冲区。

## `yank-pop` (`M-y`)

旋转剪切环并粘贴新的顶端内容。仅在执行 yank 或 yank-pop 后有效。

# 数字参数 (Numeric Arguments)

## `digit-argument` (`M-0`, `M-1`, ..., `M—`)

将此数字添加到已累积的参数中，或开始一个新参数。M— 开始负参数。

## `universal-argument`

这是指定参数的另一种方式。如果此命令后跟着一个或多个数字（可选带有前负号），则这些数字将重新定义参数。如果命令后直接跟着数字，执行 `universal-argument` 会结束数字参数，否则会被忽略。一种特殊情况是：如果此命令后紧跟着一个既不是数字也不是负号的字符，则下一个命令的参数计数将乘以四。参数计数初始为一，因此第一次执行此函数将使参数计数变为 4，第二次变为 16，依此类推。

# 补全 (Completing)

## `complete` (`TAB`)

尝试对光标前的文本进行补全。Bash 会依次尝试将文本视为变量（如果以 $ 开头）、用户名（如果以 ~ 开头）、主机名（如果以 @ 开头）或命令（包括别名和函数）进行补全。如果这些都不产生匹配项，则尝试文件名补全。## `possible-completions` (`M-?`)

列出光标前文本可能的补全。

## `insert-completions` (`M-*`)

插入所有由 `possible-completions` 生成的光标前文本补全。

## `menu-complete`

与 `complete` 类似，但会将待补全的单词替换为补全列表中的单个匹配项。通过补全列表重复执行 `menu-complete` 步骤，依次插入每个匹配项。在列表末尾，会响铃（取决于 bell-style 的设置）并恢复原始文本。参数 m 会在匹配列表中向前移动 n 个位置；可以使用负参数向后移动。此命令本应绑定到 TAB，但默认未绑定。

## `menu-complete-backward`

与 `menu-complete` 相同，但如果给 `menu-complete` 给了负参数，则在可能的补全列表中向后移动。此命令默认未绑定。

## `delete-char-or-list`

如果不在行首或行尾，则删除光标下的字符（类似于 delete-char）。如果在行尾，行为与 `possible-completions` 相同。

## `complete-filename` (`M-`)

对光标前的文本执行文件名补全。

## `possible-filename-completions` (`C-x /`)

列出光标前可能的文件名补全。

## `complete-username` (`M~`)

对光标前的文本执行用户名补全。

## `possible-username-completions` (`C-x ~`)

列出光标前可能的用户名补全。

## `complete-variable` (`M-`)

对光标前的文本执行变量补全。

## `possible-variable-completions` (`C-x $`)

列出光标前可能的变量补全。

## `complete-hostname` (`M@`)

对光标前的文本执行主机名补全。

## `possible-hostname-completions` (`C-x @`)

列出光标前可能的主机名补全。

## `complete-command` (`M-!`)

对光标前的文本执行命令补全。按别名、保留字、shell 函数、shell 内内置以及可执行文件的顺序进行匹配。

## `possible-command-completions` (`C-x !`)

列出光标前可能的命令补全。

## `dynamic-complete-history` (`M-TAB`)

对光标前的文本进行动态补全，与历史列表进行匹配。

## `dabbrev-expand`

对光标前的文本进行菜单补全，与历史列表进行匹配。

## `complete-into-braces` (`M{}`)

执行文件名补全并将补全列表在大括号内，以便 shell 可以使用该列表（见上文的大括号展开）。

# 键盘宏 (Keyboard Macros)

## `start-kbd-macro` (`C-x (`)

开始记录输入的字符到当前键盘宏。

## `end-kbd-macro` (`C-x)`)

停止记录输入的字符并存储定义。

## `call-last-kbd-macro` (`C-x e`)

重新执行最后定义的键盘宏，宏中的字符就像在键盘上输入的一样。

## `print-last-kbd-macro`

以 inputrc 文件的格式打印最后定义的键盘宏。

# 其他 (Miscellaneous)

## `re-read-init-file` (`C-x C-r`)

读取 inputrc 文件的内容，并纳入其中的任何变量赋值。

## `abort` (`C-g`)

取消当前的编辑命令并响终端铃（取决于 bell-style 的设置）。

## `do-uppercase-version` (`M-a`, `M-b`, `M-x`, ...)

如果元字符 x 是小写的，则运行绑定到相应大写字符的命令。

## `prefix-meta` (`ESC`)

将下一个字符元化。ESC f 等同于 Meta-f。

## `undo` (`C-_, C-x C-u`)

增量撤销，每行单独记忆。

## `revert-line` (`M-r`)

撤销对此行进行的所有更改。这相当于反复执行撤销命令，直到该行恢复到初始波浪展开状态 (M-&)。

对当前单词执行波浪展开。

`set-mark` (`C-@`, `M-<csp>`) 将标记（mark）设置在当前光标处。如果提供了数值参数，则将标记设置在相应位置。

`exchange-point-and-mark` (`C-x C-x`) 交换光标和标记。当前的光标位置被设置为之前保存的位置，而旧的光标位置被保存为标记。

`character-search` (`C-J`) 读取一个字符并移动到该字符的下一次出现处。负数计数将搜索之前的出现处。

`character-search-backward` (`M-C-J`) 读取一个字符并移动到该字符的上一次出现处。负数计数将搜索后续的出现处。

`skip-csi-sequence` 读取字符以消耗多键序列，例如为 Home 和 End 等键定义的序列。此类序列以控制序列指示符（CSI）开头，通常为 ESC[-。如果此序列没有显式绑定到某个按键，则产生的序列将产生产生影响（除了执行 readline 命令外），而不是将字符插入到编辑缓冲区。它默认未绑定的，通常绑定到 ESC[-。

`insert-comment` (`M-#`) 在不提供数值参数的情况下，将 readline comment-begin 变量的值插入到当前行的开头。如果提供了数值参数，此命令将作为切换开关：如果行开头的字符与 comment-begin 的值不匹配，则插入该值；否则，从行开头删除 comment-begin 中的字符。无论何种情况，如果之前输入过，该行都被视为换行符。comment-begin 的默认值使此命令将当前行变为注释。如果数值参数导致注释字符被移除，该行将由 shell 执行。

`glob-complete-word` (`M-g`) 将光标前的单词视为路径名扩展的模式，并隐式地添加星号 **。该模式用于生成匹配的文件名列表以供可能的补全。

`glob-expand-word` (`C-x *`) 将之前的单词视为路径名扩展的模式，并插入匹配的文件名列表以替换该单词。如果提供了数值参数，则在路径扩展之前添加星号 **。

`glob-list-expansions` (`C-x g`) 显示 glob-expand-word 将会生成的扩展列表，并重绘行。如果提供了数值参数，则在路径扩展之前添加星号 **。

## `dump-functions`

将所有函数及其按键绑定打印到 readline 输出流。如果提供了数值参数，输出的格式将处理为可以作为 inputrc 文件的一部分。

## `dump-variables`

将所有可设置的 readline 变量及其值打印到 readline 输出流。如果提供了数值参数，输出的格式将处理为可以作为 inputrc 文件的一部分。

## `dump-macros`

打印所有绑定到宏的 readline 键序列及其输出的字符串。如果提供了数值参数，输出的格式将处理为可以作为 inputrc 文件的一部分。

## `display-shell-version` (`C-x C-v`)

显示关于当前 bash 实例的内部版本信息。

## 可编程补全 (Programmable Completion)

当尝试对命令的参数进行补全，且该命令已通过下文定义的“完整的 SHELL 内置命令”定义了补全规范（compspec）时，将调用可编程补全。

首先，识别命令名称。如果空行开头是命令单词，则将使用带有 -E 选项定义的补全 compspec。如果为该命令定义了 compspec，则使用该 compspec 生成该单词的可能补全列表。如果命令单词是全名（fullname），则会首先搜索全名的 compspec。如果没有为全名找到 compspec，将尝试寻找斜杠后部分的 compspec。如果这些搜索都没有找到 compspec，则将使用带有 -D 选项定义的任何补全 compspec 作为默认值。

一旦找到 compspec，将使用它来生成匹配单词列表。如果未找到 compspec，则执行上述上文“补全（Completing）”部分描述的默认 bash 补全。

首先，使用 compspec 指定的操作。只返回以正在补全的单词为前缀的匹配项。当使用 -f 或 -d 选项进行文件名或目录名补全时，将使用 shell 变量 IGNORE 来过滤匹配项。

接下来生成由 -G 选项指定的路径名模式的补全。模式生成的单词可能与正在补全的单词不匹配。不使用 shell 变量 GLOBIGNORE 来过滤匹配项，但会使用 IGNORE 变量。

接下来，考虑作为 -W 选项参数的字符串。该字符串使用 IFS 特殊变量中的字符作为分隔符进行分割。遵循 shell 引用。每个单词随后将使用括号扩展、波浪展开、参数和变量扩展、命令替换和算术扩展进行扩展，如“扩展（EXPANSION）”部分所述。扩展的结果将与正在补全的单词进行前缀匹配，匹配的单词将成为可能的补全。

在生成这些匹配项后，将调用使用 -F 和 -C 选项指定的任何函数或命令。当调用命令或函数时，将为 COMP_LINE、COMP_POINT、COMP_KEY 和 COMP_TYPE 变量赋值，正如“shell 变量”部分所示。如果调用了 shell 函数，还会设置 COMP_WORDS 和 COMP_CWORD 变量。当调用命令或函数时，第一个参数 ($S1) 是正在补全参数的命令名称，第二个参数 ($S2) 是正在补全的单词，第三个参数 ($S3) 是当前行上正在补全的单词。不会对生成的补全进行过滤；函数或命令可以自由生成匹配项。

调用使用 -F 指定的任何函数。第一个函数可以使用 shell 功能（包括下文描述的 compgen 内置命令）来生成匹配项。它必须将可能的补全放入 COMPREPLY 数组中，每个元素一个。

接下来，在使用 -C 指定的任何命令，等同于命令替换的环境调用。它应该向标准输出打印补全列表，每行一个。必要时，可以使用反斜杠转义换行符。

在生成所有可能的补全后，对列表应用由 -X 选项指定的过滤器。过滤器是路径名扩展的模式；模式中的 & 将替换为正在补全单词的文本。字面量 & 可以用反斜杠转义；在尝试匹配之前删除反斜杠。任何匹配模式的补全将从列表中移除。领先的符号取反模式；在这种情况下，不匹配模式的补全将被移除。

最后，将 -P 和 -S 选项指定的任何前缀和后缀添加到补全列表的每个成员中，并将结果返回 readline 补全代码作为可能的补全列表。

如果之前应用的操作没有生成任何匹配项，且在定义 compspec 时提供了 -o dirnames 选项，则尝试进行目录名补全。

如果在定义 compspec 时提供了 -plus dirs 选项，则尝试进行目录名补全，并将任何匹配项添加到其他操作的结果中。

默认情况下，如果指定了 compspec，其生成的任何内容将作为完整的补全集返回给补全代码。不会尝试默认的 bash 补全；如果在定义 compspec 时提供了 -bashdefault 选项，则当 compspec 未生成匹配项时将尝试 bash 默认补全。如果在定义 compspec 时提供了 - default 选项，则使用 readline 的默认

补全将由 compspec（以及如果尝试，则由默认的 bash 补全）执行，未生成任何匹配项。

当 compspec 指明需要进行目录名补全时，可编程补全函数会调用 readline 在完成的指向目录的符号链接名称后添加斜杠，这取决于 readline `mark-directories` 变量的值，而不受 readline `mark-synlinked-directories` 变量设置的限制。

对动态修改补全提供了某些支持。这在与 `complete -D`指定的默认补全结合使用时最为有用。作为补全处理程序执行的 shell 函数可以通过返回退出状态 124 来指示应该重试补全。如果 shell 函数返回 124，并更改了与正在尝试补全的命令关联的 compspec（该命令在函数执行时作为第一个参数提供），则可编程补全将从头开始重启，尝试为该命令寻找新的 compspec。这允许在尝试补全时动态构建一组补全，而不是一次性加载所有。

例如，假设有一个 compspec 库，每个 compspec 都存储在一个与命令名相对应的文件中，以下默认补全函数将动态加载补全：

```
```
