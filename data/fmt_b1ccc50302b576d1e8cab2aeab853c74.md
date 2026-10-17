
```bash
$ script.sh arg1 arg2
$ echo $1  # 输出 arg1
$ echo $2  # 输出 arg2
```

**特殊参数**

Shell 有一些特殊参数可以提供有用信息：

- `$0`：当前脚本的名字。
- `$#`：参数的个数。
- `$*`：所有参数的列表。
- `$@`：所有参数本身。
- `$?`：上一个命令的退出状态。
- `$$`：当前 shell 进程的 ID (`PID`)。
- `$!`：最近一个后台作业的 PID。

```bash
$ script.sh a b c
$ echo $# # 输出 3
$ echo $* # 输出 a b c
$ echo $@ # 输出 a b c
```

空格（SPACES）由于双引号不会阻止变量替换，而只是关闭大多数其他字符的特殊含义，因此在给变量赋值以及使用这些值时，双引号是非常有用的。要给变量赋值包含空格或制表符（TABs）的值，请在值周围使用双引号。虽然并不是所有情况下都需要双引号，但使用它们是一个好习惯。

```bash
$ person="max and zach"
$ echo $person
max and zach
$ person=max and zach
bash: echo command not found
```

当你引用一个值包含制表符或多个相邻空格的变量时，你需要使用引号来保留间距。如果你不对变量加引号，shell 在将变量传递给实用程序之前，会将每个字符字符串收缩为单个空格（SPACE）：

```bash
$ person="max and zach"
$ echo $person
max and zach
$ echo "*$person"
max and zach
```

### 路径扩展（Pathname expansion）

当你执行一个带有变量作为参数的命令时，shell 会将变量名替换为变量的值并将其传递给正在执行的程序。如果变量包含特殊字符，例如 `*` 或 `?`，shell 可能会展开该变量。

以下命令序列中的第一行将字符串 `*` 赋值给变量 `memo`。Bourne Again Shell 在变量赋值时不会展开该字符串，因为它在给变量赋值时会进行路径扩展（见第 256 页）。所有的 shell 都会按照特定的顺序处理命令行。在这个顺序中，`bash` 扩展在解释命令之前进行展开，双引号引用了 `$memo` 展开后的值中的星号 (`*`)，并防止了 `bash` 在将值传递给 `echo` 命令之前对展开后的 `memo` 变量执行路径扩展：

```bash
$ memo=*
$ echo "$memo"
max*
```

当你在引用一个包含未加引号的特殊字符的变量时，所有的 shell 都会将特殊字符解释为特殊。在下面的示例中，shell 展开了 `memo` 变量的值，因为它没有加引号：

```bash
$ memo=.*
max.report
max.summary
$ echo $memo
max.report max.summary
```

在这里，shell 将 `$memo` 变量展开为 `max*`，将 `max*` 展开为 `max.report` 和 `max.summary`，然后将这两个值传递给 `echo`。

`$VARIABLE` 语法是更通用语法 `${VARIABLE}` 的特殊情况，其中变量名被 `${}` 包围。大括号将变量名与相邻字符隔离开。在将变量值与字符串拼接时，大括号是必要的：

```bash
$ PREF=counter
$ WAY=$PREFclockwise
$ FAKE=$PREFFeit
$ echo SWAY $FAKE
```

上一个示例并没有按预期工作。只输出了空行，因为虽然 `PREFclockwise` 和 `PREFFeit` 符号是变量名，但它们没有被设置。默认情况下，`bash` 将未设置的变量评估为空字符串（null）并显示该值。要实现这些语句的意图，请使用括号引用 `PREF` 变量：

```bash
$ PREF=counter
$ WAY=${PREF}clockwise
$ FAKE=${PREF}feit
$ echo SWAY $FAKE
counterclockwise counterfeit
```

Bourne Again Shell 通过位置引用其命令行上的参数，使用特殊变量 `$1, $2, $3` 等到 `$9`。如果你想引用超过第九个的参数，必须使用大括号：`${10}`。命令名称存储在 `$0` 中（见第 997 页）。

# unset：移除变量

除非你删除变量，否则它将存在于创建它的 shell 中。要移除变量的值但不移除变量本身，请给变量赋一个空值：

