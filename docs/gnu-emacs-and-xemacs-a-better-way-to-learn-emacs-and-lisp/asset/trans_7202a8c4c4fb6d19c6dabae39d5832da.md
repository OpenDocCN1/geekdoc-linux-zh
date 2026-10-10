

## XEmacs 专属鼠标操作

- **按钮 3**：主要模式鼠标菜单。
- **M-Ctrl-按钮 3**：缓冲区鼠标菜单。
- **Ctrl-按钮 1**：创建选区并将其插入到光标处。
- **Shift-按钮 1**：扩展选区。
- **Ctrl-按钮 2**：将光标定位在鼠标点击处，并将选中的区域移动至此。
- **Ctrl-Shift-按钮 1**：使用鼠标剪切选区并插入，但不移动光标。

## 帮助键

这些是最常用的帮助键。Emacs Info 手册的帮助章节描述了许多其他帮助键。

- **Ctrl-h m**：简要描述当前激活的主要模式和次要模式。
- **Ctrl-h b**：列出当前激活的按键绑定。
- **Ctrl-h i**：启动 Info 帮助系统。
- **Ctrl-h a**：Apropos 命令；正则表达式帮助（参见第 23 章）。
- **Ctrl-h c**：按键命令的简要描述。
- **Ctrl-h k**：按键命令的详细描述。
- **Ctrl-h t**：启动交互式 Emacs 教程。
- **Ctrl-h v**：Lisp 变量的描述——默认情况下，描述光标处的变量。
- **Ctrl-h f**：Lisp 函数的描述——默认情况下，描述光标处的函数。
- **Ctrl-h p**：通过关键词帮你查找 Emacs 软件包。
- **Ctrl-h K 命令名**：显示某命令的按键绑定信息。
- **Ctrl-h n**：显示你的 Emacs 或 XEmacs 版本中所做的更改，最近的更改显示在首位。

## 退出 Emacs

- **Ctrl-x Ctrl-c**：结束 Emacs 会话。

## 附录 B：Mini-buffer 命令

Emacs 拥有大量的可用命令，鉴于标准 101 键键盘的限制，不可能为所有命令分配可用的快捷键。因此，那些较不常用且偏门的命令是通过在命令名前添加 M-x 前缀来执行的，这表示 Emacs 期望在 mini-buffer 中接收用户输入的命令。按下 M-x 前缀后，后续的按键输入将显示在 mini-buffer 中，而不是主编辑窗口中。你可以通过按 Enter 键执行命令。之后，你的按键输入将像往常一样指向编辑窗口。

以下是 mini-buffer 命令中最有用的一些列表。

- **M-x bookmark-save**：将所有当前书签保存到默认书签文件。
- **M-x bookmark-load**：提示输入要加载的书签文件名。按 Enter 键将加载默认书签文件。
- **M-x bookmark-write**：你可以指定一个文件名，所有当前书签将保存至该文件。
- **M-x bookmark-delete**：按名称删除书签。系统会在 mini-buffer 中提示你。
- **M-x bookmark-insert**：在光标处插入书签所指向文件的完整内容。
- **M-x bookmark-insert-location**：在光标处插入书签所指向文件的文件名。
- **M-x customize**：打开顶层 Customize 缓冲区，其中包含指向所有 Customize 组的链接。如果你已经知道要自定义的组或变量，请使用以下 customize 命令之一。
- **M-x customize-group**：系统会要求你在 mini-buffer 中输入组名。如果不确定完整名称，Tab 补全功能将非常有帮助。
- **M-x customize-variable**：与前面的命令类似，系统会提示你输入具体的变量。在所有 mini-buffer 命令中，Tab 补全功能都可用。
- **M-x customize-face**：系统会提示你输入一个 face 的名称（一种字体和其他显示特征的组合，如前景和背景颜色）。一个好的入门选择是默认 face。

