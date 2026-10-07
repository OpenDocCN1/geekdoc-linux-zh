
## BOURNE AGAIN 和 TC SHELL 共有的特征

`bash` 和 `tcsh` 共享许多共同特征，其中大部分源于原始的 C Shell。这些特征包括

- 历史 (`history`)
- 别名 (`aliases`)
- 作业控制 (`job control`)
- 文件名替换 (`filename substitution`)

## Bourne Again 和 TC Shell 共有的特征 413

由于 `bash` 章节详细讨论了这些特征，本节重点关注 `bash` 和 `tcsh` 版本之间的差异。

## 历史 (History)

`tcsh` 中历史的使用与其在 `bash` 中的用法相似。（关于历史功能的完整描述请参阅第 340 页，该功能实际上源于 `csh`）。变量 `event` `!!` 指 `tcsh` 中的上一个事件，就像在 `bash` 中一样。命令 `:3` 指 `tcsh` 中的上上三个事件，就像在 `bash` 中一样。

| 修饰符 (Modifier) | 效果 (Effect) |
| :--- | :--- |
| `u` | 将首字母转换为大写 |
| `l` | 将首字母转换为小写 |
| `a` | 在历史中搜索包含字符串的事件 |

在命令中使用可以使用多个修饰符。例如，`!!u` 获取上一个事件并将其首字母转换为大写。

## Bourne Again Shell 和 TC Shell 共同特性 415

## 选项（继续）

如果你想在 `w` 命令后追加命令数字 250，可以使用大括号将事件数字与 `w` 隔离开。

`! {250}w`

## tcsh 和 bash 别名机制的区别

`bash` 中的 `alias` 内置命令和替换是参考 Korn Shell 中的 `alias` 内置命令设计的。它与 `tcsh` 中的 `alias` 内置命令略有不同，后者是参考 C Shell 中的 `alias` 设计的。`tcsh` 使用的版本语法格式为：

`alias name value`

`tcsh` 版本的 `alias`（见下一节）允许你替换命令参数。如果你想在 `bash` 中实现类似的功能，必须使用 shell 函数（第 403 页）。

## Alias（别名）

`tcsh` 中的 `alias/unalias` 特性与 `bash` 中的对应功能非常相似（第 348 页）。然而，`alias` 内置命令本身的格式略有不同。在 `bash` 中，你可以使用以下命令为 `ls` 创建别名：

```bash
bash alias ls="ls -1F"
```

在 `tcsh` 中，你可以创建相同的别名：

`alias ls='ls -1F'`

在 `tcsh` 中，你可以使用历史记录机制替换命令行参数，单个感叹号表示包含别名的输入行。修饰符与 `history` 使用的相同（第 413 页）。在以下示例中，感叹号被引号引用，以免 shell 在构建别名时对其解释（这将导致错误的结果）：

```
21> alias last echo \!:s
22> last this is just a test
test
23> fn2 echo \!:t
24> fn2 /home/jenny/test /home/alex/temp /home/barbara/temp
```

事件 21 为 `last` 定义了一个别名，用于显示该别名。事件 23 为 `fn2` 定义了一个别名，用于显示命令行中第二个参数的文件名（或尾）。

某些别名名称（特殊别名，见第 416 页表格）对 `tcsh` 有特殊含义。如果你使用这些名称之一定义别名，它会在与 shell 交互的某些点自动执行。初始状态，所有特殊别名都是未定义的。

## 416 第 12 章：TC Shell

| 特殊别名 | 执行时机 |
| --- | --- |
| `beepcmd` | 每当 shell 通常会触发终端铃声时。这让你能够在这些时间产生其他视觉或音频效果。 |
| `cwdcmd` | 每当你切换到另一个工作目录时。 |
| `periodic` | 定期执行，由变量 `tperiod` 中的分钟数决定。如果 `tperiod` 未设置或值为 0，则无法设置 `periodic`。 |
| `precmd` | 在 shell 显示提示符之前。 |
| `shell` | 为不以 `#!` 开头的脚本提供想要使用的解释器名称（第 317 页）。别名的第一个单词必须是所用解释器的完整路径。 |

