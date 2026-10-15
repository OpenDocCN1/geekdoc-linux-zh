

其值为 70

设置后会自动变为缓冲区本地变量。
如果满足以下谓词，则该变量可作为文件本地变量安全使用

其值

为 'integerp'。
文档：

自动换行应发生的列。

交互式地，你可以用 <Ctrl+X> f 设置本地值

你可以自定义此变量。

点击下划线文字 customize，你可以使用一个缓冲区来更改此变量的值。

设置特定可定制变量最方便的按键方法是输入 <Alt+X> set-variable。这会使用 minibuffer（带补全）读取变量名，然后再次在 minibuffer 中读取你输入的新值的 elisp 表达式（你可以通过 <Alt+N> 将旧值插入 minibuffer 进行编辑）。例如：

```
<Alt+X> set-variable <ENTER> fill-column <ENTER> 75 <ENTER>
```

将 fill-column 设置为 75。

<Alt+X> set-variable 仅限于用户选项、可定制变量，但你可以用类似的 elisp 表达式设置任何变量：

```
(setq fill-column 75)
```

要执行此类表达式，输入 <Alt+;:>（eval-expression）并在 minibuffer 中输入表达式。或者，转到 *scratch* 缓冲区，输入表达式，然后输入 <Ctrl+J>。

以这种方式设置变量仅影响当前 emacs 会话。唯一能改变未来会话中变量的方法是在你的初始化文件中将更改作为 Lisp 语句写入。

## 3.3.13.3 Init File Syntax

你的 GNU emacs 系统的初始化文件 ~/.emacs 包含 elisp 表达式。每个 elisp 表达式由一个函数名后跟参数组成，所有内容都用括号括起来。例如：

```
(setq fill-column 60)
```

调用函数 setq 将变量 fill-column 设置为 60。
你可以用 setq 设置任何 Lisp 变量，但对于某些变量 setq 不会起作用。
setq 的第二个参数是变量新值的表达式。这可以是常量、变量或函数调用表达式。在你的 ~/.emacs 文件中，大多数情况下使用常量。它们可以是：

- Numbers: 数字以十进制书写，可选择以减号开头。
- Strings: Lisp 字符串语法与 C 字符串语法相同，并具有一些额外功能。使用双引号字符（"）开始和结束字符串常量。
- Characters: Lisp 字符常量语法由 ? 后跟一个字符或以 \ 开头的转义序列组成。
- True: t 代表“真”。
- False: nil 代表“假”。
- Other Lisp objects: 写一个单引号（'）后跟你想要的 Lisp 对象。

## 3.3.13.4 Keystroke Abbreviations or Abbrevs

就像普通语言中的缩写一样，abbrev 是一个在你插入时展开为通常更长或更长的文本字符串的词。Abbrev 由用户定义以特定方式展开。例如，你可能将 Bob 定义为展开为 Better off built 的 abbrev。然后你可以通过输入 Bob <Space> 将 Better off built 插入到缓冲区中。

第二种缩写功能，我们在此不举例，称为动态 abbrev 展开。你使用显式命令使用动态 abbrev 展开，通过查找缓冲区中以这些字母开头的其他词来展开光标前面的字母。

Abbrev 仅在 Abbrev mode、一种缓冲区本地次要模式启用时展开。禁用 Abbrev mode 不会导致 abbrev 定义被遗忘，但在再次启用 Abbrev mode 之前它们不会展开。命令 <Alt+X> abbrev-mode 切换 Abbrev mode；使用数字参数时，如果参数为正则打开 Abbrev mode，否则关闭。

你可以在编辑会话期间交互式地定义 abbrevs，而不管 Abbrev mode 是否启用。你也可以将 abbrev 定义列表保存在文件中，然后在以后的会话中重新加载使用。

### 3.3.13.4.1 Defining Abbrevs

以下是定义和管理 abbrevs 的方法：<Ctrl+X> a g

定义一个 abbrev，使用光标前的一个或多个词作为其展开（add-global-abbrev）。

