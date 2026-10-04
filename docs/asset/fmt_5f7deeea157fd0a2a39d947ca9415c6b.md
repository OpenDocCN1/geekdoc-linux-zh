
当你使用变量作为参数执行命令时，shell 会用变量的值替换变量名，并将该值传递给正在执行的程序。如果变量的值包含特殊字符（例如 `*` 或 `?`），shell 可能会扩展该变量。

在以下命令序列的第一行将字符串 `alex*` 赋值给变量 `memo`。Bourne Again Shell 在给变量赋值时不会扩展字符串；bash 在变量赋值时不执行路径名扩展（第 239 页）。所有 shell 都会按照特定的顺序处理命令行。在这个顺序中，bash 在解释命令之前扩展变量。在接下来的 `echo` 命令行中，双引号引用了 `$memo` 扩展值中的星号（`*`），并防止 bash 对扩展后的 `memo` 变量进行路径名扩展，将其值传递给 `echo` 命令：

```
$ memo=alex*
$ echo "$memo"
alex*
```

当你引用一个包含未引号特殊字符的变量时，所有 shell 都会将特殊字符视为特殊。在以下示例中，shell 扩展了 `memo` 变量的值，因为它没有加引号：

```
$ ls
alex.report
alex.summary
$ echo $memo
alex.report alex.summary
```

在这里，shell 将变量扩展为 `alex*`，再将 `alex*` 扩展为 `alex.report` 和 `alex.summary`，并将这两个值传递给 `echo`。

`$VARIABLE` 语法是更通用语法 `${VARIABLE}` 的特例，变量名包含在 `${}` 中。括号保护了变量名。将变量值与字符串拼接时，括号是必须的：

```
$ PREF=counter
$ WAY=$PREF
$ FAKE=$PREF
$ echo $SWAY $FAKE
```

上面的示例没有按预期工作。虽然 `PREclockwise` 和 `PREfeit` 是有效的变量名，但它们尚未设置。bash 默认将未设置的变量评估为空（null）字符串并显示此值。要实现这些语句的意图，请使用括号引用 PREF：

```
$ PREF=counter
$ WAY=${PREF}clockwise
$ FAKE=${PREF}feit
$ echo $SWAY $FAKE
counterclockwise counterfeit
```

Bourne Shell 使用位置引用命令行参数，使用 `$1`、`$2` 直到 `$9`。如果要引用第十个参数，必须使用括号： `${10}`。命令名称存储在 `$0` 中（第 439 页）。

## unset 移除变量

除非移除变量，否则将在创建它的 shell 中一直存在。要移除变量的值而非变量本身，将其赋值为空：

```
$ person=
$ echo Person
```

你可以使用 `unset` 内置命令移除变量。移除变量 `person` 请执行以下命令：

```
$ unset person
```

## 变量属性

本节讨论属性并解释如何为变量分配属性。

### readonly：使变量值永久

你可以使用 `readonly` 内置命令确保变量的值无法被更改。接下来的示例详细介绍了只读变量 `person`。你必须在声明只读之前为其赋值；声明后无法更改其值。当你尝试取消或更改只读变量的值时，shell 会显示错误信息：

```
$ person=jenny
$ echo Person
jenny
$ readonly person
$ person=helen
bash: readonly variable
```

如果不带参数使用 `readonly` 命令，它将列出所有只读 shell 变量。此列表包含了自动设置为只读的关键字变量以及你声明为只读的关键字或用户创建变量。参见第 300 页的“列出属性”（readonly 和 declare -r 输出相同）。

### declare 和 typeset：为变量分配属性

`declare` 和 `typeset` 内置命令（同一命令的两个名称）为 shell 变量设置属性和值。表 9-3 列出了其中的五个属性。

#### 表 9-3 变量属性（设置或声明）

| 属性 | 含义 |
| :--- | :--- |
| -a | 将变量声明为数组（第 432 页） |
| -f | 将变量声明为函数名（第 331 页） |
| -i | 将变量声明为整数类型（第 301 页） |
| -r | 将变量设置为只读；也可用 readonly（第 299 页） |
| -x | 导出变量（变为全局）；也可用 export（第 434 页） |

以下命令声明了几个变量并设置了一些属性。第一行声明了 person1 并给其赋值为 alex。无论是否包含 `declare` 单词，该命令的效果相同。

```bash
$ declare person1=alex
$ declare -rx person2=jenny
$ declare -rx person3=helen
$ declare -x person4
```

