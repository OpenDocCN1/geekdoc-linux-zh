
- `accept-line` (Newline): 无论光标在哪里都接受该行。如果此行非空，则根据 `HIST-CONTROL` 变量的状态将其添加到历史列表。如果该行是修改过的，则将历史恢复到原始状态。

- `previous-history` (C-p): 从历史列表中获取上一个命令，在列表中向后移动。

- `next-history` (C-n): 从历史列表中获取下一个命令，在列表中向前移动。

- `beginning-of-history` (M-<): 移动到行首。

- `end-of-history` (M->): 移动到输入历史的末，即当前输入的行。

- `reverse-search-history` (C-r): 从当前行开始向后搜索，并在历史中“向上”移动，这是一种增量搜索。

- `forward-search-history` (C-s): 从当前行开始向前搜索，并在历史中“向下”移动，这是一种增量搜索。

- `non-incremental-reverse-search-history` (M-p): 使用非增量搜索提供的字符串，从当前行开始在历史中向后搜索。

## 修改文本命令

- `delete-char` (C-d): 删除光标下的字符。

- `backward-delete-char` (C-h): 删除光标前的字符。

- `delete-horizontal-space`: 删除所有空格和制表符。默认情况下未绑定按键。

- `kill-line` (C-k): 删除从光标位置到行尾的文本。

- `kill-word` (C-w): 删除光标前的单词，使用空格作为边界。单词边界与 `backward-kill` 不同。

- `kill-word` (M-d): 删除从光标到结束。默认情况下，如果是单词，则删除到下一个单词结束。

- `backward-kill-word` (M-_): 删除光标后的单词。

- `yank` (Y-y): 将删除环顶端的内容到光标处。取出新的顶端。

- `yank-pop` (M-y): 弹出。

## 数字参数

- `digit-argument` (M-0, M-1, ...): 将此数字添加到正在累计的参数中，或开始新参数。M- 开始负参数。

- `universal-argument`: 每次执行此命令时，参数计数乘以四。初始计数为一，因此第一次执行时乘以四。默认情况下未绑定按键。

## 补全

- `complete` (TAB): 尝试对光标前的文本进行补全。Bash 补会将文本视为变量（如果以 `$` 开头）、用户名（如果以 `#` 开头）、主机名（如果以 `@` 开头）或命令（包括别名和函数）。如果这产生了匹配，则将尝试文件名补全。

- `possible-completions` (M-?): 列出光标处可能的补全项。

- `insert-completions`: 插入之前通过 `possible-completions` 生成的所有光标处补全项。默认情况下未绑定按键。

- `complete-filename` (M-/): 尝试对光标前的文本进行文件名补全。

# 第一部分：用户命令

## completion

- `possible-filename-completions` (C-x /)

