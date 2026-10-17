
人们在 `.emacs` 中做的另一件事是将某些变量设置为首选值。例如，将此放入你的 `.emacs` 然后启动一个新的 Emacs：

```
(setq inhibit-startup-message t)
```

Emacs 通过检查 `inhibit-startup-message` 变量来决定启动时是否显示关于版本和缺少担保的信息。Emacs 使用 `setq` 将该值设置为 `'t`，这是一个表示真的特殊列表值。`'t` 的反面是 `'nil`，它是 Emacs 的默认值。在你的 `.emacs` 中可能会发现：

```
(setq case-field nil)
```

第一个表达式（使用 `is`）是不区分大小写的；也就是说，即使字符串只包含小写，搜索也会匹配参数的大写或小写版本。第二个表达式将 C 语句的默认缩进设置为比现在小一点——这仅仅是个人偏好；我发现这让 C 代码更易读。Lisp 中的注释是 `;`；Emacs 会忽略其后的任何内容，除非它出现在字面量内部。如果注释单独成一行，会在它前面加两个分号。

```
;; 这些行会被 Lisp 解释器忽略，但紧随其后的
;; s 表达式将被完全求：
(setq some-literal-string 'Awake pause; for no purpose.\')
```

要交互式加载文件，请使用命令 `M-x load-file`。它会提示你输入文件名。要从其他 Lisp 文件加载 Lisp 文件，这样做：

## 第 8 章 使用 Emacs 编辑文件

```
(load 'c-mode')
```

强制 Emacs 加载 `c-mode` 或 `.el` 中的内容

Emacs 首先为文件名添加 `.el` 扩展名，并尝试在 `load-path` 中查找它。如果失败，它会尝试使用 `.extension`，如果仍然失败，它将使用传递给 `load` 的原始字符串。你可以使用 `M-x-compile-file` 命令编译文件，但如果你经常修改该文件，这可能不值。在运行 emacs 之后，你应该重新编译你的文件，即使你给它提供了 `.el` 扩展名。

在 Emacs 加载后，它会搜索名为 `default.el` 的文件进行加载。通常它位于 `load-path` 中名为 `site-lisp` 或 `local-isp` 或类似的目录。人们在多用户系统上工作时使用 `default.el` 来做出影响所有人 Emacs 的更改，因为每个 Emacs 都会加载个人的 `.emacs`。`default.el` 也不应该被字节编译，因为之后它往往会被修改。

如果 Emacs 在期间遇到任何错误，它将不会尝试加载 `default.el`，而是直接停止并抛出一条显示“Error in file.”的消息。如果你看到这条消息，可能是你的 Emacs 出了问题。

还有一种经常出现在 `.emacs` 中的问题。Emacs 列表提供了以不同方式实现相同功能的包。这意味着你必须指定你想使用哪一个。发生这种情况的一个领域是 Emacs 的 Scheme 特性。Emacs 中存在两个不同的 Scheme 接口（至少在版本 19 中）：`xscheme` 和 `cmscheme`。

```
prompt* = /usr/lib/emacs/19.19/lib/*scheme*
/usr/lib/emacs/19.19/cmscheme.el
/usr/lib/emacs/19.19/scheme.el
/usr/lib/emacs/19.19/scheme.el
/usr/lib/emacs/19.19/xscheme.el
/usr/lib/emacs/19.19/xscheme.el
```

我恰好更喜欢 `cmscheme` 提供的界面而不是 `xscheme` 提供的界面，但 Emacs 默认使用的是 `xscheme`。我该如何让 Emacs 按照我的偏好运行？我把它放在了 `.emacs` 中：

> ; 注意这个表达式可以跨越两行。Lisp

;; 通常会忽略空白符

```
(autoload 'run-scheme "cmscheme"
"运行一个我喜欢的低级 Scheme。" t)
```

