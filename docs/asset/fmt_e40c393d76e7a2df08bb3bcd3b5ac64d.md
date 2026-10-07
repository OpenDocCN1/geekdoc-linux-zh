
```bash
bash$ ls -l
total 3
-rw-rw-r-- 1 alex group 14 Jan 22 08:54 file1
-rw-rw-r-- 1 alex group 14 Jan 22 08:54 file2
-rw-rw-r-- 1 alex group 14 Jan 22 08:55 file3
bash$ mkdir version[A,B,C,E]
bash$ ls -l
total 8
-rw-rw-r-- 1 alex group 14 Jan 22 08:54 file1
-rw-rw-r-- 1 alex group 14 Jan 22 08:54 file2
-rw-rw-r-- 1 alex group 14 Jan 22 08:55 file3
drwxr-xr-x 2 alex group 1024 Jan 25 15:27 versionA
drwxr-xr-x 2 alex group 1024 Jan 25 15:27 versionB
drwxr-xr-x 2 alex group 1024 Jan 25 15:27 versionC
drwxr-xr-x 2 alex group 1024 Jan 25 15:27 versionD
drwxr-xr-x 2 alex group 1024 Jan 25 15:27 versionE
```

如果使用了歧义通配符（ambiguous glob），我们必须指定目录而不是使用上面的表示法，这将得到一个完全不同（不符合预期）的结果：

```bash
bash$ ls -l
total 4
-rw-rw-r-- 1 alex group 14 Jan 22 08:54 file1
-rw-rw-r-- 1 alex group 14 Jan 22 08:54 file2
-rw-rw-r-- 1 alex group 14 Jan 22 08:55 file3
bash$ mkdir version[A-E]
bash$ ls -l
total 4
-rw-rw-r-- 1 alex group 14 Jan 22 08:54 file1
-rw-rw-r-- 1 alex group 14 Jan 22 08:54 file2
-rw-rw-r-- 1 alex group 14 Jan 22 08:55 file3
drwxr-xr-x 2 alex group 1024 Jan 25 13:38 version[A-E]
```

# 波浪号扩展 (Tilde Expansion)

第 4 章展示了指定你的主目录或其他用户主目录的简写法，这被称为波浪号扩展。本节提供了对该表示法的更详细解释。

当 shell 扫描上一个示例中的令牌时，它发现其中一个以波浪号（~）开头，当它出现在令牌开头时是一个特殊字符。当 shell 找到波浪号时，它会查看后续字符，直到第一个斜杠（/），或者如果没有斜杠则到单词结束，将其作为可能的名称。如果此登录名为空（如果波浪号单独出现，或者后面紧跟一个斜杠），shell 将用 `HOME` 的值替换波浪号。或者说 shell 将波浪号扩展为 `HOME` 的值。下面的示例演示了这种替换或扩展。最后一个命令将 Alex 的主目录中名为该的文件复制到当前工作目录。

# 命令行扩展 353

```bash
bash$ echo $HOME
/home/alex
bash$ echo ~
/home/alex
bash$ echo ~letter
/home/alex/letter
bash$ cp ~letter .
```

如果可能的登录名是有效的登录名，shell 将与该登录名关联的主目录替换波浪号和名称。如果它既不为空又不是有效的登录名，shell 则不会进行任何替换。

```bash
bash$ echo ~jenny
/home/jenny
bash$ echo ~root
/root
bash$ echo ~xx
~xx
```

这种波浪号扩展是对 C Shell 中存在的波浪号扩展的适配。**bash** shell 包含了 C Shell 或 tsh 中未找到两种特殊波浪号扩展；然而，你可以使用 `~` 作为工作目录的简写，而 `+` 是当前工作目录的简写。与其他类型的命令行扩展一样，对波浪号表示法的解释是由 shell 在执行命令之前完成的。

# 参数扩展 (Parameter Expansion)

当美元符号（$）后紧跟单个数字或用大括号括的整数时，shell 将与该整数对应的位置参数的值替换该令牌。这被称为*参数扩展*。另一种类型的参数扩展发生在美元符号后跟随特殊字符时，在这种情况下，命令或其参数的某些方面将被替换为令牌。

# 变量扩展 (Variable Expansion)