`readonly` 和 `export` 内置分别是命令 `declare -r` 和 `-x` 的同义词。在不给变量赋值的情况下声明变量是合法的，如前面对变量 `person4` 的声明所示。此声明使 `person4` 对所有子壳可用（变为全局）。在对变量进行赋值之前，它的值为空。

你可以按照任何顺序单独列出 `declare` 的选项。以下内容与之前的 `person3` 声明等效：

```bash
$ declare -x -r person3=helen
```

当你想要从变量中删除属性时，使用 `+` 字符代替 `-`。在执行以下命令后，变量 `person3` 不再被导出，但仍然是只读的。

```bash
$ declare +x person3
```

你可以使用 `typeset` 代替 `declare`。

没有任何选项的情况下列出变量属性，`declare` 内置会列出所有 shell 变量。当你不带参数运行 `set`（第 442 页）时，也会输出相同的列表。

如果你使用带有选项的 `declare` 内置但没有变量名作为参数，命令将显示所有设置了指定属性的变量。例如，配合 `declare` 使用 `-r` 选项会列出所有只读 shell 变量。此列表与不带任何参数的 `readonly` 命令产生的列表相同。在给出的示例声明后，结果如下：

```bash
$ declare -r
declare -ir BASH_VERSINFO='([0]="2" [1]="05b" [2]="0" [3]="1" ... )'
declare -ir UID="500"
declare -ir PPID="936"
declare -r SHELLOPTS=braceexpand:emacs:hashall:histextend:history...
declare -ir UID="500"
declare -r person2="jenny"
declare -rx person3="helen"
```

前五个项目是自动声明为只读的关键字变量。其中一些变量以整数形式存储（-）。指示 `BASH_VERSINFO` 是数组变量的 `-a` 选项；数组每个元素的值列在等号右侧。

变量的默认值是字符串。当你对字符串变量进行算运算时，shell 会将变量转换为数字进行处理，然后转换回字符串。具有整数属性的变量以整数形式存储。如下所示分配整数属性：

```bash
$ typeset -i COUNT
```

## 关键字变量

关键字变量要么是被继承的，要么是在 shell 启动时声明并初始化的。你可以从命令行或启动文件为这些变量赋值。通常你希望这些变量适用于你启动的所有子壳，并由 shell 自动导出，此时你必须使用 `export`（第 434 页）使它们对子壳可用。

### HOME: 你的主目录

默认情况下，你的主目录是你登录时的工作目录。你的主目录在你建立账户时确定；其名称存储在 `/etc/passwd` 中。

```bash
$ grep sam /etc/passwd
sam:501:501:Sam 5:/home/sam:/bin/bash
```

登录时，shell 会继承你主目录的路径并将其赋值给变量 `HOME`。当你不带参数给出 `cd` 命令时，它会将存储在 HOME 中的目录目录设置为工作目录：

```bash
$ pwd
/home/alex/laptop
$ echo $HOME
/home/alex
$ cd
$ pwd
/home/alex
```

此示例显示了 `HOME` 变量的值以及 `cd` 内置的效果。执行不带参数的 `cd` 后，工作目录的路径与 `HOME` 的值相同：即你的主目录。

波浪线 (`~`)：shell 使用 `HOME` 的值来展开使用波浪线（~）符号（第 190 页）表示用户主目录的路径。以下示例使用 `echo` 显示此快捷方式的值，然后使用 `ls` 列出 Alex `laptop` 目录中的文件，该目录是他主目录的子目录：

```bash
$ echo ~
/home/alex
ls ~laptop
tester count lineup
```

### PATH: 程序的 shell 路径

当你给 shell 一个绝对或相对路径而不是简单的文件名作为命令时，它会在指定的目录查找具有指定文件名的可执行文件。如果指定路径的文件不存在，shell 会报告未找到命令。如果文件按指定存在但你没有其执行权限，或者对于 shell 脚本，你没有读取和执行权限，shell 将报告权限被拒绝。

如果你给出简单的文件名作为命令，shell 将在 `PATH` 中搜索。

## 参数与变量

将工作目录放入 `PATH` 可能会创建一个安全漏洞。如果你是 root 用户，绝不应该将工作目录放入 `PATH`。

## 304 第 9 章 再次回归 Bourne 外壳

你可以自定义 PS1 显示的提示符。例如，通过赋值：

```
$ PS1="\u@\h W \!$ "
```

