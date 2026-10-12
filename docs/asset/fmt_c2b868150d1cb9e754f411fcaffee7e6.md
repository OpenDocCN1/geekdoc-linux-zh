
在以下示例中，用户输入 `bz` 并按 <kbd>TAB</kbd>。Shell 发出蜂鸣声（用户处于 emacs 模式），指示有多个命令以字母 `bz` 开头。用户输入另一个 <kbd>TAB</kbd> 使 shell 显示以 `bz` 开头的命令列表，后跟 `bz`，即用户到目前为止输入的命令行为：

```bash
$ bz →<kbd>TAB</kbd> <em>(beep)</em> →<kbd>TAB</kbd>
  bzcat      bzdiff     bzip2      bzless
  bzcmp      bzgrep     bzip2recover  bzmore
$ bz█
```

接下来，用户输入 `c` 并按 <kbd>TAB</kbd> 两次。Shell 显示以 `bzc` 开头的两个命令。用户输入 `a` 后跟 <kbd>TAB</kbd>，然后 shell 补全命令，因为只有一个命令以 `bzca` 开头。

```bash
$ bzc →<kbd>TAB</kbd> <em>(beep)</em> →<kbd>TAB</kbd>
  bzcat      bzcmp
$ bzca →<kbd>TAB</kbd> → t █
```

## 路径名补全

路径名补全同样使用 <kbd>TABs</kbd>，允许你输入路径名的一部分，并让 `bash` 提供其余部分。如果你输入的路径名部分足以确定一个唯一的路径名，`bash` 将显示该路径名。如果有多个路径名与之匹配，`bash` 将补全路径名直到有选择的点，以便你可以输入更多。

当你正在输入路径名（包括简单的文件名）并按下 <kbd>TAB</kbd> 时，shell 会发出蜂鸣声（如果 shell 处于 emacs 模式——在 vi 模式下没有蜂鸣声）。然后它将命令行扩展到尽可能远。

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
| `editing-mode` | 设置为 `vi` 可使 Readline 以 vi 模式启动。设置为 `emacs` 可使 Readline 以 emacs 模式启动（默认值）。类似于 `set -o vi` 和 `set -o emacs` Shell 命令（第 326 页）。 |
| `horizontal-scroll-mode` | 设置为 `on` 可使长行延伸到显示区域的右边缘之外。当光标位于显示区域的右边缘时向右移动，会将行向左移动，以便你可以看到更多行内容。通过让光标向左移出左边缘，可以将行移回。默认值为 `off`，这将导致长行换行到多行显示。 |
| `mark-directories` | 设置为 `off` 可使 Readline 在补全的目录名末尾不放置斜杠 `/`。通常它是 `on`。 |
| `mark-modified-lines` | 设置为 `on` 可使 Readline 在修改过的历史记录行前加一个星号。默认值为 `off`。 |

## 按键绑定

你可以指定绑定，将按键序列映射到 Readline 命令，从而允许你更改或扩展默认绑定。与 **emacs** 一样，Readline 库包含许多未绑定到按键序列的命令。要使用未绑定的命令，你必须使用以下形式之一进行映射：

```
keyname: command_name
"keystroke_sequence": command_name
```

在第一种形式中，你写出单个键的名称。例如，**CONTROL-u** 应写为 `control-u`。这种形式用于将命令绑定到单个键非常有用。

在第二种形式中，你指定一个描述按键序列的字符串，该序列将绑定到命令。你可以使用 **emacs** 风格的反斜杠转义序列来表示特殊键 **CONTROL (\C)**、**META (\M)** 和 **ESCAPE (\e)**。通过用另一个反斜杠转义来指定反斜杠：`\\`。类似地，双引号或单引号可以通过反斜杠转义：`"` 或 `'`。

`kill-whole-line` 命令仅在 **emacs** 模式下可用，它删除当前行。将以下命令放入 `.inputrc`，可以将 `kill-whole-line` 命令（默认未绑定）绑定到按键序列 `CONTROL-r`。

```
control-r: kill-whole-line
```

输入命令 `bind -P` 以显示所有 Readline 命令的列表。如果命令绑定到按键序列，则显示该序列。可以在 vi 模式中使用的命令以 vi 开头。例如，`vi-next-word` 和 `vi-prev-word` 分别将光标移动到下一个和上一个单词的开头。不以 vi 开头的命令通常在 **emacs** 模式下可用。

使用 `bind -q` 来确定哪个按键序列绑定到某个命令：

```
$ bind -q kill-whole-line
kill-whole-line can be invoked via "^C-r".
```

你还可以通过在双引号内包含引用来绑定文本（仅限 *emacs* 模式）：

```
"QQ": "The Linux Operating System"
```

当你输入 `QQ` 时，此命令会导致 *bash* 插入字符串 `The Linux Operating System`。

## 条件结构

你可以使用 `$if` 指令有条件地选择 *inputrc* 文件中的部分。条件结构的语法是

```
$if test[=value]
    commands
[$else
    commands]
$endif
```

其中 *test* 是 *mode*、*term* 或 *bash*。如果 *test* 等于 *value* 或者 *test* 为 *true*，此结构执行第一组 *commands*。如果 *test* 不等于 *value* 或者 *test* 为 *false*，如果存在则执行第二组 *commands*，如果不存在则退出该结构。

`$if` 指令的强大之处在于它可以执行三种类型的测试。

1. 你可以测试当前设置的模式。

   ```
   $if mode=vi
   ```

   如果当前 *Readline* 模式为 *vi*，上述测试为 *true*，否则为 *false*。你可以测试 `vi` 或 `emacs`。

2. 你可以测试终端类型。

   ```
   $if term=xterm
   ```

   如果 `TERM` 变量设置为 `xterm`，上述测试为 *true*。你可以测试 `TERM` 的任何值。

3. 你可以测试应用程序名称。

   ```
   $if bash
   ```

   当你运行 *bash* 而不是使用 *Readline* 库的其他程序时，上述测试为 *true*。你可以测试任何应用程序名称。