另一种扩展类型——变量扩展，发生在 shell 处理一个由美元符号（$）后跟一个名称组成的令牌时，例如 `$VARIABLE`。shell 将令牌替换为变量的值，无论该变量是用户定义的还是关键字。

前述语法是更通用的语法 `${VARIABLE}` 的特例，其中变量名被括在大括号中。大括号用于将变量名与周围文本隔离开。

```bash
bash$ echo ${VARIABLE}
```

下面的示例展示了如何使用大括号扩展变量：

```bash
bash$ NAME=world
bash$ echo Hello ${NAME}
```

当变量名后紧跟可能被认为是名称本身部分的字符时，大括号也是必要的。

```bash
bash$ VAR=123
bash$ echo ${VAR}abc
```

# 356 第 10 章：Bourne Again Shell (bash)

当你在使用 `let` 或 `$(expression)` 进行算术扩展并引用变量时，bash并不要求你将变量名以美元符号（$）开头，尽管这样做是一个好习惯（因为在大多数地方你必须这样做）。以下两个表达式为 `numpages` 分配了相同的值：

```bash
bash let numpages=numpages+1
bash let numpages=$numpages
```

## 单词拆分 (Word Splitting)

`IFS`（内部字段分隔符）壳变量指定了你可以用于分隔命令行参数的字符。它的默认值为空格（SPACE）、制表符（TAB）和换行符（NEWLINE），你可以始终使用一个或多个空格或制表符来分隔命令行参数，只要这些字符没有被引用或转义。当你使用 `IFS` 作为新字符，这些字符也可以分隔字段，但仅当它们经历了某种类型的扩展时。这种对命令行的解释被称为“单词拆分”。接下来的示例演示了 `IFS` 如何影响对命令行的解释：

```bash
bash$ IFS=:
w:x:y:z
bash$ cat sa
cat: w:x:y:z: No such file or directory
bash$ IFS=$'
bash$ cat sa
cat: w: No such file or directory
cat: x: No such file or directory
cat: y: No such file or directory
cat: z: No such file or directory
```