要查看当前别名列表，请输入命令 `alias`。要查看特定名称的别名，请输入命令 `alias [名称]`。

## 作业控制（Job Control）

`bash`（第 310 页）和 `tcsh` 中的作业控制之间没有太大区别。你可以在前台后台之间移动命令，临时挂起作业，并获取当前作业列表。当 `%` 字符跟随作业数字或唯一标识作业的字符串前缀时，它引用该作业。在后台运行多进程命令行时，你会发现细微差别：`bash` 只显示每个作业中最后一个后台进程的 PID，而 `tcsh` 显示属于该作业的所有进程的数字。第 310 页的示例在 `tcsh` 下如下所示：

```
> find -print | sort | lpr & grep -1 alex /tmp/* > exfiles &
[1] 18839 18840 18841
[2] 18876
```

## 文件名替换

TC Shell 展开路径中的 `bash` 中的字符 `*`、`?` 和 `[]`（第 106 页）。`*` 匹配零或多个字符的任何字符串。`?` 匹配任何单个字符，`[]` 定义字符类，用于匹配方括号内的单个字符。

TC Shell 处理以波浪号 (`~`) 开头的参数的方式与 `bash` 相同（第 419 页），`~` 代表用户家目录或波浪号后跟随用户的家目录（`tcsh` 不支持特殊扩展 `+` 和 `~`）。

`tcsh` 支持大括号扩展，与波浪号扩展一样，被视为文件名替换的一种。即使大括号扩展可以生成不是实际文件名的字符串，也是如此。在 `tcsh` 及其前身 `csh` 中，使用模式匹配文件名的过程被称为 `globbing`（通配符），模式本身被称为 `globbing pattern`。如果 `tcsh` 无法生成匹配 `glob` 模式的一个或多个文件列表，它会报告错误（除非模式中包含大括号）。

## 重定向标准错误 417

设置 shell 变量 `globlob` 会抑制文件名提交，包括波浪号和大括号解释。

## 目录栈操作

`bash`（第 313 页）和 `tcsh` 中的目录栈操作之间没有太大区别。`dirs` 内置命令显示栈的内容，而 `pushd` 和 `popd` 内置命令将目录推入或从栈中弹出。

## 重定向标准错误

在 `tcsh` 中，你可以使用大于符号 (`>`) 后接一个量符号 (`&`) 来重定向标准错误。与 `bash` 不同（`bash` 可以用一个命令重定向输出和错误），`tcsh` 要求你分别重定向。例如，如果你想将输出重定向到一个文件，将错误重定向到另一个文件，可以使用：

```
> command > file1 2> file2
```

如果你想将输出和错误都重定向到同一个文件，可以使用：

```
> command > file1 2>&file1
```

`>>` 符号用于将输出追加到文件而不是覆盖。

```
> command >> file1 2>> file2
```

`|&` 符号可以将输出和错误都管道到另一个命令。

```
> command |& next_command
```

`tee` 命令可以将输出同时重定向到文件和标准输出。

```
> command | tee file1
```

`tee -a` 命令可以将输出追加到文件和标准输出。

```
> command | tee -a file1
```

## 波浪号补全 (Tilde Completion)

TC Shell 会解析出现在单词开头的波浪号 (`~`)，并在你使用 TAB 键时，尝试将其展开为用户名。

```
> cd -al -> TAB -> cd ~alex/
> pw
/home/alex
```

通过添加斜杠 (`/`)，`tcsh` 会让你知道补全的单词是一个目录。斜杠也便于继续指定路径。

## 命令和变量补全 (Command and Variable Completion)

你可以使用相同的机制来补全和列出命令名、变量名的文件名。除非给出完整名称，否则 shell 会尝试使用变量 `path` 来补全命令名；列出的选项将位于不同的目录中。