`autoload` 函数接受一个用单引号 `'` 引用的函数名，并告诉 Emacs 该函数定义在某个文件中。该文件是第二个参数，一个以 ".el" 或 ".scm" 结尾的字符串，表示在 `load-path` 中要查找的文件名。

其余参数是可选的，但在这种情况下是必要的：第三个参数是函数的文档字符串，这样你就可以对它使用 `describe-function`。第四个参数告诉 Emacs 该函数可以交互式地加载，即通过使用 `M-x`。这在 Scheme 中非常重要，因为你可以输入 `run-scheme` 来启动一个在 Emacs 下运行的进程。

现在 `run-scheme` 已定义为可自动加载的函数，当我输入 `M-x run-scheme` 时会发生什么？Emacs 寻找 `run-scheme` 以及由 `autoload` 指定的文件。在这种情况下为 "cmscheme"。字节编译的文件 `cmscheme.el` 存在，因此 Emacs 将加载它。该文件必须定义函数 `run-scheme`，否则将报错。

`autoload` 就像是对 Emacs 的一个承诺，当时间到达时，可以在你让它查找的文件找到函数。现在你对加载的内容有了控制权。`autoload` 通过在需要之前不加载条目，有助于减少 Emacs 的内存占用。

10 顺便说一下，`cmscheme` 就是你之前谈论的与 Scheme 工作的那个，如果你想使用该教程中的任何内容，请确保你运行了 `cmscheme`。

## 8.14. 发现

当 Emacs 启动时。它们只是被设置为自动加载某个特定文件。如果你从未调用该命令，它就永远不会被加载。这种节省空间的行为对 Emacs 的运行至关重要：如果它加载 Lisp 库中的每个可用文件，启动将需要二十分钟，而且一旦完成，可能会占用你机器上大部分的可用内存。别担心，你不需要在 `.emacs` 中设置所有这些 `autoload`；它们在构建 Emacs 时已经被处理好了。

我还没有告诉你关于 Emacs 的所有知识。事实上，我认为我甚至只掌握了关于 Emacs 知识的 1%。虽然你已经有了足够应付的知识，但仍然有许多节省时间的技巧和便利之处是你应该去发现的。最好的方法是等到你自己需要某些东西时，然后寻找执行该功能的函数。

熟悉 Emacs 在线帮助设施的重要性再怎么强调都不为过。例如，你知道的越多，能做的就越多。

## 9.1. 定定义

Unix 哲学的一个独特之处是，系统设计者并没有预测所有的需求；他们尝试让每个用户根据自己的需求定制环境。这主要通过配置文件来实现。

### 9.1.1 Shell 启动

Bash 有几种运行方式。它可以作为登录 shell 运行，这是你首次登录时的运行方式。登录 shell 应该是你使用的第一个 shell。

另一种运行方式是作为交互式 shell。这是任何交互式 shell。获取非交互式 shell 的方法可以是 xterm 内部。任何通过登录以外的方式创建的 shell 都是非登录 shell。

最后是非交互式 shell。这些 shell 用于执行命令文件，类似于 MS-DOS bash 文件——以 `.BAT` 结尾的文件。这些 shell 脚本就像微程序。虽然它们通常比普通的编译程序慢得多，但通常更容易编写。

根据 shell 的类型，启动时将使用不同的文件：

| Shell 类型 | 动作 |
|---|---|
| 交互式登录 | 读取并执行 `.bash_profile`；执行 `.bashrc` |
| 交互式非交互 | 读取并执行 shell 脚本 |

### 9.1.2 启动文件

由于大多数用户希望无论使用何种类型的交互式 shell 都有相同的环境，我们通过在 `.bash_profile` 中放入一个非常简单的命令来开始配置：`source .bashrc`。`source` 命令告诉 shell 将参数解释为 shell 脚本。这对我们意味着，每当运行 `.bash_profile` 时，`.bashrc` 也会运行。

现在，我们将命令添加到 `.bash_profile` 中。如果你想添加一个只在登录时运行的命令，请将其添加到 `.bash_profile`。

