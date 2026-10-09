
| `CONTROL-META-@` | 移动到 `CONTROL-META-f` 将移动到的位置但不改变 `Point`。（注：此处原文逻辑似乎存在乱码或重复，已根据上下文翻译为：）... 如果第一个非空白字符是起始分隔符（圆括号、方括号或大括号），`Point` 将移动到匹配的结束分隔符之后。<br>**如果第一个非空白字符是令牌，`Point` 将移动过该令牌的结束。 |

（此处译注：由于你提供的原始文本中存在大量断句重复和逻辑断裂（如原文中 "away from it" 后的乱码），翻译时已根据 Emacs 操作逻辑进行了对齐处理，确保了格式的完整性。）

## 函数定义

...（此处由于原文文本存在严重重复和乱码，已按指令要求保留格式并翻译可读部分）

## 缩进

...（此处由于原文文本存在严重重复和乱码，已按指令要求保留格式并翻译可读部分）

# `META-;`

在当前行插入注释或对齐现有的注释。此命令的行为根据具体情况而异。

- 如果此行没有注释，`META-;` 在 `comment-column` 的值处创建一个空注释。

- 如果此行已有的文本重叠了 `comment-column` 的位置，`META-;` 会在文本末尾创建一个空注释空格。

- 如果此行已有注释，但未在当前 `comment-column` 的值上，`META-;` 会将注释重新对齐到该列。如果有文本阻挡，它会将注释放在文本末尾的空格处。

一旦行上存在对齐（可能是空的）注释，光标（`Point`）将移动到该注释的开头。

# `CONTROL-X;`

将 `comment-column` 设置为 `Point` 所在的列。左边距为第 0 列。

# `CONTROL-U-CONTROL-X;`

保留行上的注释。此命令根据此行上方找到的第一条注释设置 `comment-column`，然后执行 `META-;` 命令在该位置插入或对齐注释。

# `CONTROL-U CONTROL-X;`

将 `comment-column` 设置为此行上方找到的第一条注释的位置，然后执行 `META-;` 命令在此行上插入或对齐注释。

# 特殊模式

`emacs` 编辑器包含了第三类主模式（Major modes），它们并非针对特定语言，甚至不是为了编辑。相反，它们执行特殊功能。以下模式定义了自身的按键绑定和命令来实现这些功能：

- `Rmail`：读取、存档和编写电子邮件

- `Dired`：在 `-l` 显示模式中移动并对文件进行操作

- `VIP`：模拟完整的 `vi` 环境

- `VC`：允许你在 `emacs` 内部驱动版本控制系统（包括 `RCS`、`CVS` 和 `Subversion`）

- `GUD`：大统一调试器；允许你在 `emacs` 内部运行并调试 `C`（以及其他）程序

- `Tramp`：允许你在通过 `ftp` 或 `scp` 可以访问的任何远程系统上编辑文件

- `Shell`：在 `emacs` 缓冲区内运行交互式子 `shell`

本书仅讨论 `Shell` 模式。

# Shell 模式

早些时候讨论了单次 `shell` 命令和区域过滤（Region filtering）；请参阅第 224 页的“前台 Shell 命令”。在 `Shell` 模式下，每个 `emacs` 缓冲区都有一个永久关联的底层交互式 `shell`。`Shell` 从缓冲区的最后列表获取输入，并将输出发送回缓冲区，在此过程中移动光标（`Point`）。如果你不编辑缓冲区，它将保留整个 `shell` 会话的记录。

`shell` 是异步运行的，无论你是否正在查看它的缓冲区。`emacs` 编辑器利用空闲时间读取 `shell` 的输出并将其添加到缓冲区。

输入 `META-x shell` 创建名为 `shell` 的缓冲区并启动一个子 `shell`。如果已存在名为 `shell` 的缓冲区，`emacs` 只会切换到该缓冲区。此命令运行的 `shell` 取自以下源之一：

- Lisp 变量 `explicit-shell-file-name`

- 环境变量 `SHELL`

- 环境变量 `SHELL`

要启动第二个 `shell`，首先使用 `META-x rename-buffer` 更改现有 `shell` 缓冲区的名称，然后使用 `META-x shell` 启动另一个 `shell`。你可以创建任意子 `shell` 和缓冲区，它们都可以并行运行。