```
> up -> TAB -> upREPLY ->CONTROL-D
updated ups uptime
> upt -> TAB -> uptime
9:59am up 31 days, 15:11, 7 users, load average: 0.03, 0.02, 0.00
> which updated ups uptime
>usr/bin/updateddb
>usr/local/bin/ups
>usr/bin/uptime
```

如果你像下面的示例那样设置了 `autolist` 变量，当你按下 TAB 触发补全时，shell 会自动列出选项；你无需按下 CONTROL-D：

```
> set autolist
> up TAB -> upREPLY
updated ups uptime
> upt -> TAB -> uptime
10:01am up 31 days, 15:14, 7 users, load average: 0.20, 0.06, 0.20
```

如果你设置了 `autolist ambiguous`，shell 会列出输入行内单词的选项，以确定它是文件名、用户名、命令还是变量名。否则，按下 TAB 会导致 shell 向单词添加一个或多个字符，直到它是最长前缀；再次按下 TAB 将列出选项。

```
> set autolist=ambiguous
> echo sh -> TAB ->upREPLY
histfile history home
> echo shi -> TAB -> echo $shiTAB
histfile history
> echo Shisto -> TAB -> echo History
100
```

shell 必须根据单词在输入行中的上下文来确定它是文件名、用户名、命令还是变量名。如果单词是输入行的第一个，则被假设为命令名；如果它以特殊字符 S 输入，则被视为变量名，以此此类推。在接的示例中，**第二个**命令没有正常工作，因为单词 `up` 的上下文使其在 `tsh` 看起来像是一个文件前缀，而不是命令前缀。TC Shell 将 `which` 作为 `updates`（一个不可执行文件）的参数；`which` 会显示错误信息。

```
> ls*
updates
> whichdatedb ups uptime
>/usr/bin/updateddb
>/usr/local/bin/ups
>/usr/bin/uptime
> which up TAB → which updates
updates: Command not found.
```

## 命令编辑 (COMMAND-LINE EDITING)

`tsh` 的命令行编辑功能与 `bash`（以及你将在下一章看到的 `zsh`）类似。你可以使用类似 GNU `emacs` 风格的命令或类似 `vi` 风格的命令。默认是 `emacs` 命令，但你可以通过 `bindkey` 绑定进行更改。如果你在使用 `emacs` 风格的绑定，可以使用 `bindkey -e` 更改 `vi` 命令。箭头键已绑定到显而易见的移动命令，因此你可以在历史列表中来回移动（上下），也可以在当前命令中左右移动。

`bindkey` 内置命令在不带参数时，显示编辑器命令与你可以在键盘上输入的键序列之间的当前映射。

```
> bindkey | less
```

这里使用 `less` 工具是因为它允许你在阅读这个很长的列表时，在其中来回移动和搜索。如果你熟悉 `emacs` 或 `vi`，你将认识 `bind-key` 列出的某些命令。

## 拼写检查 (SPELLING CORRECTION)

如果你愿意，可以让 `tsh` 尝试对命令名以及命令参数不进行拼写纠正（但仅在你使用 `emacs` 风格的绑定时）。关于拼写检查你有几种选择。使用 `spell-word` 和 `spell-line`。要纠正光标左侧单词的拼写，请输入 Meta-S（META字符的描述请见第250页“按单词移动光标”）。输入 Meta-S 会调用 `spell` 函数，它尝试纠正命令行上的所有单词。你可以通过设置 shell 变量 `correct` 来启用自动拼写检查。以下命令说明了这些函数的使用：

```
> set correct
> ls
bigfile.gz
> gzip → Meta-s → gzip bigfile.gz → Meta-s → gzip bigfile.gz
> gunzip bigfile.gz → Meta-S → gunzip bigfile.gz
```

## 变量

如果设置为 `cmd`，则只对命令名进行拼写检查。将 `correct` 设置为 `all` 会对整个命令行进行拼写检查。自动拼写检查会显示一个提示，允许你输入 `y` 拒绝，`n` 编辑，或 `a` 终止命令。关于在拼写检查中使用的特殊提示，请参阅第430页的 ``prompt3``。

## 字符串变量