第一次调用 `cat` 时，shell扩展变量 `a`，将字符串 `a:b:c:d` 解释为单个标记，作为 `cat` 的参数。`cat` 工具找不到名为 `a:b:c:d` 的文件，并对该文件名报告错误。当 `IFS` 设置为冒号（:`）后，shell 将变量扩展为四个单词作为 `cat` 的参数。这导致 `cat` 工具对四个文件报告错误：a、b、c 和 d。基于字符 `:` 的单词拆分仅在变量 `a` 扩展之后发生。

> 注意
> - 1. 虽然连续的空格或制表符序列被视为单个分隔符，但其他字符的每次出现都会作为分隔符。
> - 2. 更改 `IFS` 有多种副作用，因此请谨慎更改。你可能会发现先在更改 `IFS` 前保存 `IFS` 的值很有用；这样如果你得到意外的结果，就可以轻松地恢复它。

bash 中 `IFS` 的用法已与原始的 Bourne Shell有所不同。在 Bourne Shell 中，命令行上的所有单词都是根据 `IFS` 中找到的分隔符进行拆分的。

# 命令行扩展 357

bash 单词拆分仅在命令行中的标记被扩展后才会发生。这种差异细微但至关重要。考虑以下命令：

```bash
bash$ IFS="p"
bash export IFS
```

在原始的 Bourne shell 中，标记 `export` 中的字符 `p` 是一个分隔符，因此命令行的效果将是以两个文件名 `ort` 和 `IFS` 开头启动 `ex` 命令。在某些 UNIX 版本上，可以利用这一特性在不知道超级用户密码的情况下获得超级用户权限。出于此原因，bash 改变了 `IFS` 的行为。

你无法取消（unset）`IFS` 变量。

## 路径扩展 (Pathname Expansion)

解释歧义引用并替换适当文件名列表的过程称为路径扩展（第 106 页）。当 shell 遇到歧义的文件引用——包含任何字符 `*`、`?`、`[` 或 `]` 的标记时——它会执行此功能。如果 shell 无法找到匹配指定模式的文件，该标记将保持原样；shell 不删除该标记也不会将其替换为空字符串。在以下示例的第一个命令中，shell 扩展了歧义的文件引用 `tmp*`，并将三个标记（`tmp1 tmp2 tmp3`）传递给 `echo`，它显示了 shell 传递的三个文件名。在 `rm` 这三个 `tmp*` 文件后，shell 在尝试扩展时没有找到匹配 `tmp*` 的文件名，因此它将未扩展的字符串传递给命令，该命令显示了它所收的字符串。

```bash
bash$ ls
tmp tmp2 tmp3
bash$ echo tmp*
tmp tmp2 tmp3
bash$ rm tmp*
bash$ echo tmp*
tmp*
```

在参数周围加上引号会导致 shell 抑制路径扩展以及除参数和变量扩展以外的所有其他扩展。在 `echo` 的参数周围加上单引号会抑制所有类型的扩展。在接下来的示例中，当用双引号引用时，shell 将 `$0` 扩展为运行命令的程序名称（`-bash`）；当使用单引号时，不会发生扩展。因为单引号和双引号都不允许路径扩展，最后两个命令显示了未扩展的参数 `tmp*`。

```bash
bash$ ls
tmp tmp2 tmp3
bash$ echo "tmp* $0"
tmp tmp2 tmp3 -bash
bash$ echo "tmp* $0"
tmp**
bash$ echo 'tmp* $0'
tmp* $0
```

# 358 第 10 章：Bourne Again Shell (bash)

shell 能够区分变量的值和变量的引用，如果歧义的文件引用出现在变量的值中，则不会被扩展。这使得你可以为变量赋值包含星号（`*`）等特殊字符的值。

在下一个示例中，工作目录有三个以 `tmp` 开头的文件。尽管如此，当你将值 `tmp*` 赋值给变量 `var` 时，shell 不扩展该歧义的文件引用，因为它出现在变量的值中。字符串 `tmp*` 周围没有引号。仅凭上下文就防止了扩展。赋值后，`set` 内置命令（在 `grep` 的帮助下）显示 `var` 的值为 `tmp*`。

三个 `echo` 演示了三个层级的扩展。当 `$var` 用单引号引用时，shell 不执行任何扩展并传递 `echo $var`；使用双引号时，shell 执行变量扩展并向 `echo` 传递扩展后的值。如下所示：

```bash
bash$ ls
tmp tmp2 tmp3
bash$ echo '$var'
$var
var=tmp*
bash$ echo "$var"
tmp*
bash$ echo $var
tmp*
```

## 扩展顺序

shell 扫描标记按以下顺序执行不同类型的扩展：

1. 花括号扩展（第 351 页）
2. 波浪号扩展（第 352 页）
3. 参数扩展（第 353 页）
4. 变量扩展（第 353 页）
5. 命令替换扩展（第 354 页）
6. 算术扩展（第 354 页）
7. 单词拆分（第 356 页）
8. 路径扩展（第 357 页）

这些扩展发生的顺序非常重要；如果 shell 以不同的顺序执行扩展，结果可能会截然不同。在下面的示例中，如果路径扩展发生在单词拆分之前，结果将如下：

```bash
bash$ IFS=":"
bash$ var="a:b:c"
bash$ echo $var
a b c
```

# 命令行编辑 359

## 命令行编辑 (COMMAND-LINE EDITING)

bash 提供了一个功能，可以在执行前纠正输入的错误——这是一个非常需要的功能。这种交互式功能类似于 Korn Shell 中的命令行编辑功能，并类似于 tsh 和 zsh。它自己也有一些实用的扩展。

## Readline Library

[PAGE 408]在变量扩展之前，给 `echo` 的参数将是 `tmp`，这将 `echo` 的输出。

```bash
bash$ ls
tmp tmp2 tmp3
bash$ var=tmp*
bash$ echo $var
```

记住，双单引号会导致 shell 执行扩展时有所不同（第 320 页）。双引号允许参数和变量扩展，但抑制其他类型的扩展。单引号抑制所有类型的扩展。

Readline Library

在 bash 中使用命令行编辑时，你可以选择两种基本模式：emacs 或 vi。这两种模式都提供了许多但并非所有的编辑器可用命令。默认模式是 emacs，但你可以通过以下命令交互地切换到 vi 模式：

```bash
bash set -o vi
```

要切换回 emacs 模式，给出命令：

```bash
bash set -o emacs
```

对 emacs 的熟悉使得使用 emacs 类的快捷键变得容易，文档中使用的符号也是类似的。还有熟悉的剪贴板（kill ring）和粘贴（yank）概念，这些在 emacs 中都存在。你键盘上的键已绑定到用于编辑所需的命令。你可以在家目录下的 `.inputfile` 中更改这些绑定。任何使用 Readline Library 的应用程序首先读取 `.inputfile`（如果存在）、初始命令绑定以及特殊配置设置。参阅第 361 页更多关于使用 `.inputrc` 的信息。

使用 `bind -v` 查看哪些键绑定有效。该命令显示所有可用命令的列表，如果某个命令绑定到了按键序列，它也会显示该序列。本讨论使用的是 emacs 模式。

# 360 第 10 章：Bourne Again Shell

## Readline 命令

有若干类命令符合通用文本编辑所需的命令：

- 在命令行中来回移动
- 在历史列表中向上和向下移动
- 修改、删除和替换文本
- 撤销和重做更改

这些操作最常用的 emacs 均可用，你应该尝试你已经用过的命令，看看它们是如何运行的。你也可以使用方向键来移动。向上和向下移动会让你在历史列表中向后移动。关于 vi 和 emacs 的命令摘要，请参考第 238 页和 290 页。

## 其他命令

除了上述命令外，还有一些设计用于在使用 shell 时更加实用。

## 补全

你可以使用 TAB 键补全你在命令行上输入的单词。这种功能被称为补全，类似于 tcsh 和 zsh 中的功能。补全的类型取决于你正在输入的内容。

如果你正在输入命令名称（命令行上的第一个单词），按下 TAB 将导致命令补全；bash 会查找名称以你输入的单词部分开头的命令。如果有，bash 就会补全。再次按下 TAB 会导致 bash 显示一个以你输入的前缀开头的命令列表，并允许你完成命令名的输入。

如果你正在输入文件名，则 TAB 将执行文件名补全。如果它能明确确定名称是什么，bash 会替你输入文件名的剩余部分。与命令补全一样，你可以使用 ESC TAB 来列出候选项。

在输入变量名时，按下 TAB 将导致变量补全；bash 会尝试为你补全变量名。

如果你想随时查看可能的补全列表，请按下 ESC ??。

杂项命令。以下是使用 bash 时可用的其他一些 Readline 命令：

- 波浪号扩展命令（Tilde-expand command）尝试将当前单词扩展为以该前缀开头的用户名。例如，如果你的系统中只有一个以 sc 开头的用户名 scott，那么输入 `scTAB` 将结果是 `scott`。
  ESC ~
- 历史扩展行命令（history-expand-line command）对当前行中的所有历史事件执行历史扩展。
  ESC ^
- ESC CONTROL-e 壳扩展行命令（shell-expand-line command）对当前行进行完全扩展，就像 bash 在准备执行命令时一样。所有的别名（alias）和历史扩展都会被执行。

## .inputrc 文件

Bourne Shell 以及其他使用 Readline 库的程序从你的主目录读取 `.inputrc` 以获取初始化信息。如果没有设置 `INPUTRC` 环境变量，则使用该默认文件。如果设置了 `INPUTRC`，则使用其值作为初始化文件的名称。

你可以在 `.inputrc` 中设置一些变量来控制 Readline 库的行为。你使用以下语法通过 set 设置这些变量：

```
set variable_value
```

以下你可以通过这种方式设置的一些变量：

- `editing-mode`：设置为 vi 可让 Readline 以 vi 模式启动。将其设置为 emacs 则让 Readline 以 emacs 模式启动，这是默认设置。
- `expand-tilde`：设置为 on 时，Readline 在每次尝试补全单词时都会执行波浪号扩展。通常情况下它是关闭的（off）。
- `horizontal-scroll-mode`：设置为 on 可让长行超出显示区域的边缘。当你在边缘处向右移动光标时会将行向左移动，以便你看到更多行内容。你可以通过将光标移过左边缘来移回。默认值是 off，这会导致长行换行到显示器的多行中。
- `mark-modified-lines`：设置为 on 时，Readline 在修改过的历史行前加一个星号（）。默认值是 off。
