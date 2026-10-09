
由于内置命令 `echo` 将其参数复制到标准输出，你可以使用它来显示变量的值。

预测示例的第二行 `person` 并不代表 `ale`。相反，字符串 `person` 被回显为 `person`。只有当你在变量名前加上美元符号 `$` 时，`shell` 才会替换变量的值。命令 `echo $person` 显示的是变量 `person` 的值；它不会显示 `Person`，因为 `shell` 没有将 `Person` 作为参数传递给 `echo`。由于存在领先的 `$`，`shell` 识别出 `Person` 是变量名，替换了变量的值，并将该值传递给 `echo`。`echo` 显示的是变量的值，而不是变量名，它完全不知道你称它为变量。

### 转义 `$`

你可以通过对 `$` 进行引用来防止 `shell` 替换变量的值。双引号不会阻止替换；单引号或反斜杠 (`\`) 可以。

```
$ echo Person
alex
$ echo "Person"
alex
$ echo 'Person'
person
$ echo \$Person
person
```

### 空格

由于双引号不会阻止大多数其他字符的特殊含义，因此在为变量赋值以及使用这些值时，双引号非常有用。要为变量赋值包含空格或制表符（`TAB`）的值，请在值周围使用双引号。虽然在所有情况下并不需要双引号：

```
$ person="alex and jenny"
$ echo $person
alex and jenny
```

如果你不对变量进行引用，`shell` 会将每个空格合并为一个空格。

```
$ person="alex and jenny"
$ echo $person
alex and jenny
```

*(注：此处原文示例输出似乎有误，根据逻辑应为合并后的效果，见下文)*

```
$ person="alex and jenny"
$ echo $person
alexandjenny
```

### 赋值中的路径扩展

`$VARIABLE` 语法是更通用的 `${VARIABLE}` 语法的特例，其中变量名被 `{}`` 包围。括号隔离了变量名。在将变量值与字符串拼接时，括号是必要的：

```
$ PREF=counter
$ WAY=$PREFclock
$ FAKE=$PREFeit
$ echo $WAY $FAKE
```

```
$
```

上面的示例没有按照预期工作。只输出了一个空行，因为虽然符号 `PREclock` 和 `PREFeit` 是有效的变量名，但它们没有设置。默认情况下，`bash` 将未设置的变量评估为空（空）字符串并显示该值。要这些语句的意图，请使用括号引用 `PREF` 变量：

```
$ PREF=counter
$ WAY=${PREF}clock
$ FAKE=${PREF}feit
$ echo $WAY $FAKE
counterclockwise counterfeit
```

`shell` 通过位置引用命令行上的参数，使用特殊变量 `$1`, `$2`, `$3` 直到 `$9`。如果你想引用第九个之后的参数，必须使用括号 `${10}`。命令名称存储在 `$0` 中（第 921 页）。

### `unset`：删除变量

除非你删除变量，否则只要创建它的 `shell` 存在，变量就会存在。要删除变量的值但不删除变量本身，请将其值设置为空：

```
$ person=
$ echo $person
```

```
$
```

你可以使用 `unset` 内置命令删除变量。要删除变量 `person`，请执行以下命令：

```
$ unset person
```

## 变量属性

本节讨论了属性，并解释了如何将它们分配给变量。

`readonly`：使变量的值持久化

你可以不带参数使用 `readonly` 内置命令来确保变量的值不能被更改。下一个示例将变量 `person` 声明为只读。在将变量声明为只读之前，你必须先给变量赋值；声明后，你不能更改它的值。当你尝试取消只读或更改只读变量的值时，`shell` 会显示错误信息：

```
$ person=jenny
$ echo $person
jenny
$ readonly person
$ person=helen
bash: readonly variable
```

如果你不带参数使用 `readonly` 内置命令，它会列出所有只读的 `shell` 变量。此列表包含了自动设置为只读的关键字变量，以及你声明为只读的用户创建的变量。参见[列出变量属性](page 290) 关于 `readonly` 和 `declare -r` 产生相同输出的示例。

`declare` 和 `typeset`：为变量分配属性

`declare` 和 `typeset` 内置命令（同一个命令的不同名称）用于为 `shell` 变量设置属性和值。[表 9-3] 列出了这些属性中的五个。

## 表 9-3. 变量属性 (`typeset` 或 `declare`)

| 属性 | 含义 |
| --- | --- |
| `-a` | 将变量声明为数组（page 914） |
| `-f` | 将变量声明为函数名（page 321） |
| `-i` | 将变量声明为整数类型（page 291） |
| `-r` | 使变量只读；`readonly`（page 289） |
| `-x` | 导出变量（变为全局变量）；也称为 `export`（page 916） |

以下命令声明了变量并设置了一些属性。第一行声明了 `person1` 并赋值为 `alex`。无论是否包含 `declare` 单词，该命令的效果都是相同的。

```
$ declare person1=alex
$ declare -r person2=jenny
$ declare -rx person3=helen
$ declare -x person4
```

`readonly` 和 `export` 内置命令分别是命令 `declare -r` 和 `declare -x` 的同义词。在声明变量时不为其赋值是合法的，正如前面对变量 `person4` 的声明所示。此声明使得 `person4` 可供子 `shell` 使用（使其变为全局变量）。在对变量进行赋值之前，它的值是空。

你可以按任何顺序单独列出选项。以下等同于前面对 `person3` 的声明：

```
$ declare -x -r person3=helen
```

使用 `+` 代替你想要从变量中移除属性的地方。然而，你不能移除只读属性。执行以下命令后，变量 `person3` 不再被导出，但它仍然是只读。

```
$ declare +x person3
```

你也可以使用 `typeset` 代替 `declare`。

### 列出变量属性

在不带任何参数或选项的情况下，`declare` 内置命令列出所有 `shell` 变量。在不带任何参数重新运行时（page 924），会输出相同的列表。

如果你使用带选项的 `declare` 内置命令但不带变量名参数，该命令将列出所有设置了指定属性的 `shell` 变量。例如，配合 `declare` 使用 `r` 选项会给出所有只读变量的列表。此列表与不带任何参数的 `readonly` 命令产生的列表相同。在执行前面示例中的声明后，结果如下：

```
$ declare
declare -ar BASH_VERSINFO=[0]="2" [1]="05" [2]="0" [3]="1" ...
declare -ir EU="50"
declare -ir PPID="936"
declare -rt SHELLOPTS="braceexpand:emacs:hash:htextand:history:..."
declare -ir UID="500"
declare -rt person2="jenny"
declare -rx person3="helen"
```

前五项是自动声明为只读的变量。其中某些变量是整数（`i`）。`-a` 选项表示 `BASH_VERSINFO` 是一个数组；数组每个元素的值列在等号右侧。

### 整数

默认情况下，变量作为字符串存储。当你对字符串变量进行算术运算时，`shell` 会将其转换为数字，进行处理，然后转换回字符串。具有整数属性的变量作为整数存储。通过如下方式分配整数属性：

```
$ typeset -i COUNT
```

## 关键字变量

关键字变量是在 `shell` 启动时继承或由 `shell` 声明的。你可以从命令行或启动文件为这些变量赋值。通常，你希望这些变量适用于你启动的所有子 `shell` 以及你的登录 `shell`。对于 `shell` 未自动导出的变量，你必须使用 `export`（page 916）让它们对子 `shell` 可用。

## `HOME`: 你的主目录

默认情况下，主目录是你登录时的工作目录。主目录在你建立账户时确定；它的名称存储在 `/etc/passwd` 文件中。

```
$ grep sam /etc/passwd
sam:x:501:5:Sam x:301:/home/sam:/bin/bash
```

当你登录时，`shell` 会继承主目录的路径。

```
$ pwd
/home/sam
```

### 波浪号

波浪号 (`~`) 是主目录的快捷方式。`shell` 将波浪号扩展为用户的主目录。如果你在命令中使用波浪号，`shell` 会将其扩展为主目录。

```
$ echo ~
/home/sam
```

## `PATH`: `shell` 查找的位置

`PATH` 变量是 `shell` 搜索命令的目录列表。当你输入命令时，`shell` 按 `PATH` 中列出的顺序搜索目录。如果在其中一个目录中找到了命令，`shell` 将执行它。如果不在任何目录中都找到命令，`shell` 将显示“找不到命令”错误。

默认 `PATH` 包含几个标准目录。你可以通过给它赋值新值来更改 `PATH`。

```bash
$ PATH=/usr/bin:/bin:/sbin
```

### 安全：`PATH` 与安全

在考虑安全时，不要将工作目录放入 `PATH`。如果你以超级用户（`Superuser`）身份运行，绝不要将工作目录放在 `PATH` 的前面。将工作目录放在 `PATH` 头部可能会导致安全漏洞。如果目录所有者包含一个名为命令的可执行文件，且该工作目录出现在用户的 `PATH` 中，那么用户在工作目录输入命令时将执行该文件而不是系统工具，这可能导致意外的结果。

## `MAIL`: 你的邮件存储在哪里

`MAIL` 变量包含存储邮箱箱文件的路径，通常为 `/var/spool/mail/name`，其中 `name` 是你的用户名。如果设置了 `MAIL` 而没有 `MAILPATH`，当有新邮件到达 `MAIL` 指定的文件时，`shell` 会通知你。在图形环境中，你使用 `MAIL` 是为了防止 `shell` 在终端模拟器中显示提醒（假设你正在使用图形程序）。

## `PS1`: 用户提示符（主）

默认的 `Bourne Shell` 提示符是美元符号 (`$`)。当你以 `root` 身份运行 `bash` 时，你可能会看到井号 (`#`) 提示符。`PS1` 变量持有 `shell` 用来告知你它正在等待输入命令的提示符字符串。当你更改 `PS1` 的值时，你就会更改提示符的外观。

你可以自定义 `PS1` 显示的提示符。例如，以下赋值操作：

```
$ PS1="[u@h \W \$]"
```

将显示以下提示符：

```
[user@host directory event]$
```

其中 `user` 是用户名，`host` 是主机名，`directory` 是工作目录的基名（`basename`），`event` 是当前命令的事件号。

如果你在多个系统上工作，将系统名称包含在提示符中可能会很有帮助。例如，可以将提示符更改为你正在使用的系统名称，后面加冒号和空格（在提示符末尾加空格可以使得你在提示符后输入的命令更易读）：

```
$ PS1="$(hostname)"
bravo.example.com: echo test
test
bravo.example.com:
```

第一个示例将提示符更改为本地主机名、一个空格和一个美元符号（或者，如果用户运行 `root`，则是井号）。第二个示例将提示符更改为时间，后跟用户名。第三个示例将提示符更改为书中使用的提示符（`root` 对应井号，否则为美元符号）：

```
$ PS1="\h \$ *"
bravo $
```

```
$ PS1="\@ u \$"
09:44 PM alex $
```

```
$ PS1="\$"
$
```

表 9-4 描述了你可以在 `PS1` 中使用的一些符号。要获得提示符字符串中使用的特殊字符完整列表，请打开 `bash` `man` 手页并搜索 `PROMPTING` 的第二次出现（输入命令 `/PROMPTING` 然后按 `n`）。

## 表 9-4. `PS1` 符号

| 符号 | 在提示符中的显示 |
| --- | --- |
| `\$` | 如果用户以 `root` 身份运行则为 `#`；否则为 `$` |
| `\w` | 工作目录的路径 |
| `\W` | 工作目录的基名 |
| `\!` | 当前事件（历史）编号（第 307 页） |
| `\d` | “星期 月份 日”格式的日期 |
| `\h` | 不带域名的机器主机名 |
| `\H` | 包含域名的完整主机名 |
| `\u` | 当前用户的用户名 |
| `\@` | 12 小时制 `AM/PM` 格式的当前时间 |
| `\T` | 12 小时制 `HH:MM:SS` 格式的当前时间 |
| `\A` | 24 小时制 `HH:MM:SS` 格式的当前时间 |
| `\t` | 24 小时制 `HH:MM:SS` 格式的当前时间 |

## `PS2`: 用户提示符（次）

提示符字符串 2 是 `shell` 存储在 `PS2` 中的次提示符。在接下来的示例的第一行中，`echo` 后面跟着一个未闭合的引号字符串。`shell` 假设命令尚未完成，并在第二行给出默认的次提示符 (`$`)；此提示符表示 `shell` 正在等待用户继续输入命令行。`shell` 会一直等待接收到引号，然后该引号会闭合并执行命令：

```
$ echo "demonstration of prompt string\n- 2"
$ PS2="secondary prompt: "
$ echo "this demonstrates\nprompt string 2"
secondary prompt:
this demonstrates
prompt string 2
```

第二个命令将次提示符更改为 `secondary prompt: `（后面跟一个空格）。多行 `echo` 演示了新的提示符。

## `PS3`: 菜单提示符

`PS3` 持有 `select` 控制结构的菜单提示符（第 908 页）。

## `PS4`: 调试提示符

`PS4` 持有 `bash` 调试符号（第 890 页）。

## `IFS`: 分隔输入字段（单词拆分）

`IFS`（内部字段分隔符）`shell` 变量指定用于分隔命令行参数的字符，其默认值为空格、制表符、换行。无论 `IFS` 的值是什么，只要这些字符没有被引用或转义，你就可以使用一个或多个空格制表符来分隔命令行上的参数。当你分配 `IFS` 字符值时，只有这些字符经过扩展后才能分隔字段。这种对命令行的解释方式被称为单词拆分（`word splitting`）。

### 注意：更改 `IFS` 时要小心

更改 `IFS` 有各种副作用，因此请谨慎操作。在更改 `IFS` 之前保存 `IFS` 的值可能会很有用；如果得到意料之外的结果，你可以恢复原始值。或者，你可以在尝试 `IFS` 之前用 `bash` 命令派生一个新的 `shell`；如果你遇到麻烦，可以退出回到旧的 `shell`，那里的 `IFS` 运行正常。你也可以通过以下命令将 `IFS` 设置为其默认值：

```
$ IFS='\t'
```

下面的示例演示了 `IFS` 如何影响对命令行的解释：

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

第一次调用 `cat` 时，`shell` 将变量 `w:x:y:z` 扩展为单个单词作为 `cat` 的参数。`cat` 报错 `w:x:y:z: No such file or directory`。设置 `IFS=":"` 后，再次执行 `cat $a`，`cat` 分别处理 `w`、`x`、`y`、`z`，每个都报错文件不存在。

第一次 `cat` 调用时，`shell` 将变量 `w:x:y:z` 扩展为单个单词作为 `cat` 的参数。`cat` 找不到名为 `w:x:y:z` 的文件。设置 `IFS` 为冒号 (`:`) 后，`shell` 扩展变量为四个单词。`cat` 查找 `w`、`x`、`y`、`z`。

如果你取消设置 `IFS`，只有空格和制表符被视为分隔符。

（示例）

```
$ IFS='\t'
```

### 提示：多个分隔符

虽然多个空格或制表符序列被视为单个分隔符，但每个其他字段字符的出现都会作为分隔符。

（示例）

```
$ a=w:x:y:z
$ cat $a
cat: w:x:y:z: No such file or directory
```

## `CDPATH`: 扩展 `cd` 的范围

`CDPATH` 变量允许你使用简单文件名作为 `cd` 内置命令的参数，以切换到工作目录以外的目录。如果你有多个可以工作的目录，这个变量可以加快速度，并避免使用长路径在它们之间进行切换。

当 `CDPATH` 未设置且你指定简单文件名作为参数时，`cd` 在工作目录中搜索同名子目录。如果子目录不存在，`cd` 将显示错误消息。当 `CDPATH` 设置后，`cd` 在 `CDPATH` 中的目录中搜索指定的子目录。如果 `cd` 找到了，该目录将成为工作目录。设置 `CDPATH` 后，你可以使用 `cd` 和简单文件名将工作目录更改为 `CDPATH` 中列出的任何目录的子目录。

```
export CDPATH=$HOME:$literature
```