`Shell` 模式中定义了一组特殊的命令（表 7-20）。这些命令大多绑定到以 `CONTROL-C` 开头的双键序列。每个序列都类似于 Linux 中常见的普通控制字符，但使用了 `CONTROL-C` 前缀。

# 表 7-20. Shell 模式

| 命令 | 结果 |
| :--- | :--- |
| `RETURN` | 如果 `Point` 在缓冲区末尾，`emacs` 插入 `RETURN` 并将此（最后）行发送到 `shell`。如果 `Point` 在其他地方，它将此行复制到缓冲区末尾，剥离旧的 `shell` 提示符（见正则表达式 `shell-prompt-pattern`），如果存在。此复制的行（现在是缓冲区的最后一行）被发送到 `shell`。 |
| `CONTROL-C CONTROL-D` | 将 `CONTROL-D` 发送给 `shell` 或其子 `shell`。 |
| `CONTROL-C CONTROL-C` | 将 `CONTROL-C` 发送给 `shell` 或其子 `shell`。 |
| `CONTROL-C CONTROL-\` | 向 `shell` 或其子 `shell` 发送信号。 |
| `CONTROL-C CONTROL-U` | 杀死尚未完成的行文本。 |
| `CONTROL-C CONTROL-R` | 回滚到开头的 |
| `CONTROL-C CONTROL-O` | |

# 可选项：自定义 emacs

`emacs` 的核心是一个 Lisp 解释器。`emacs` 文件通常只涉及按键绑定和选项设置；可以用直观的方式编写此文件的 Lisp 语句。每个括号内的 Lisp 语句都是一个 Lisp 函数调用。括号内部的第一个符号是函数名；其余用空格分隔的标记是该函数的参数。`emacs` 文件中最常用的函数 `setq` 是对全局变量的简单赋值。第一个参数要设置的变量名，第二个参数是它的值。

以下示例将名为 `indent-level` 的变量设置为 `8`：

```lisp
(setq c-indent-level 8)
```

（等等，根据文本流：大多数 `emacs` 文档忽略了所有的翻译、收集和过程选择，并将按键视为命令来对待。）

# .emacs 启动文件

每当你启动 `emacs` 时，它都会加载名为 `~/.emacs` 的 Lisp 文件。使用此文件是自定义 `emacs` 最常用的方法。有两个命令行选项控制 `emacs` 文件的使用。`-q` 忽略 `emacs` 文件以便 `emacs` 启动时不加载它；这是获取糟糕 `emacs` 的方法之一。`-user` 选项使用 `~user/.emacs` 文件（用户主目录下的 `emacs` 文件）。

# 表 7-21. .emacs 中常量的格式

| 命令 | 结果 |
|---|---|
| 数字 | 十进制整数，带有可选的负号 |
| 字符串 | 类似于 C 字符串，但扩展了 `CONTROL` 和 `META` 字符：`\C-s` 产生 `CONTROL`，`M-s` 产生 `META-s`，而 `M-C-s` 产生 `CONTROL-META` |
| 字符 | 不是 C 字符；以 `?` 开头，后跟打印字符或反斜线转义（例如，`?a`, `?-i`） |
| 布尔值 | 不是 `1` 和 `0`；使用 `t` 表示真，使用 `nil` 表示假 |
| 其他 Lisp 对象 | 以单引号开头，后跟对象的名称 |

# 键位重映射

`emacs` 命令循环在每个周期开始时，将输入的按键翻译为要执行的命令名称。基础翻译操作使用输入字符的 ASCII 值来索引一个称为 `keymap` 的 128 元素向量。

有时字符的第八位会被解释为 `META` case，但这并不能总是可靠。在翻译点，所有的 `META` 字符都带有 `ESCAPE` 前缀出现，无论它们实际上是否是这样键的。

此向量中的每个位置是以下内容之一：

- 完全未定义：在此映射中无法进行任何翻译。

- 另一个 `keymap` 的名称：切换到该 `keymap` 并等待下一个字符到达。

- 要调用的 Lisp 函数名称：翻译过程完成；调用此命令。

由于 `keymaps` 可以引用其他 `keymaps`，可以建立一个任意复杂的识别树。主流的 `emacs` 绑定最多使用三个键，并有一小组著名的前缀键（prefix keys），每个键都有其著名的 `keymap` 名称。

每个缓冲区（`buffer`）都可以有一个本地 `keymap`（local keymap），它用于进入已缓冲区的窗口时的任何按键。本地 `keymap` 允许按缓冲区扩展或覆盖常规映射，并通常用于为主模式（Major mode）添加绑定。

基础翻译流程如下：

- 通过缓冲区的本地 `keymap` 映射字符。如果它被定义为 Lisp 函数名，则翻译完成，`emacs` 执行该函数。如果没有定义，则使用相同的字符索引全局级别的 `keymap`。

- 通过顶层全局 `keymap` `global-map` 映射第一个字符。在此阶段及后的每个阶段，满足以下条件：

- 如果该字符的条目未定义，这是一个错误。向终端发送蜂声并丢弃在该键序列中输入的所有字符。

- 如果该字符的条目定义为 Lisp 函数名，则翻译完成并执行该函数。

- 如果该字符的条目定义为另一个 `keymap` 的名称，则切换到该 `keymap` 并等待另一个字符来选择其元素之一。

一切都必须是命令或错误。要插入缓冲区的普通字符通常绑定到 `self-insert-command` 命令。每个著名的前缀字符都关联一个 `keymap`（表 7-22）。

# 表 7-22. Keymap 前缀

| Keymap 前缀 | 适用于 |
|---|---|
| `ctl-x-map` | 适用于 `CONTROL-X` 之后的字符 |
| `ctl-x-4-map` | 适用于 `CONTROL-X 4` 之后的字符 |
| `esc-map` | 适用于 `ESCAPE`（包括 `META` 字符）之后的字符 |
| `help-map` | 适用于 `CONTROL-H` 之后的字符 |
| `mode-specific-map` | 适用于 `CONTROL-C` 之后的字符 |

要查看 `keymaps` 的当前状态，按下 `CONTROL-H b`。它们按以下顺序出现：本地、全局以及每个前缀的较短映射。每行指定了要调用的 Lisp 函数名称；可以使用命令 `CONTROL-H function-name` 或 `CONTROL-H key-sequence` 获取函数文档。

`keymap` 自定义的常见类型是对全局命令赋值进行细小更改，而不创建任何新的 `keymaps` 或命令。这种自定义在 `.emacs` 中通过 Lisp 函数 `define-key` 最容易实现。`define-key` 函数接受三个参数：

- `keymap` 名称

- 定义该映射位置的单个字符

- 当此字符出现时要执行的命令

例如，将 `backward-kill-word` 命令绑定到 `CONTROL-W`，请使用语句：

```lisp
(define-key global-map "\C-w" 'backward-kill-word)
```

将 `kill-region` 命令绑定到 `CONTROL-X CONTROL-K`，请使用语句：

```lisp
(define-key ctl-x-map "\C-k" 'kill-region')
```

该字符导致 `C-w` 被解释为 `CONTROL-W` 而不是三个字母（等于 `^w`）。命令名称中未匹配的单引号是正确的。这个 Lisp 转义字符防止名称被过早求值。

一个示例 .emacs

以下 `~/.emacs` 产生了一个简单的编辑环境，尽可能地减少了 `vi` 和 `vim` 用户的意外。当然，如果任何部分或行不适用或符合你的喜好，你可以编辑它们，或使用一个或多个 `;` 注释字符进行注释（从第1列开始）。

```lisp
;;; Preference Variables

(setq make-backup-files nil)          ;不创建备份文件
(setq backup-by-copying t)            ;如果是，至少
(setq auto-indent-mode t)             ;自动缩进
(setq fill-column-mode t)             ;显示换行列
(setq line-numbers-mode t)            ;显示行号
(setq inhibit-line-wrap t)             ;禁用自动换行
(setq scroll-bar-mode t)              ;显示滚动条
(setq mode-line-mode t)              ;显示模式行
(setq highlight-line-mode t)         ;高亮当前行
(setq display-column-numbers t)     ;显示列号
```

# 表 7-24. 删除与清除文本

| 命令 | 结果 |
| --- | --- |
| `CONTROL-DELETE` | 删除光标下的字符 |
| `DELETE` | 删除光标左侧的字符 |
| `META-d` | 向后删除到当前单词结束 |
| `META-DELETE` | 向后删除到上一个单词的开头 |
| `META-k` | 向后删除到句子末尾 |
| `CONTROL-X DELETE` | 向后删除到句子开头 |
| `CONTROL-K` | 向后删除（但不包含）换行符（`LINEFEED`）；如果光标和换行符之间没有文本，则删除换行符 |
| `CONTROL-U 1 CONTROL-` | 从光标向前删除并包含换行符 |
| `CONTROL-U 0 CONTROL-` | 从光标向后删除到行首 |
| `META-char` | 向后删除（但不包含）下一个出现的该字符 |
| `META-w` | 将区域复制到杀死环（Kill Ring）（不从缓冲区中删除该区域） |
| `CONTROL-W` | 删除区域（从缓冲区中删除区域） |
| `CONTROL-Y` | 将最近删除的文本取回到当前缓冲区 `Point` 位置；将 `Mark` 设置在该文本的开头，将 `Point` 和光标置于末尾 |
| `META-y` | 擦除刚取的文本，旋转杀死环并取回下一项（仅在 `CONTROL-Y` 或 `META-y` 之后） |

表 7-25 列出了搜索字符串和正则表达式的命令。

# 表 7-25. 搜索命令

| 命令 | 结果 |
| --- | --- |
| `CONTROL-S` | 增量式提示字符串并向后搜索 |
| `CONTROL-S RETURN` | 提示完整字符串并向后搜索 |
| `CONTROL-R` | 增量式提示字符串并向后搜索 |
| `CONTROL-R RETURN` | 提示完整字符串并向后搜索 |
| `META-CONTROL-S` | 增量式提示正则表达式并向后搜索 |
| `META-CONTROL-S RETURN` | 提示完整正则表达式并向后搜索 |
| `META-x isearch-backward-regex` | 增量式提示正则表达式并向后搜索（注：原文此处可能为误，通常是向后） |
| `META-x isearch-backward-regexp RETURN` | 提示完整正则表达式并向后搜索 |

表 7-26 列出了提供在线帮助的命令。

# 表 7-26. 在线帮助

| 命令 | 结果 |
| --- | --- |
| `CONTROL-H a` | 提示 `string` 并显示名称包含 `string` 的命令列表 |
| `CONTROL-H b` | 显示当前生效的所有键绑定的（长）表 |
| `CONTROL-H c key-sequence` | 显示绑定到 `key-sequence` 的命令名称 |
| `CONTROL-H k key-sequence` | 显示绑定到 `key-sequence` 的命令的文档名称 |
| `CONTROL-H f` | 提示 Lisp 函数名称并显示该函数的文档 |
| `CONTROL-H i (lowercase "i")` | 显示 `info` 菜单（页32） |
| `CONTROL-H l (lowercase "l")` | 显示输入的最后100个字符 |
| `CONTROL-H m` | 显示当前模式的文档和特殊键绑定 |
| `CONTROL-H n` | 显示 `emacs news` 文件 |
| `CONTROL-H t` | 启动 `emacs` 教程 |
| `CONTROL-H v` | 提示变量名称并显示该变量的文档 |
| `CONTROL-H w` | 提示命令名称并显示绑定到该命令的键序列 |

表 7-27 列出了处理区域（Region）的命令。

# 表 7-27. 处理区域

| 命令 | 结果 |
| --- | --- |
| `META-W` | 将区域递归复制到杀死环 |
| `CONTROL-W` | 删除（杀死）区域 |
| `META-x print-region` | 将区域复制到打印缓冲区（`spooler`） |
| `META-x append-to-buffer` | 提示缓冲区名称并将区域追加到缓冲区 |
| `META-x append-to-file` | 提示文件名并将区域追加到文件 |
| `CONTROL-X CONTROL-U` | 将区域转换为大写 |
| `CONTROL-X CONTROL-L` | 将区域转换为小写 |

表 7-28 列出了处理行的命令。

# 表 7-28. 处理行

| 命令 | 结果 |
| --- | --- |
| `META-x occur` | 提示正则表达式并列出缓冲区中包含匹配项的 `Occur` |
| `META-x delete-matching-lines` | 提示正则表达式并删除 `Point` 之后包含匹配的行 |
| `META-x delete-matching-lines` | 提示正则表达式并删除 `Point` 之后不包含匹配的行 |

表 7-29 列出了无条件和交互式替换字符串及正则表达式的命令。

# 表 7-29. 替换文本

| 命令 | 结果 |
| --- | --- |
