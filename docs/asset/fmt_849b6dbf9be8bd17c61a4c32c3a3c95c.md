
# 编程技巧 577

当使用 `setq` 来给一个未通过 `Let` 的变量赋值时，该变量被视为全局变量。然而，在命名全局变量时必须小心，以防止它们与已存在的 Emacs 变量冲突。

## 定义你自己的函数

用户定义的函数使用 `defun` 定义。参数指定在函数名后的括号内。`interactive` 关键字使得函数通常情况下是可用的，因此可以通过 `Alt+X function.name` 调用函数。

```lisp
(defun func1() ;不带参数的函数
  (interactive)
  (function1 parameter1 parameter2 ...)
  (function2 parameter1 parameter2 ...)
  (function3 parameter1 parameter2 ...))
```

当函数请求用户输入参数值时，`interactive` 指令必须包含一个描述参数的字符串：

```lisp
(defun func1(p1 p2 p3) ;带参数的函数
  (interactive "nLine number:\nfile:")
  (function1 parameter1 parameter2 ...)
  (function2 parameter1 parameter2 ...)
  (function3 parameter1 parameter2 ...))
```

`interactive` 字符串使用 `\n` 分分为三部分，每部分由一个输入类型字符和一个简短的说明文本组成。在上面的示例中，函数开始后，Emacs 会提示用户输入行号、一些文本和一个文件名。在 `interactive` 中，可以使用以下字符指定输入类型：`\n` (数字), `s` (字符字符串), `b` (现有文本缓冲区), `B` (新文本缓冲区), `f` (现有文件), `F` (新文件)。

函数的返回值是函数内部执行的最后一个指令的返回值。

## 分支

大多数情况下，分支是用 `if` 构建的。语法如下：

```lisp
(if condition)
  (progn
    then block
    (function1 ...)
    (function2 ...))
  (progn
    optional else block
    (function1 ...)
    (function2 ...))
```

## 578 Emacs 配置与编程

如果 then 块只包含一个函数，可以省略 `progn`。条件大部分通过比较来构建，例如表示小于 5 的 `(< 5)`。条件可以通过 `(or cond1 cond2 cond3 ...)`、`(and ...)` 和 `(not cond)` 进行逻辑连接。

## 循环

循环的最简单形式是以 `while` 开始。与 `if` 不同，循环体不需要用 `progn` 标明。语法如下：

```lisp
(while condition)
(function1 ...)
(function2 ...)
```

## 区分 GNU Emacs 和 XEmacs

这两个版本的 Emacs 都会评估 `~/.emacs` 文件。然而，某些 Lisp 函数是取决于版本的，也就是说，并行使用这两个版本可能会导致冲突和语法错误。为了防止这种情况发生，你可以将 `~/.emacs` 中的代码分为三个部分：一个通用部分和每个编辑器各一个部分。所需的代码片段大致如下：

```lisp
; file "~/.emacs"
common part
code

(defvar running-emacs (string-match "XEmacs [Lucid]" emacs-version))

; 仅 GNU Emacs
(cond ((not running-emacs))
 code
)

; 仅 XEmacs
(cond (running-emacs))
 code
)
```

## 17.4 用户定义的键盘快捷键

基本上，为用户定义的命令或预定义命令分配新的键盘快捷键并不困难。因此，如果你经常需要某个 Emacs 命令，并且一直对使用 `Alt-X` 长长的调用感到恼恼，你就不再需要绝望了。

`global-set-key` 命令传递两个参数：方括号内的键盘快捷键和跟有单引号的函数名。

```lisp
(global-set-key [f1] goto-line)
```

在实践中，遗憾的是，用户定义键盘快捷键的分配并没有看起来那么简单：