会显示以下提示符：

```
[user@host directory event|$]
```

其中 user 是用户名，host 是第一个点之前的基名，directory 是工作目录的基名，而 event 是当前命令的事件号。

如果你在多个系统上工作，将系统名称整合到提示符中可能会很有。例如，你可能将提示符更改为你正在使用的系统名称，后面跟着一个冒号和一个空格（在提示符末尾加空格使得你在提示符后输入的命令更易读）：

```
$ PS1="$(hostname): "
```
bravo.example.com: echo test
bravo.example.com:

接随后的第一个示例将提示符更改为本地主机名、空格和一个美元符号（如果用户以 root 权限运行，则是井号）。第二个示例将提示符更改为时间后跟用户名。第三个示例将提示符更改为书中使用的提示符（root 用户用井号，否则用美元符号）：

```
$ PS1=\h \$ '
bravo $
```

```
$ PS1='\@ \u $\$'
09:44 PM alex $
```

```
$ PS1=\$ ''
$
```

表 9-4 描述了你可以在 PS1 中使用的一些符号。要获取提示符字符串中可以使用字符完整列表，请打开 bash man 手页并搜索 PROMPTING 的第二次出现（输入命令 `/PROMPTING` 然后按 n）。

#### 表 9-4 PS1 符号

| 符号 | 在提示符中的显示 |
| :--- | :--- |
| $ | 如果用户以 root 权限运行；否则为 $ |
| \w | 工作目录的路径名 |
| \W | 工作目录的基名 |
| \! | 当前事件（历史）编号（第 317 页） |
| \d | “星期 月 日”格式的日期 |

#### 表 9-4 PS1 符号（续）

| 符号 | 在提示符中的显示 |
| :--- | :--- |
| \h | 机器主机名，不带域名 |
| \H | 完整主机名，包含域名 |
| \u | 当前用户的用户名 |
| \@ | 12 小时制 AM/PM 格式的当前时间 |
| \T | 12 小时 HH:MM:SS 格式的当前时间 |
| \A | 24 小时 HH:MM 格式的当前时间 |
| \t | 24 小时 HH:MM:SS 格式的当前时间 |

### PS2：用户提示符（次）

提示符字符串 2（Prompt String 2）是 存储在 PS2 中的次提示符。在下一个示例的第一行，echo 后面跟着一个未关闭的引号字符串。shell 假设命令尚未完成并在第二行给出默认的次提示符 (`>`)。此提示符表示 shell 正在等待用户继续命令行。shell 会一直等待直到收到关闭字符串的引号，然后执行命令：

```
$ "demonstration of prompt string"
> 2"
demonstration of prompt string
2
$ PS2>"secondary prompt:"
$ echo "this demonstrates"
secondary prompt: prompt string 2"
this demonstrates
prompt string 2
```

第二个命令将次提示符更改为 `secondary prompt:` 后面跟一个空格。多行 echo 演示了新的提示符。

### PS3：菜单提示符

PS3 存储 select 控制结构的菜单提示符（第 426 页）。

### PS4：调试提示符

PS4 存储 bash 调试符号（第 408 页）。

### IFS：分隔输入字段（单词拆分）

IFS（内部字段分隔符）变量指定了你可以用于分隔命令行参数的字符，其默认值为空格、制表符和换行。无论 IFS 的值如何，只要这些字符未被引号引用或转义，你就可以一个或多个空格/制表符来分隔命令行上的参数。当你分配 IFS 字符值时，这些字符也可以分隔字段，但仅当它们经过扩展时。这种对命令行的解释被称为单词拆分。

## 更改 IFS 时要小心

> 注意：更改 IFS 有多种种副作用，因此请谨慎操作。你可能会发现先在更改之前保存 IFS 的值是有帮助的；如果得到意外结果，可以轻松恢复原始值。或者，你可以在实验 IFS 之前，使用 bash 命令派生一个新的 shell；如果遇到麻烦，退出回到旧 shell，那里的 IFS 工作正常。你还可以通过以下命令将 IFS 设置为默认值：
>
> ```
> $ IFS=' \t\n'
> ```

以下示例演示了设置 IFS 如何影响对命令行的解释：

```
$ a=w:x:y:z
$ cat $a
cat: w:x:y:z: No such file or directory
$ IFS=":"
$ cat $a
cat: w: No such file or directory
cat: x: No such file or directory
cat: y: No such file or directory
cat: z: No such file or directory
```
