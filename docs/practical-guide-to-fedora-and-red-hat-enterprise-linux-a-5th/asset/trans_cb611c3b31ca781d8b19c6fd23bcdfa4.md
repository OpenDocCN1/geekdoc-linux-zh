

在 `films` 目录下，每个以 `dar` 开头的文件接下来都跟着 `k_`，因此 `bash` 无法在不从文件中做出选择的情况下进一步扩展该行。光标会停留在 `_` 字符之后。此时，你可以继续键入路径名，或者按两次 `TAB`。在后者情况下，`bash` 会发出蜂鸣声，显示你的选项，重新显示命令行，并再次将光标置于 `_` 字符之后。

```
$ cat films/dar<TAB> (beep) cat films/dark_
```

当你添加足够的信息来区分这两个可能的文件并按下 `TAB` 时，`bash` 会显示唯一的路径名。如果在 `_` 字符后输入 `p` 并接着按 `TAB`，Shell 将补全命令行：

```
$ cat films/dark_p<TAB> passage
```

由于没有进一步的歧义，Shell 会追加一个 `SPACE`，以便你可以完成输入命令行，或者直接按 `RETURN` 执行命令。如果完整的路径名是目录，`bash` 会在 `SPACE` 的位置追加一个斜杠（`/`）。

## 变量补全

在键入变量名时，按下 `TAB` 会触发*变量补全*，此时 `bash` 会尝试补全变量名。如果出现歧义，按两次 `TAB` 将显示选项列表：

```
$ echo $HO<TAB>
HOME    HOSTNAME    SHOSTTYPE
$ echo $HOM<TAB>E
```

### 按 RETURN 执行命令

按下 `RETURN` 会促使 Shell 执行命令，无论光标在命令行上的位置如何。

### .inputrc：配置 Readline

Bourne Again Shell 以及其他使用 Readline 库的程序会读取由 `INPUTRC` 环境变量指定的文件，以获取初始化信息。如果未设置 `INPUTRC`，这些程序将读取 `~/.inputrc` 文件。它们会忽略 `.inputrc` 中为空的或以井号（`#`）开头的行。

## 变量

你可以在 `.inputrc` 中设置变量，以使用以下语法控制 Readline 库的行为：

```
set variable value
```

表 9-11（下一页）列出了一些可用的变量和值。有关完整列表，请参见 `bash` 手册页或 info 页中的*Readline 变量*部分。

| 变量 | 效果 |
| --- | --- |
| editing-mode | 设置为 vi 可使 Readline 以 vi 模式启动。设置为 emacs 可使 Readline 以 emacs 模式启动（默认值）。类似于 set -o vi 和 set -o emacs Shell 命令（第 326 页）。 |
| horizontal-scroll-mode | 设置为 on 可使长行延伸到显示区域的右边缘之外。当光标位于显示区域的右边缘时向右移动，会将行向左移动，以便你可以看到更多行内容。通过让光标向左移出左边缘，可以将行移回。默认值为 off，这将导致长行换行到多行显示。 |
| mark-directories | 设置为 off 可使 Readline 在补全的目录名末尾不放置斜杠 (/)。通常它是 on。 |
| mark-modified-lines | 设置为 on 可使 Readline 在修改过的历史记录行前加一个星号。默认值为 off。 |

## 按键绑定

你可以指定绑定，将按键序列映射到 Readline 命令，从而允许你更改或扩展默认绑定。与**emacs**一样，Readline 库包含许多未绑定到按键序列的命令。要使用未绑定的命令，你必须使用以下形式之一进行映射：

```
keyname: command_name
"keystroke_sequence": command_name
```

在第一种形式中，你写出单个键的名称。例如，**CONTROL-u** 应写为 **control-u**。这种形式用于将命令绑定到单个键非常有用。

在第二种形式中，你指定一个描述按键序列的字符串，该序列将绑定到命令。你可以使用**emacs**风格的反斜杠转义序列来表示特殊键**CONTROL (\C)**、**META (\M)**和**ESCAPE (\e)**。通过用另一个反斜杠转义来指定反斜杠：`\\`。类似地，双引号或单引号可以通过反斜杠转义：`"` 或 `'`。

