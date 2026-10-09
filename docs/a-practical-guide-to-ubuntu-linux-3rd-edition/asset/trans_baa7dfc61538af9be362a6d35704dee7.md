

以下第一个示例将提示符更改为主机名称、一个 `SPACE`（空格）以及一个美元符号（或者，如果用户以 **root** 权限运行，则为井号）。第二个示例将提示符更改为时间后跟用户名称。第三个示例将提示符更改为本书中使用的样式（root 使用井号，其他情况使用美元符号）：

```
$ PS1='\h \$ '
bravo $
$ PS1='\@ \u $ '
09:44 PM max $
$ PS1='\$ '
$
```

表 9-4 描述了一些你可以用在 `PS1` 中的符号。要查看提示字符串中可使用的特殊字符完整列表，请打开 `bash` 手册页并搜索第二次出现的 PROMPTING（输入命令 `/PROMPTING` 然后按 n）。

### 表 9-4 PS1 符号
| **符号** | **在提示符中的显示** |
| :--- | :--- |
| `\$` | 如果用户以 **root** 权限运行，显示 #；否则显示 $ |
| `\w` | 工作目录的路径名 |
| `\W` | 工作目录的基名 |
| `\!` | 当前事件（历史）编号（第 335 页） |
| `\d` | 星期几、月份、日期的格式 |
| `\h` | 机器主机名，不包含域名 |
| `\H` | 完整的机器主机名，包含域名 |
| `\u` | 当前用户的用户名 |
| `\@` | 当前时间，12 小时制，AM/PM 格式 |
| `\T` | 当前时间，12 小时制 HH:MM:SS 格式 |
| `\A` | 当前时间，24 小时制 HH:MM 格式 |
| `\l` | 当前时间，24 小时制 HH:MM:SS 格式 |

## PS2：用户提示符（次级）

`PS2` 变量保存次级提示符。在下一个示例的第一行中，`echo` 后面跟着一个未闭合的引号字符串。Shell 假设命令未完成，并在第二行给出默认的次级提示符（`>`）。此提示符表明 Shell 正在等待用户继续命令行。Shell 会等待直到接收到闭合字符串的引号。只有那时它才会执行命令：

```
$ echo "demonstration of prompt string
> 2"
demonstration of prompt string
2
$ PS2="secondary prompt: "$ echo "this demonstrates
secondary prompt: prompt string 2"
this demonstrates
prompt string 2
```

第二个命令将次级提示符更改为 `secondary prompt:` 后跟一个 SPACE（空格）。多行 `echo` 演示了新的提示符。

## PS3：菜单提示符

PS3 变量保存 `select` 控制结构的菜单提示符（第 984 页）。

## PS4：调试提示符

PS4 变量保存 `bash` 调试符号（第 966 页）。

## IFS：分隔输入字段（单词分割）

`IFS`（内部字段分隔符）Shell 变量指定了你可以用来分隔命令行参数的字符。其默认值为 `SPACE TAB NEWLINE`（空格 制表符 换行符）。无论 `IFS` 的值如何，你都可以始终使用一个或多个 SPACE（空格）或 TAB（制表符）字符来分隔命令行上的参数，前提条件是这些字符没有被引用或转义。当你为 `IFS` 赋值时，这些字符也可以分隔字段——但只有经过扩展时才起作用。这种对命令行的解释方式被称为 *word splitting*（单词分割）。

**更改 IFS 时要小心**

> *注意* 更改 `IFS` 会有各种副作用，因此请谨慎操作。你可能会发现，在更改 `IFS` 之前保存其值很有用。这样，如果你得到意外结果，就可以轻松恢复原始值。或者，你可以使用 **bash** 命令分叉一个新的 Shell，然后再试验 `IFS`；如果遇到困难，你可以 **exit** 回到旧的 Shell，在那里 `IFS` 工作正常。

以下示例演示了设置 `IFS` 如何影响命令行的解释：

```
$ a=w:x:y:z

$ cat $a
cat: w:x:y:z: No such file or directory
$ IFS=";"

$ cat $a
cat: w: No such file or directory
cat: x: No such file or directory
cat: y: No such file or directory
cat: z: No such file or directory
```