```bash
$ person=
$ echo $person
```

你可以使用 `unset` 内置命令移除变量。以下命令移除了变量 `person`：

```bash
$ unset person
```

# 变量属性（VARIABLE ATTRIBUTES）

本节讨论了属性并解释了如何将它们分配给变量。

# readonly：使变量值永久

你可以使用 `readonly` 内置命令确保变量的值不能被更改。下一个示例将变量 `person` 声明为只读。在将其声明为只读之前，你必须给变量赋值；在声明之后不能更改它。当你尝试 `unset` 或更改只读变量的值时，shell 会显示错误消息：

```bash
$ person=zach
$ echo $person
zach
$ readonly person
$ person: readonly variable
```

如果你在不带参数的情况下使用 `readonly` 内置命令，它会列出所有只读 shell 变量。这包括自动设置为只读的关键字，以及你声明为只读的用户创建的变量。示例参见第 318 页（`readonly` 和 `declare -r` 产生相同的输出）。

# declare 和 typeset：为变量分配属性

`declare` 和 `typeset`（同一命令的两个名称）用于设置 shell 变量的属性和值。表 9-3 列出了这些属性中的五个。

表 9-3 变量属性 (`typeset` 或 `declare`)

| 属性 | 含义 |
| :--- | :--- |
| `-a` | 将变量声明为数组（第 990 页） |
| `-f` | 将变量声明为函数名（第 349 页） |
| `-i` | 将变量声明为整数类型（第 318 页） |
| `-r` | 使变量变为只读；也可用 `readonly`（第 317 页） |
| `-x` | 导出变量（变为全局）；也可用 `export`（第 992 页） |

以下命令声明了几个变量并设置了一些属性。第一行声明了 `person1` 并为其赋值为 `max`。此命令无论带带有 `declare` 单词，效果都是相同的。

```bash
$ declare person1=max
$ declare -r person2=zach
$ declare -rx person3=helen
$ declare -x person4
```

# 318 第 9 章 BOURNE AGAIN SHELL

`readonly` 和 `export` 内置命令分别是 `declare -r` `-x` 的同义词。你可以在不给变量赋值的情况下声明变量，正如前面对变量 `person4` 的声明所示。此声明使得 `person4` 对所有子 shell 可用（即使其变为全局）。在对变量进行赋值之前，它的值为空值。

你可以按照任何顺序单独列出选项。以下与前面对 `person3` 的声明等效：

```bash
$ declare -xr person3=helen
```

当你想要从变量中移除属性时，用 `+` 字符代替 `-`。你不能移除该属性。在执行以下命令后，变量 `person3` 不再被导出，但它仍然是只读的。

```bash
$ declare +x person3
```

你可以使用 `unset` 代替 `declare`。在不带任何参数或选项的情况下，shell...

# 关键字变量（KEYWORD VARIABLES）

关键字变量是在 shell 启动时被继承或初始化的。你可以从命令行或启动文件为变量赋值。通常，你希望变量适用于你启动的所有子 shell。

# HOME：你的目录

默认情况下，登录时你的主目录就是工作目录。你的主目录在设置账户时建立；其名称存储在 `/etc/passwd` 文件中。

```bash
$ grep sam /etc/passwd
sam:x:301:501:/home/sam:/bin/bash
```

登录时，shell 继承主目录路径并将其赋值给变量 `HOME`。当你使用无参数 `cd` 时，会将 `HOME` 中的目录变为工作目录：

```bash
$ pwd
/max/laptop
$ echo HOME
/home/max
$ cd
$ pwd
/home/max
```

此示例显示了 `HOME` 变量的值以及 `cd` 命令的作用。当你执行无参数 `cd` 时，目录路径与 `HOME` 的值相同。

shell 使用 `HOME` 的值来展开使用波浪号（~）符号表示用户主目录的路径。下面的示例使用 `echo` 显示该快捷方式，然后使用 `ls` 列出 `laptop` 目录中的文件，它是主目录的子目录：

```bash
$ echo ~/
/home/max
$ ls ~laptop
tester count      lineup
```

# PATH：shell 查找程序的位置