**kill-whole-line** 命令仅在**emacs**模式下可用，它删除当前行。将以下命令放入 **.inputrc**，可以将**kill-whole-line**命令（默认未绑定）绑定到按键序列**CONTROL-r**。

```
control-r: kill-whole-line
```

输入命令**bind -P**以显示所有 Readline 命令的列表。如果命令绑定到按键序列，则显示该序列。可以在 vi 模式中使用的命令以 vi 开头。例如，**vi-next-word**和**vi-prev-word**分别将光标移动到下一个和上一个单词的开头。不以 vi 开头的命令通常在**emacs**模式下可用。

使用**bind -q**来确定哪个按键序列绑定到某个命令：

```
$ bind -q kill-whole-line
kill-whole-line can be invoked via "^C-r".
```

你还可以通过在双引号内包含引用来绑定文本（仅限*emacs*模式）：

```
"QQ": "The Linux Operating System"
```

当你输入 **QQ** 时，此命令会导致 *bash* 插入字符串 **The Linux Operating System**。

## 条件结构

你可以使用 $if 指令有条件地选择 *inputrc* 文件中的部分。条件结构的语法是

```
$if test[=value]
    commands
[$else
    commands]
$endif
```

其中 *test* 是 *mode*、*term* 或 *bash*。如果 *test* 等于 *value* 或者 *test* 为 *true*，此结构执行第一组 *commands*。如果 *test* 不等于 *value* 或者 *test* 为 *false*，如果存在则执行第二组 *commands*，如果不存在则退出该结构。

$if 指令的强大之处在于它可以执行三种类型的测试。

1. 你可以测试当前设置的模式。

   ```
   $if mode=vi
   ```

   如果当前 *Readline* 模式为 *vi*，上述测试为 *true*，否则为 *false*。你可以测试 *vi* 或 *emacs*。

2. 你可以测试终端类型。

   ```
   $if term=xterm
   ```

   如果 *TERM* 变量设置为 *xterm*，上述测试为 *true*。你可以测试 *TERM* 的任何值。

3. 你可以测试应用程序名称。

   ```
   $if bash
   ```

   当你运行 *bash* 而不是使用 *Readline* 库的其他程序时，上述测试为 *true*。你可以测试任何应用程序名称。

这些测试可以根据当前模式、终端类型和你正在使用的应用程序来定制 *Readline* 库。它们在与 *bash* 和其他程序一起使用 *Readline* 库时赋予了你极大的力量和灵活性。

**.inputrc** 中的以下命令使 CONTROL-y 无论 bash 处于 vi 还是 emacs 模式，都将光标移动到下一个单词的开头：

```
$ cat ~/.inputrc
  set editing-mode vi
  if mode=vi
    "\C-y": vi-next-word
  else
    "\C-y": forward-word
  endif
```

因为 *bash* 在启动时读取上述条件结构，所以你必须将编辑模式设置在 **.inputrc** 中。使用 *set* 交互式更改模式不会改变 CONTROL-y 的绑定。

有关 Readline 库的更多信息，请打开 *bash* 手册页并输入命令 */^READLINE*，该命令搜索行首的单词 READLINE。

### 如果 Readline 命令不起作用，请注销并重新登录

Bourne Again Shell 在你登录时读取 ~/.inputrc。在对这个文件进行修改后，你应该在测试更改之前先注销并重新登录。

## 别名

*别名* 是 Shell 将其转换为另一个（通常更长的）名称或（复杂的）命令的（通常较短的）名称。别名允许你通过用字符串替换简单命令的第一个标记来定义新命令。它们通常放置在 ~/.bashrc 启动文件中，以便对交互式子 Shell 可用。

*alias* 内建的语法是

```
alias [name=value]
```

等号周围不允许有空格。如果 *value* 包含空格或制表符，你必须用引号将 *value* 括起来。别名不接受来自 *命令行* 的 *value* 中的参数。当需要使用参数时，请使用函数（第 335 页）。

别名不会替换自身，这避免了对如下的别名进行无限递归处理的可能性：

```
$ alias ls='ls -F'
```

你可以嵌套别名。在非交互式 Shell（即 Shell 脚本）中，别名是被禁用的。要查看当前别名的列表，请键入命令 *alias*。要查看特定名称的别名，请输入 *alias* 后跟该名称且没有其他内容。你可以使用 *unalias* 内建命令删除别名。