### 9.1.3 别名

你想自定义的内容有哪些？这里是我认为 90% 的 Bash 用户都放在 `.bashrc` 中的内容

# 第 9 章. 我必须做到！

该命令定义了一个名为 `11` 的 shell **别名**，当用户调用它时，它会“展开”为普通的 shell 命令 `ls -1`。因此，在使用 Bash 并从 `.bashrc` 中调用该命令后，你只需要输入 `11` 就能实现“ls -1”的效果。

图 9.1 显示了一些别名。你可以将它们放在 `.bashrc` 中。其中，一个特别有意思的别名是第一个。有了它，每当有人输入它时，他们就会被自动标记。这是添加你每次调用程序时都会用的选项的常用方法。

注意图 9.1 中带有 `#` 字符的注释。当 `#` 出现时，该行的其余部分会被忽略。

```bash
alias rf='refrobnicate-verbose -prolix -wordy -o foo.out'
```

```bash
alias ed2="emacs -d floss:0 \gray95\ -bg \gray50*"
```

正如你可能猜到的那样，我有时会在选项中传递双引号，因此我必须用反斜杠对它们进行引用，以防止 bash 认为那是别名的结束。

最后，我将两个常见的拼写错误 `mroe` 和 `moer` 别名指向我想要输入的命令 `more`。别名不会干扰你向程序传递参数。

```bash
/home/larry# mroe hrd.txt
```

尝试一下，找到你经常自己使用的长命令，并为它们创建别名。你会发现，这会让在 shell 提示符下工作变成一种更愉悦的体验。

## 9.4 环境变量

在 `.bashrc` 中做的另一件事是设置环境变量。什么是环境变量？让我们反过来来看：假设你正在阅读 fruggle 的文档，并遇到了这样几句话：

“Fruggle 在用户的家目录中查找它的配置文件 `.fglers`。然而，如果环境变量 `FRUGGLEPATH` 被设置为不同的文件，它将转而去那里查找。”

每个程序都运行在一个环境中，而该环境是由调用该程序的 shell 定义的。程序员们有一段特殊的例程来查询环境，而 fruggle 程序就使用了这段例程。它会检查环境变量 `FRUGGLEPATH` 的值。

以下是你如何在 bash 中更改环境的方法：

```bash
/home/larry# export PGPPATH=/home/larry/secrets/pgp
```

## 9.1 bash 自定义

图 9.1 一些著名的 bash 别名。

```bash
alias ls='ls -F'           # 在列列表末尾添加字符
alias ll='ls -l'               # 特殊 ls
alias la='ls -a'
alias rm='rm *'; rm *'      # 这会删除 Emacs 创建的备份文件
alias rd='rmdir'               # 节省打字！
alias md='mkdir'
alias pu=pushd                 # 此处未涵盖 pushd, popd 和 dirs
alias po=popd                   # 手册--你可能想去查一下它们
alias ds=dirs                  # 在 bash 手页中
# 这些都是键盘快捷键
alias to='telnet cs.oberlin.edu'
alias ta='telnet altair.mcs.ans.gov'
alias tg='telnet womombat.gnu.mit.edu'
alias thakk='talk kold@cs.oberlin.edu'
alias tj='talk jimb@cs.oberlin.edu'
alias mroe='more -f'            # 拼写纠！
alias moer='more'
alias email='emacs -f mail *'  # 我的邮件阅读器
alias ed2='emacs -d floss:0 -fg\gray95\* -bg\gray50*' # 调用 emacs 的一种方式
```

你可能认为 `export` 命令意味着“请将此变量导出到我将调用程序的环境中”。

这个特定的变量由 Phil Zimmermann 臭名昭著的公钥加密程序 `pgp` 使用。默认情况下，它使用你的家目录查找它需要的文件，并作为存储运行时创建的临时文件的地方。通过将 `PGPPATH` 设置为此值，你可以更改它的行为。