- GNU Emacs 和 Emacs 对组合键盘快捷键有不同的语法。在 GNU Emacs 中，`Ctrl-X` 表示为 `[C-x]`；相比之下，在 Emacs 中表示为 `control x`。
- 某些键盘快捷键的默认含义几乎随着每个 Emacs 版本发生变化。（特别容易导致你发现的合理配置失效的是 `Del` 和 `Backspace`。每当你认为下一个版本到来将作废你所有努力时……）
- 当按下组合键时，X 服务器通常提供 Emacs 的代码高度取决于 X 配置（特别是 `xmodmap`）。这意味着 `Del` 在两个 Linux 发行版中的行为可能不同，即使具有相同的 Emacs 配置！
- 某些键被 Linux、X 服务器或窗口管理器占用，不再可以在 Emacs 中使用（例如，用于 `Ctrl-Alt-F7` 切换控制台）。
- 当在文本控制台中使用 Emacs 时，许多键盘快捷键完全无法处理。此外，键盘快捷键的含义还取决于 `loadkeys` 程序。（控制台中的键盘快捷键将在该上下文中进一步讨论。本章假设你在 X 环境下使用 Emacs。）
- 最后，必须遵守几项 Emacs 限制：许多键盘快捷键是预先分配的，将这些快捷键替换为自己的快捷键并不总是有意义。某些键会激活单独层级的快捷键，只能与其他键组合使用（例如 `Ctrl-X`、`Ctrl-C`、`Ctrl-H`）。

（注：原文后续存在大量重复内容，已根据要求对核心逻辑进行处理翻译）

# 582 EMACS 配置与编程

放弃上述列表中的第一个指令，而是为现有的 `expand-abbrev` 函数定义一个易于使用的键盘快捷键。通过这种方式，只有按下 F3 才会手动展开缩写。

```lisp
(global-set-key [F3] 'expand-abbrev)  ;手动展开缩写
```

通过下面的宏，缩写处理变得更有趣了：`expand-abbrev-or-dabbrev` 首先尝试使用缩写表中所包含的缩写。如果没有找到合适的缩写，该宏将调用 `dabbrevexpand` 进行动态展开。F3 可以同时用于预定义的缩写和动态展开。

```el
(defun expand-abbrev-or-dabbrev() ;使用 F3 展开缩写
  (interactive)
  (if not (expand-abbrev)) ;如果不存在缩写
    (progn
      (dabbrev-expand nil)))  ;动态展开
(global-set-key [F3] 'expand-abbrev-or-dabbrev)
```

上面的示例还展示了一个新 Lisp 函数的定义：该函数以关键字 `defun` 开头。通过交互命令，该函数被注册为 Emacs 命令，然后可以像所有其他命令一样，通过 `Alt+X` 调用。

# 更改大小写拼写

尽管 Emacs 有将单个字母、单词或任何其他区域转换为大写或小写的命令，但它仍然缺少一个可以简单反转现有拼写的命令：将每个大写字母替换为等效的小写字母，反之亦然。

生成的函数 `change-case` 较为复杂，它用于定义变量 `char`，该字符由 `char-after(point)` 存储当前位置。在随后的 `if` 语句中，它检查该字符的 ASCII 代码是否大于 64。所有字母（以及几个特殊字符）都是如此。如果是，则执行 `progn` 块。

此时，字符代码的第六位被改变（异或 32）。这会将 A（代码 65） 变为 a（代码 97），并使用 `insert-char` 将生成的字符插入到当前位置，同时删除原始字符。

`if` 条件的 `else` 部分仅在光标代码小于或等于 64 时执行（数字、空格、换行符、逗号等）。如果是这样，光标向前移动一个字符。由于 `else` 块只有一个函数，因此不需要 `progn` 块。

随后，新函数被赋值给键 F2。如果连续按下几次，光标会在文本中向前移动并更改所有字母。要撤销此类更改，必须在相关字母上再次按下 F2。该程序对德语变音也有效。

![](img/b30873dd3d753687a59253fb9ad26a0b_609_0.png)

# EMACS 编程示例 583

```elisp
(defun change-case()
;更改大小写
  (interactive) ;字符的拼写
  (let ((char (char-after (point)))) ;光标所在位置的字符
    (if (char > 64) ;代码 > 64，因此来自 'A'
```
