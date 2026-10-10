
某方法可能无法正常工作，尽管文档声称可以。有时，尝试三种加载方法中的另一种可能有助于让该模式在你这里正常运行。

### 加载

加载 Lisp 文件最基本的方法是使用内置函数 `load`。一个 `load` 语句如下所示：

```lisp
(load 'file-name)
```

`load` 首先查找 `file-name.elc`；如果找不到，则查找 `file-name.el`；如果该文件也不存在，则直接使用 `file-name`。

使用此函数的缺点是文件会被立即加载，即使它直到稍后才需要。对于需要快速可用的频繁使用的 Lisp 文件，使用 `load` 是合适的。由于下两种方法具有更大的灵活性，它们更常用。

### 自动加载

可能有一些你很少使用但需要在需要时仍可访问的模式。自动加载这些模式是理想的技术，因为模式直到你通过键盘按键或迷你缓冲区命令调用时才会加载。`autoload` 是一个内置函数。一个 `autoload` 命令如下所示：

```lisp
(autoload 'follow-mode "follow")
```

这是一个简单的例子；`autoload` 命令的完整语法如下：

```lisp
(autoload function-name Lisp-file docstring interactive type [最后三个是可选的])
```

上面展示的 `follow-mode` 例子只使用了语法示例中的前两个元素。它省略了三个可选开关，因为当你自动加载位于加载路径目录中的 Lisp 文件时，这些开关是不必要的。当请求时，Autoload 使用 `load` 函数实际加载文件，因此如上所述，如果存在 `.elc` 文件则使用它。

上述 autoload 语句翻译成英文可能读起来像这样：

> “在加载路径上查找名为 `follow.elc`、`follow.el` 或 `follow` 的 Emacs Lisp 文件，首选第一个。在文件中查找名为 `follow-mode` 的函数，并准备好在用户请求时加载该函数。”

如果仅存在前两个必需参数，`autoload` 认为缺失参数的值为 nil。换句话说，没有 docstring，函数不是交互式的，并且 `type` 参数指向一个函数（默认值）。

以下是从加载 `dictionary`-mode 中两个函数而非 `entire` 文件的 `~/.emacs` 文件中的两个示例：

```lisp
(autoload 'dictionary-search "dictionary"
 "Ask for a word and search it in all dictionaries" t)

(autoload 'dictionary-search-word-at-point "dictionary"
 "Search the word at point in all dictionaries" t)
```

这两个表达式从 `"dictionary"` 中加载函数，该函数被 `autoload` 扩展为 `"dictionary.elc"`。如果函数无法在 `load-path` 上找到该名称的文件，它会改为查找 `dictionary.el`。表达式末尾的 `t` 旨在使 `dictionary` 函数变为 `interactive`（交互式）——`t` 表示是或真。这意味着按下 M-x 并输入

`dictionary-search`

将导致 `dictionary` 搜索函数从 `dictionary.elc` 加载，这会导致迷你缓冲区提示 Search word:（搜索单词：）

### 需求

某些软件包是你日常工作的必需品；你希望在 Emacs 启动时加载它们，并在此后快速可用。`require` 函数专为这种需求而设计。一个 `require` 表达式可以像这样简单：

```lisp
(require 'clipper)
```

该函数不会显式加载函数或 Lisp 文件。它加载一个 `feature`（特性），这是 Emacs 术语，意为一组函数和/或变量。

完整语法是

```lisp
(require '[feature-symbol] ['file-name])
```

第二个参数是可选的；如果缺失，该函数将查找与 `feature` 同名的文件名。

为了使用 `require`，Lisp 文件中必须存在如下的语句：

```lisp
(provide 'clipper)
```

函数 `provide` 将其参数给定的 `feature-symbol` 添加到名为 `features` 的 Emacs 变量中，该变量是可用特性的列表，这些特性在当前 Emacs 会话中可用。

require 的一个优点是，该函数首先检查文件是否已经加载；如果已加载，require 不做任何事。这防止了文件在一个会话中被加载多次。

require 通常用于在 Lisp 文件中使存在于另一文件中的特性可用。require 和 autoload 函数之间的区别在于，autoload 仅将文件名及其 docstring 加载到内存中，将实际加载推迟到明确请求时进行。

使用这三个函数中的哪一个通常由软件包作者决定。源文件中被注释掉的文档通常提供了可以插入到你的 ~/.emacs 文件中的示例行。如果你难以说服软件包加载或自动加载，尝试其他函数是值得的。