TC Shell 处理字符串的方式与 Bourne Shell 类似。主要区别在于声明和赋值：`tcsh` 使用显式命令 `set`（或 `setenv`）来声明和/或赋值。

## 字符串变量数组 (Arrays of String Variables)

在访问数组的单个元素之前，必须声明整个数组。声明数组时你需要为数组的每个元素分配一个值。值列表必须包含在括号中。

## 变量 423

```bash
8 > set colors = (red green orange yellow)
9 > echo $colors
red green orange yellow
10 > echo $colors[3]
blue
11 > echo $colors[2-4]
green blue orange
```

```bash
12 > set shapes = (' ' '' ' ' '' '')
13 > echo $shapes
14 > set shapes[4] = square
15 > echo $shapes[4]
square
```

事件 8 声明了一个名为 `colors` 的字符串变量数组，包含五个元素，并为这些元素每个分配了值。如果你在声明数组时不知道元素的值，可以声明一个包含必要数量空元素的数组（元素 12）。

你可以使用美元符号 (`$9`) 通过其前置的索引来引用数组元素。方括号中的数字提供了对数组元素的引用（元素 10、14 和 15）。

方括号中两个用逗号隔开的数字引用数组中两个或多个相邻的元素（事件 11）。关于数组的信息，请参阅第 426 页的“特殊变量形式”。

## 数值型变量

内置命令 `@` 用于给数值变量赋值。你可以像使用 `set` 声明非数值变量一样声明数值变量。然而，如果你给 `@` 传递非数值参数，它会显示错误信息。不带任何参数的 `@` 命令会给你所有 shell 变量列表，就像不带参数的 `set` 命令一样。

内置命令 `@` 可以评估的许多表达式以及识别的运算符来源于 C 编程语言。以下是使用 `@` 进行声明或赋值的格式，在 `@` 之后需要加一个空格。

```bash
@variable-name expression
```

变量是你正在声明或赋值的变量名。运算符是 C 赋值运算符之一：`+=`、`-=`、`*=`、`/=`、`%`。（这些运算符的解释见第 652 页）。表达式是一个可以包含大多数运算符，请参考随后的“表达式”小节。你可以在表达式中使用括号来提高清晰度或改变求值顺序。括号必须包含以下任何字符：`<` `>` 或 `|` 的表达式部分。

## 表达式

表达式可以由常量、变量和下表中的运算符（按优先级递减排序）组成。还有一组涉及文件而非数值变量或字符串的表达式。这些表达式描述在第 435 页。

| 运算符 | 功能 |
| :--- | :--- |
| 括号 | |
| `()` | 改变求值顺序 |
| 一元运算符 | |
| `-` | 一元负 |
| `~` | 补反 |
| `!` | 逻辑取反 |
| `++` | 后置自增 |
| `--` | 后置自减 |
| 算术运算符 | |
| `%` | 取余 |
| `/` | 除法 |
| `@` | 乘法（* |
| `-` | 减法 |
| `+` | 加法 |
| 移位运算符 | |
| `>>` | 右移 |
| `<<` | 左移 |
| 关系运算符 | |
| `>` | 大于 |
| `<` | 小于 |
| `>=` | 大于等于 |
| `<=` | 小于等于 |
| `!=` | 不等于（比较字符串） |
| `==` | 等于（比较字符串） |
| 位运算符 | |
| `&` | 与 (AND) |
| `^` | 异或 (XOR) |
| `|` | 或 (OR) |
| 逻辑运算符 | |
| `&&` | 与 (AND) |
| `||` | 或 (OR) |

## 变量 425

表达式遵循以下规则：

- shell 将缺失或为空的参数评估为 0。
- 所有结果均为十进制数字。
- 除了 `!=` 和 `==` 外，运算符均作用于数值参数。
- 你必须用空格将表达式的每个元素与相邻元素分开，除非相邻元素是 `&`、`|`、`<>`、 `(` 或 `)`。

以下是一些使用 `@` 的示例：

```bash
216 > count = 0
```