第一次调用 `cat` 时，Shell 扩展变量 `a`，将字符串 `w:xyz` 解释为单个单词，作为 `cat` 的参数。`cat` 实用程序找不到名为 `w:xyz` 的文件，并针对该文件名报告错误。当 `IFS` 设置为冒号（`:`）后，Shell 将变量 `a` 扩展为四个单词，每个都是 `cat` 的参数。现在 `cat` 报告了四个文件的错误：`w`、`x`、`y` 和 `z`。基于冒号（`:`）的单词分割仅在变量 `a` 扩展 *之后* 发生。

Shell 根据 `IFS` 中找到的分隔字符，对命令行上所有 *已扩展* 的单词进行分割。如果没有扩展，就没有分割。考虑以下命令：

```
$ IFS="p"
$ export VAR
```

尽管 `IFS` 设置为 `p`，但 `export` 命令行中的 `p` 没有被扩展，因此单词 `export` 没有被分割。

以下示例使用变量扩展来尝试生成 `export` 命令：

```
$ IFS="p"
$ aa=export
$ echo $aa
ex ort
```

这次发生了扩展，因此 token `export` 中的字符 `p` 被解释为分隔符（如 `echo` 命令所示）。现在，当你尝试使用变量 `aa` 的值来导出变量 `VAR` 时，Shell 将 `aa VAR` 命令行解析为 `ex ort VAR`。其效果是命令行启动了 `ex` 编辑器，并带有两个文件名：`ort` 和 `VAR`。

```
$ ex ort VAR
2 files to edit
"ort" [New File]
Entering Ex mode.  Type  "visual" to go to Normal mode.

:q
E173: 1 more file to edit
:q
$
```

如果你取消设置 `IFS`，只有 SPACES（空格）和 TABs（制表符）可以作为字段分隔符。

### 多个分隔符字符

> > *提示* 虽然 Shell 将多个 SPACE 或 TAB 字符序列视为单个分隔符，但它将 *每个出现的* 其他字段分隔符字符视为分隔符。

### CDPATH：扩大 cd 的范围

`CDPATH` 变量允许你使用简单的文件名作为 `cd` 内置命令的参数，将工作目录更改为工作目录以外的目录。如果你通常在工作目录的几个目录之间切换，这个变量可以加快速度并省去使用 `cd` 配合较长路径名在它们之间切换的繁琐。

当 **CDPATH** 未设置且你指定一个简单的文件名作为 `cd` 的参数时，`cd` 在工作目录中搜索与参数同名的子目录。如果子目录不存在，`cd` 显示错误消息。当 **CDPATH** 设置时，`cd` 在 **CDPATH** 列表中的目录中搜索适当命名的子目录。如果找到，该目录成为工作目录。设置 **CDPATH** 后，你可以使用 `cd` 和一个简单的文件名将工作目录更改为 **CDPATH** 中列出的任何目录的子目录。

**CDPATH** 变量的值是冒号分隔的目录路径名列表（类似于 **PATH** 变量）。它通常在 `~/.bash_profile` 启动文件中通过如下命令行设置：

```
export CDPATH=$HOME:$HOME/literature
```

此命令使 `cd` 在你给出 `cd` 命令时，搜索你的主目录、**literature** 目录，然后是工作目录。如果你未在 **CDPATH** 中包含工作目录，`cd` 在 **CDPATH** 中所有其他目录的搜索失败后，会搜索工作目录。如果你想让 `cd` 首先搜索工作目录，请在 **CDPATH** 的第一个条目中包含一个空字符串，用两个冒号（`::`）表示：

```
export CDPATH=::$HOME:$HOME/literature
```

如果 `cd` 内置命令的参数是绝对路径名——以斜杠（`/`）开头——Shell 不会参考 **CDPATH**。

## 关键字变量：摘要

表 9-5 列出了 **bash** 关键字变量。

### 表 9-5 **bash** 关键字变量
| 变量 | 值 |
| :--- | :--- |
| **BASH_ENV** | 非交互式 Shell 的启动文件路径名（第 294 页） |
| **CDPATH** | `cd` 搜索路径（第 324 页） |
| **COLUMNS** | **select** 使用的显示宽度（第 983 页） |
| **FCEDIT** | `fc` 默认使用的编辑器名称（第 334 页） |
| **HISTFILE** | 保存历史列表的文件的路径名（默认：`~/.bash_history`；第 330 页） |
| **HISTFILESIZE** | 保存在 **HISTFILE** 中的最大条目数（默认：500；第 330 页） |
| **HISTSIZE** | 保存在历史列表中的最大条目数（默认：500；第 330 页） |