当你提供绝对路径或相对路径而非简单文件名作为命令时，它会在指定的目录中查找可执行文件。如果指定路径的文件不存在，shell 会报告未找到命令。如果指定路径的文件存在，但你没有执行权限，或者对于 shell 脚本你没有读取和执行权限，shell 会报告拒绝访问。

当你提供简单文件名作为命令时，shell 会在某些目录（你的搜索路径）中搜索想要执行的程序。`PATH` shell 变量控制这种搜索。

# 320 第 9 章 鲍恩 Shell

`PATH` 的默认值是在 `bash` 编译时确定的。它没有在启动文件中设置，尽管可以被修改。通常，默认值指定了 shell 搜索用于存放常用命令的几个系统目录。这些系统目录包括 `/bin` 和 `/usr/bin` 以及其他适用于本地系统的目录。当你输入一个命令时，如果 shell 在 `PATH` 列出的任何目录中都未找到以命令命名的可执行读文件，shell 将生成上述错误消息之一。

工作目录：`PATH` 变量指定了 shell 搜索目录的顺序。每个目录之间必须用冒号分隔。以下命令设置了 `PATH`，使得对可执行文件的搜索从 `/usr/local/bin` 目录开始。如果在该目录中未找到文件，shell 将在查找 `/bin`，然后是 `/usr/bin`。如果在这些目录中搜索失败，shell 将查找 `~/bin` 目录，它是用户家目录的子目录。导出 `PATH` 可以使其值被子 shell 使用：

```bash
$ export PATH=$usr/local/bin:/bin:/usr/bin:~
```

字符串中的空值表示工作目录。在前面的示例中，空值（冒号和行尾之间的内容）作为字符串的最后一个元素出现。工作目录可以用开头的冒号（不建议；见下文的安全提示）、结尾的冒号（如示例所示）或字符串任意位置的两个冒号来表示。你也可以用点（`.`）显式表示工作目录。

由于 Linux 在名为 `bin`（二进制）的目录中有许多可执行文件，用户通常将自己的可执行文件放在 `~/bin` 目录中。如果你将自己的 `bin` 目录放在 `PATH` 的末尾（如前面的示例），shell 将在 `PATH` 之前的目录中查找找不到的命令。

# PATH 与安全

安全：当考虑安全时，不要将工作目录放在 `PATH` 的第一位。如果你以 `root` 身份工作，绝不应该将工作目录放在 `PATH` 的开头。`root` 的 `PATH` 完全省略工作目录是常见现象。你可以通过在名称前加冒号来执行工作目录中的文件：`/myprog`。

将工作目录放在 `PATH` 的开头可能会导致安全隐患。大多数人在进入目录时输入的第一个命令是 `ls`。如果所有者在该目录中放置了一个名为 `ls` 的可执行文件，并且工作目录出现在用户的 `PATH` 中，那么用户在该目录下执行 `ls` 命令时，执行的是工作目录中的 `ls` 而不是系统的 `ls` 工具，这可能导致不可想要的结果。

如果你想向 `PATH` 添加目录，可以在设置 `PATH` 的新值时引用 `PATH` 变量的旧值（但请前述的安全提示）。以下命令将 `/usr/local/bin` 添加到用户家目录中当前 `PATH` `bin` 目录（`~/bin`）的开头到结尾：

```bash
$ PATH=/usr/local/bin:$PATH:~/bin
```

# MAIL：你的邮件保存在哪里

`MAIL` 变量包含存储邮件的文件路径（邮箱箱，通常为 `/var/mail/name`，其中 `name` 是你的用户名）。如果设置了 `MAIL` 且未设置 `MAILPATH`（下文），则当邮件到达 `MAIL` 指定的文件时，shell 会通知你。在图形化环境中，你可以取消 `MAIL`，以便 shell 不会在终端模拟器窗口中显示邮件提醒（假设你正在使用图形化程序）。

`MAILPATH` 变量包含用冒号分隔的文件名列表。如果设置了此变量，当任何一个文件被修改时（例如当邮件到达时），shell 会通知你。你可以在列表中的任何文件名后加上问号（`?`），后跟一条消息。该消息将替换你在登录期间看到的消息。

`MAILCHECK` 变量指定了 shell 检查新邮件的频率（以秒为单位）。如果你将此变量设置为零，shell 将在每次提示符出现前检查。

# PS1：用户提示符（主）