- `complete-username` (M-')

- `possible-username-completions` (C-x ')

- `complete-variable` (M-$)

- `possible-variable-completions` (C-x $)

列出光标之前文本可能的补全，将其视为文件名。

对光标之前的文本尝试补全，将其视为用户名。

列出光标之前文本可能的补全，将其视为用户名。

对光标之前的文本尝试补全，将其视为 shell 变量。

列出光标之前文本可能的补全，将其视为 shell 变量。

- `complete-hostname` (M-#)

- `possible-hostname-completions` (C-x #)

- `complete-command` (M-|)

对光标之前的文本尝试补全，将其视为主机名。

列出光标之前文本可能的补全，将其视为主机名。

对光标之前的前的文本尝试补全，将其视为命令。

命令补全尝试按照顺序依次匹配别名、保留字、shell 函数、内置命令（builds），最后是可执行文件名。

- `possible-command-completions` (C-x !)

列出光标之前文本可能的补全，将其视为命令名。

对光标之前的文本尝试补全，通过对比历史列表中的行查找可能的补全。

- `dynamic-complete-history` (M-TAB)

- `complete-into-braces` (M-{})

执行补全并返回括号内的可能补全列表，使列表对 shell 可用。（参见手册前面的“大括号扩展”。）

## 键盘宏

- `start-kbd-macro` (C-x ()

- `end-kbd-macro` (C-x ))

- `call-last-kbd-macro` (C-x e)

开始保存输入到当前键盘宏中的字符。

停止保存输入到当前键盘宏中的字符并保存定义。

通过让宏中的字符看起来就像是输入的一样，重新执行上定义的宏。

## 杂项

- `re-read-init-file` (C-x C-r)

- `abort` (C-g)

- `do-uppercase-variable` (M-a, M-B,...)

- `prefix-meta` (ESC)

- `undo` (C-x C-u)

- `revert-line` (M-r)

读取初始化文件的内容，并合并其中找到的变量或赋值。

取消当前编辑并响起终端铃（取决于 `bell-style` 的设置）。

运行绑定到大写字符的命令。

对输入的文本进行元化。ESC-f 等于 Meta-f。

增量撤销，每行单独记忆。

撤销此行的所有更改。这类似于使用 `undo` 命令返回到初始状态。

- `tilde-expand` (M-)

- `dump-functions`

将所有函数及其键绑定打印到输出流。如果提供了数字参数，输出的格式将可以作为输入文件的一部分。

- `display-shell-version` (C-x C-v)

- `emacs-editing-mode` (C-e)

显示关于 bash 当前状态的版本信息。

在 vi 模式下，这将切换到 emacs 编辑模式。

## 历史 (HISTORY)

在交互模式下，shell 提供命令历史记录，即之前输入的命令列表。最后 `SIZE` 条（默认 500 条）命令的文本保存在历史列表中。shell 在进行参数和变量扩展（参见手册前面的“扩展”）之前，但在历史扩展之后将每个命令存储在历史列表中，受 shell 变量 `command_oriented`、`history` 和 `HISTCONTROL` 的值的影响。启动时，历史从变量 `HISTFILE` 指定的文件（`./bash_history`）中初始化。如有必要，`HISTFILE` 会被截断为包含不超过 `HISTSIZE` 行。可以使用内置命令 `-c`（参见手册后面的“内置命令”）来编辑或重新执行历史列表的一部分。内置命令 `history` 可用于显示历史列表并操作历史。当使用命令行编辑时，每个目录下的命令都可用，以访问历史列表。当交互式 shell 启动时，最后 `HISTSIZE` 行将从历史列表复制到 `HISTFILE`。如果 `HISTFILE` 未设置或历史记录不可写，则历史不会被保存。

## 历史扩展 (HISTORY EXPANSION)

shell 支持类似于 bash 中历史扩展的句扩展功能。本节描述了什么是语法特征。此功能在交互式 shell 中启用，可以使用 `set` 内置命令的选项禁用。（参见手册后面的“内置命令”）。非交互式 shell 不执行历史扩展。

历史扩展在读取一行后立即执行，在 shell 将其拆分为单词之前。它包含两个部分：第一部分是确定在替换时使用之前历史记录中的哪一行；第二部分是选择行的一部分包含在当前行中。从之前的历史选中的行是事件（event），被处理的行部分是单词（words）。我们在输出时，行被拆分为单词，但许多被引号围绕的元字符单词被视为一个单词。反斜杠（\）和单引号可以引用历史转义字符，这是默认设置。

shell 控制历史扩展机制使用的各种字符。（参见手册前面的“变量”中的元字符描述。）

## 事件标识符 (EVENT DESIGNATORS)

事件标识符是：

- `!!` 上一个命令。

- `!` 最后一个命令。

- `!n` 倒数第 n 个命令。

- `!string` 以字符串开头的命令。

- `!?string` 以字符串结尾的命令。

- `-!string` 包含字符串的最后一个命令。

- `!` 列表中的第一个命令。

- `!n` 列表中第 n 个命令。

- `!string` 列表中以字符串开头的命令。

- `!?string` 列表中以字符串结尾的命令。

- `-!string` 列表中包含字符串的最后一个命令。

## 单词标识符 (WORD DESIGNATORS)

shell 允许：

- `$` 第一个参数。

- `$$` 最后一个参数。

- `$n` 倒数第 n 个参数。

- `$?` 以字符串开头的参数。

- `$*` 所有参数。

- `$#` 第一个参数。

- `@` 所有参数。