| 命令 | 描述 |
| :--- | :--- |
| **M-x fill-region** | 在选中的区域内对长行进行换行，使其不超过填充列，默认设置为第 70 列。 |
| **M-x goto-line** | 允许你在 mini-buffer 中输入行号，按 Enter 键，光标即移动到该行。 |
| **M-x ispell-region** | 在选中的区域运行 ispell 拼写检查器。 |
| **M-x ispell-buffer** | 检查整个缓冲区的拼写。 |
| **M-x load-library** | 输入 Lisp 文件名（不含 .el 或 .elc 后缀）后，该文件将被加载。该文件必须位于你的 load-path 中的某个目录中，例如 site-lisp 目录。这是临时尝试某个扩展的一种方式。 |
| **M-x name-last-kbd-macro** | 为最近创建的键盘宏命名。此名称仅在 Emacs 会话期间有效。 |
| **M-x insert-kbd-macro** | 提示输入你已创建并命名的宏的名称。该宏的 Lisp 定义将被插入当前缓冲区。通常用于在 .emacs 文件中插入宏定义，以便在后续会话中可用。 |
| **M-x recover-file** | 当 Emacs 因系统或 Emacs 崩溃而意外终止时使用的命令。系统会提示你输入文件名。如果找到与该文件对应的自动保存文件，它将重命名该文件，替换最后保存的版本。 |
| **M-x recover-session** | 前面命令的扩展，在崩溃时有多个已修改但未保存的缓冲区时非常有用。你可以使用此命令选择要恢复哪些自动保存文件。 |
| **M-x revert-buffer** | 丢弃对缓冲区的所有更改，并从磁盘重新加载原始未修改的文件，即最后保存的版本。 |
| **M-x server-start** | 启动 Emacs 编辑服务器，这是一个后台实用程序，允许你从命令行或其他应用程序将文件加载到已在运行的 Emacs 会话中。该用户程序称为 emacsclient。 |
| **M-x gnu-serve-start** | M-x server-start 的 XEmacs 等价命令。与用户程序 gnuclient 配合使用。 |
- **M-x shell**：打开一个 shell 缓冲区，类似于 xterm 但在 Emacs 窗口中运行。 |
- **M-x write-abbrev-file**：提示输入文件名，然后将所有当前缩写保存到该文件。 |
- **M-x read-abbrev-file**：加载缩写文件并使内容可用。 |
- **M-x list-abbrevs**：显示当前可用的缩写及其展开内容。 |
- **M-x edit-abbrevs**：打开包含你当前缩写的缓冲区。你可以添加、编辑和删除条目。 |

## 附录 C：其他模式命令

尽管主要模式通常在加载相应类型的文件时初始化，但有时需要手动加载。以下是常用模式的 mini-buffer 命令。

- **M-x auto-fill-mode**：启用自动换行。
- **M-x font-lock-mode**：在当前缓冲区中启用语法高亮。
- **M-x line-number-mode**：一个次要模式，用于在模式行中显示行号。
- **M-x column-number-mode`：类似 `M-x line-number-mode` 的模式。在模式行中显示列号。
- **M-x abrev-mode**：切换单词缩写模式。
- **M-x auto-compression-mode**：切换文件自动压缩和解压缩功能。
- **M-x transient-mark-mode**：切换选中区域的高亮显示（仅限 GNU Emacs）。
- **M-x tool-bar-mode**：切换 GNU Emacs 21 工具栏。
- **M-x rmail**：启动 Rmail 邮件阅读器。
- **M-x vm**：启动 VM 邮件阅读器。
- **M-x gnus**：启动 Gnus，邮件和新闻阅读器。
- **M-x cc-mode**：C 和 C++ 文件的主要模式。
- **M-x cperl-mode**：Perl 编程语言的主要模式。
- **M-x python-mode**：Python 编程语言的主要模式。
- **M-x Lisp-mode**：编写 Lisp 程序的主要模式。
- **M-x TeX-mode**：编写 TeX 文件的主要模式。
- **M-x latex-mode**：用于编写 LaTeX 文件的 TeX 模式变体。

## 附录 D：Emacs 与国际化

Emacs 最初是由英语使用者设计并使用的，但不久之后，世界各地的用户开始采用该编辑器。采用单字节编码的 ASCII 字符集非常适合英语字母和其他字符。其他罗曼字母语言需要 ASCII 变体字符集，以便显示带变音符号和分音线字符。

> 每个字符集在用于计算机程序或通过传输网络之前都需要进行编码。为处理世界各地用于表示各种脚本的字符集的不同需求，各种编码系统应运而生。当每个字符在计算机内存中均可用不超过 8 位（二进制位）表示时，特定的字符编码被归类为“单字节”（unibyte），这相当于 1 字节。标准 ASCII 字符集仅使用 8 位中的 7 位。多字节字符编码用于表示汉语、日语等语言所使用的脚本，这些语言字符众多，单个字节不足以表示。这些脚本每个字符使用 2 个字节。

![](img/c8827ea52a0796def3f6891892ed9d3a_523_0.png)

音节文字和图形字符脚本（如用于表示东方语言的脚本）需要更复杂的解决方案。虽然为这些语言开发了多字节或 16 位字符集编码，但需要一种方法让 Emacs 能够利用它们。Mule 项目最初是一个独立的项目，最终与 Emacs 合并，现在构成了 Emacs 显示和接收世界主要语言所用大多数脚本输入的核心能力。

### 设置

你安装的 Emacs 版本可能能够也可能无法显示替代字符集。Emacs 和 XEmacs 各自拥有处理此选项的方法。由于 Linux 发行版打包编辑器的差异，情况变得复杂。通常，Mule 和非 Mule 软件包都可用。默认安装是非 Mule 版本。

你可以很容易地查明你的 Emacs 是否支持 Mule。你的菜单栏上是否有 Mule 菜单？在 GNU Emacs 21 中，Mule 是 Options 下的一个子菜单。如果此菜单缺失，请检查你的 ~/.emacs 文件中是否有禁用多字节字符支持的行，如下例所示：

```lisp
(setq-default enable-multibyte-characters nil)
```

注释掉此行并重启 Emacs。现在 Mule 菜单应该可见了。此变量仅对 GNU Emacs 有效。