默认的 Bourne Again Shell 提示符是美元符号（`$`）。当你以 `root` 权限运行 `bash` 时，`bash` 通常会显示井号（`#`）提示符。`PS1` 变量持有 shell 用于告知它正在等待命令的字符串。当你更改 `PS1` 的值时，你就更改了提示符的外观。

你可以自定义由 `PS1` 显示的提示符。例如，赋值语句：

```bash
$ PS1="\u@\h \W \$ "
```

显示如下提示符：

```
[user@host directory event]$
```

其中 `user` 是用户名，`host` 是第一个点之前的主机名，`directory` 是工作目录的基名，`event` 是当前命令的事件次数（第 331 页）。

如果你在多个系统上工作，将系统名称整合到提示符中可能会很有帮助。例如，你可以将提示符改为正在使用的系统名称，后面跟一个冒号并在结尾加一个空格，使得你在提示符后输入的命令更易读。此命令在分配给 `PS1` 的字符串使用了命令替换（第 362 页）：

```bash
$ PS1="$(hostname): "
bravo.example.com: echo test
test
bravo.example.com:
```

接下来的第一个示例将提示符更改为本地主机名、空格以及美元符号（如果用户以 `root` 权限运行，则是井号）。第二个示例将提示符更改为时间后跟用户名。第三个示例将提示符更改为书中使用的提示符（`root` 为井号，用户为美元）：

```bash
$ PS1='\h \$ '
bravo $
```

```bash
$ PS1='\h \$ '
bravo $
```

```bash
$ PS1='\u@ '
09:
```

```bash
$ PS1=' '
$
```

表 9-4 描述了可以在 `PS1` 中使用的某些符号。

| 符号 | 显示内容 |
| :--- | :--- |
| `\$` | 如果用户以 `root` 权限运行，否则为 `#` |
| `\w` | 工作目录的路径 |
| `\W` | 工作目录的基名 |
| `\!` | 事件次数（第 335 页） |
| `\d` | 星期几日期格式 |
| `\h` | 不带域的主机名 |
| `\H` | 带域的完整主机名 |
| `\u` | 当前用户的用户名 |
| `\@` | 12 小时制 AM/PM 格式 |
| `\T` | 12 小时制 HH:MM:SS 格式 |
| `\A` | 24 小时制 HH:MM:SS 格式 |
| `\t` | 24 小时制 |

# PS2：用户提示符（次级）

`PS2` 变量持有次级提示符。在示例的第一行中，`echo` 后面一个未关闭的字符串。shell 假设命令尚未完成，并在第二行给出默认的次级提示符（`>`）。此提示符表示 shell 正在等待用户继续命令行。shell 直到接收到关闭字符串的引号时才会执行命令：

```bash
$ echo "demonstration of prompt string\n> 2"
demonstration of prompt string
2
$ PS2="secondary prompt: "
$ echo "this demonstrates\nprompt string 2"
this demonstrates
prompt string 2
```

第二个命令将次级提示符更改为 `secondary prompt:` 以及空格。多行 `echo` 展示了新的提示符。

# PS3：菜单提示符

`PS3` 变量持有 `select` 结构的菜单提示符（第 984 页）。

# PS4：调试提示符

`PS4` 变量持有 `bash` 调试符号（第 966 页）。

# IFS：分隔输入字段（单词拆分）

`IFS`（内部字段符）变量指定了用于分隔命令行参数的字符。默认值为空格、制表、换行。无论 `IFS` 的值如何，你都可以使用一个或多个空格或制表符来分隔参数，只要这些字符没有被引号或转义。当你赋值 `IFS` 值时，这些字符也可以分隔字段——前提是它们经历了扩展。这种对命令行的解释方式被称为*单词拆分*。

**小心更改 `IFS`，它有各种副作用，请谨慎操作。你可能会发现在更改 `IFS` 之前保存其值是有帮助的。这样如果你得到意想不到的结果，就可以轻松地恢复原始值。或者，你可以在对 `IFS` 进行实验之前使用 `bash` 命令派生一个新的 shell；如果你遇到麻烦，可以 `exit` 回到旧 shell（前提是 `IFS` 工作正常）。

以下示例演示了 `IFS` 如何影响对命令行的解释：