### 从另一个模式派生模式

模式派生是一种节省时间的技术。这是一个常见情况：你需要一种模式来使编辑某种类型的文件更容易。为另一种类型的文件设计的模式几乎是你需要的，从头开始似乎很可惜。你可以从另一个模式派生一个新模式，保留旧模式的核心功能，但更改某些特性，使新模式按你需要的方式工作。这有助于防止“我是不是在重新发明轮子？”的感觉。

使这成为可能的是一个名为 define-derived-mode 的 Lisp 软件包。它具有简单的语法：

```lisp
(define-derived-mode new-mode's-name old-mode's-name mode-line-string
docstring
expression-1
expression-2
etc.)
```

以下是来自 gametree.el 的一个示例，这是 Emacs 游戏模式附带的一个文件：

```lisp
(define-derived-mode gametree-mode outline-mode "GameTree"
"Major mode for managing game analysis trees.
Useful to postal and email chess (and, it is hoped, also checkers, go, shogi, etc.) players, it is a slightly modified version of Outline mode.

\\{gametree-mode-map}"
(auto-fill-mode 0)
(make-variable-buffer-local 'write-contents-hook)
```

```lisp
(add-hook 'write-contents-hooks 'gametree-save-and-back-layout!)

;;; Key bindings

(define-key gametree-mode-map "\C-c\C-j" 'gametree-break-line-here)
[etc]
```

第一行设定了场景：调用 `define-derived-mode` 使用 `outline-mode` 作为基础创建新模式 `gametree-mode`。`mode-line-string` 是一段简短的描述性文本，显示在模式行中——在这种情况下是“Gametree”。

接下来的三行是 docstring，即大多数编写良好的模式中发现的可选内置文档。注意第一行过早断开（在 `name` 之后立即断开）。这是 Emacs 的惯例，在单独一行上以单句摘要开始 docstring。apropos 帮助设施查找该摘要行，如果在 `gametree-mode` 加载后按下 `C-h l`，则会显示它。docstring 以以两个反斜杠开头的奇特表达式结束。这是 Emacs 内部帮助系统理解的代码；它意味着“评估大括号之间的表达式，并用结果替换此行。”如果在 `gametree-mode` 中有一个缓冲区，并且你通过按下 `C-h m` 召唤模式帮助，Help 缓冲区将看起来像 **图 11.2**。

![](img/c8827ea52a0796def3f6891892ed9d3a_215_0.png)

图 11.2 Gametree 帮助

注意 docstring 如何被修改：反斜杠前缀的行消失了，键绑定列表 (`gametree-mode-map`) 在其位置被替换。紧随 docstring 之后的是表达式的实际主体，由一系列函数定义和/或变量声明组成。此例中的 define-key 函数使用了一种显示键绑定的替代方式。使用反斜杠转义字符代替前一章中说明的括号系统。此键绑定等同于 [(control c) (control j)]。

### 修改模式

迟早，每个 Emacs 用户都会想到“我希望有某种模式使这种编辑更容易！”。也许你在编辑新类型的文件，并希望有用于该文件类型的字体锁定，或能加速重复任务的新的键命令。

我愿意打赌，许多有经验的 Lisp 黑客在从头创建新模式之前，是通过修改现有模式入门的。几乎每个模式的 Lisp 源代码都是自由可用的；你需要做的是找到一个接近你需求的模式。

如果你想在修改模式方面走得更远，一项必不可少的 Lisp 技能是熟练运用正则表达式。它们在几乎所有模式中以某种方式被使用，特别是在字体锁定例程中。

你需要能够告诉字体锁定引擎如何识别特定的文本块，而正则表达式是做到这一点的唯一实用手段。看看这个从 rmail.el 中摘录的字体锁定代码：

```lisp
(defvar rmail-font-lock-keywords
  (eval-when-compile
    (let* ((cite-char "[>]")
           (cite-prefix "^A-Za-z")
           (cite-suffix (concat cite-prefix "0-9_~^\"")))
     (list '("^\\[From\\|Sender\\]:" . font-lock-function-name-face)
           '("^Reply-To:.\\$" . font-lock-function-name-face)
           '("^\\[Subject]" . font-lock-comment-face)
           '("^\\[To\\[Apparently-To\\[Cc\\[Newsgroups\\]:"
             . font-lock-keyword-face)
           [remainder of defvar statement cut])))
```

这就是 rmail Emacs 邮件客户端确定要突出显示哪些行的方式。注意整个过程中使用的众多正则表达式符号，例如

