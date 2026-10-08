

# 214

# csh

switch

依次将每个 `label` 与指定的 `string` 进行匹配，该 `string` 会首先经过命令和文件名扩展。你可以在 `case label:` 中使用元字符 `*`、`?` 和 `[...]`，这些元字符会进行变量扩展。如果在找到 `default` 标签之前没有 label 匹配，则 `break` 将在默认 `label` 之后开始执行。每个 `case` 语句必须出现在行首。默认命令 `break` 在 `endsw` 之后继续执行。否则，控制流将通过 `C` 经过后续的 case 和 default 语句。如果没有 label 匹配且没有 default，则执行在 `endsw` 之后继续。

(string)

breaksw

default:

breaksw

endsw

time [command]

如果不带参数，则打印此 shell 及其子进程使用的 own摘要。带有一个可选的 `command`，则执行 `command` 并打印时间使用的摘要。

在编写时，`time` 内置命令并不计算输出的最后六字段，错误地报告了这些字段的值。

```
example$ time
```
```
9.0u 11.0s 3:32 10% 0k+0:1o 0Pf+0Ow
```

umask [value]

显示文件创建掩码。带有一个可选的 `value`，则设置文件创建掩码。给定 `value`，你可以关闭任何位，但不能开启位来允许新权限。常见值包括 077，限制所有其他人的权限；022，赋予组完全访问权限，并赋予他人读取（及目录搜索）权限；或 022，赋予组和他人读取（及目录搜索）权限但不赋予写入权限。

unalias pattern

- 丢弃匹配（文件名替换）`pattern` 的别名。unalias*  own移除所有别名。

unhash

禁用 `path` 和 `cdpath` 变量的哈希表。

unlimit [-h]

[resource]

移除对 `resource` 的限制。如果你未指定资源，则移除所有资源限制。请参见 `limit` 命令的描述以获取资源名称列表。只有超级用户可以使用 -h 选项来移除相应的硬限制。

unset pattern

移除名称匹配（文件名替换）`pattern` 的变量。unset 移除所有变量，这具有明显令人不悦的副作用。

unset variable

从环境中移除 `variable`。与 unset 一样，不进行模式匹配。

# csh 215

wait 在提示符出现前等待后台作业完成（或等待中断）。

```
while (expr)
...
end
```

当 expr 为真（求值结果非零）时，重复 while 和匹配语句之间的命令。你可以使用 break 和 continue 提前终止或继续循环。while 和 end 必须单独出现在它们的输入行上。如果 shell 的输入是终端，它将用问号提示命令，直到输入 end 命令为止，并执行循环中的命令。

```
%[job] [&]
@ [var=expr]
@ var[n]=expr
```

将当前或指定的作业带到前台。带上可选的安培符符号（`&`），则继续在后台运行作业。

如果不带参数，显示所有 shell 变量的值。带参数时，将变量 var 设置或 var 值的第 n 个单词设置为 expr 求值的结果（前提是 var 和第 n 个组件必须已经存在）。

如果表达式包含字符 `>`, `<`, `&`, `|`，那么至少该 expr 必须放在括号内。

运算符 `+=` 等像 C 语言中一样可用。名称与赋值运算符之间的空格是可选的。然而，在分离原本会被视为单个单词的 `expr` 组件时，空格是强制性的。

特殊的后缀 `++` 和 `--` 用于递增或递减 expr：

# 环境变量与预定义 shell 变量

与 Bourne shell 不同，C shell 区分了环境变量和 shell 变量。环境变量会自动导出到它所调的进程中。shell 变量则不会。两类变量在变量替换时的处理方式是类似的。shell 在初始化时设置变量 argv, cwd, home, path, prompt 和 status。shell 会将环境变量 USER 复制到 shell 变量中，将 TERM 复制到 HOME 中，并在每当 shell 变量重置时，将每个变量都复制回相应的环境变量中。PATH 和 path 的处理方式类似。你只需要在 .cshrc 或 .login 文件中设置一次 path。每当后者 更改时，环境变量 PWD 就会设置为 cwd。下面显示的 shell 变量具有预定义的含义。

- argv 提供给当前 shell调用的命令行参数列表。此变量决定了位置参数 $1, $2 等的值。

- cwd 如果 cd, cd 和 popd 命令接受的目录参数各不是当前目录的子目录，则这些命令将搜索的目录列表。

- cwd（此处重复）当前目录的完整路径。

# 216

# csh

- echo 在执行前回显（经过替换后）命令。

- fignore 在尝试文件名补全时忽略的文件名后缀列表。通常是单单词 .o.。

- filec 启用文件名补全，在这种情况下，在终端输入行末尾输入 Control-D 字符 EOT 和 ESC 字符具有特殊意义。

- EOT 打印所有以前述字符串开头的文件名。

- ESC 将前述字符串替换为最长无歧扩展名。

- hardpaths 解析目录栈中的路径，使其不包含符号链接组件。注意，符号链接可能会欺骗 shell。hardpaths 对此进行了去哈希。

- history 历史列表的行数。savehist 值大会会减慢 shell 启动。

- home 用户的主目录。此变量用于派生的 shell 解释具有执行位的文件。

- ignore 忽略终端的 EOF。

- mail C shell 检查的文件列表。

- nobeep 在命令补全期间抑制铃声。

- noclobber 限制输出重定向，使现有文件不受破坏。

- noglob 抑制文件名替换。

- nonmatch 如果未匹配模式，则返回文件名替换而非错误。

- notify 在作业完成后立即通知你。

# 246

# csh 217

- path 搜索命令的目录列表。path 从环境变量初始化，shell 每当 path 更改时都会更新它。空单词指定当前目录。

- prompt $prompt 的设置有三个值：

```
$prompt not set
```
非交互式 shell，测试 $prompt。

```
$prompt set but = ""
```
由 which(1) 命令调用的 .cshrc。

```
$prompt set and != ""
```
正常的交互式 shell。

- status 最近一次命令的状态。如果该命令异常终止，则状态加上 200。内置命令失败退出状态 1；所有其他内置命令将状态设置为 0。

- status 控制命令的自动计时。可以提供一个或两个值。第一个是 CPU 秒的报告阈值。第二个是指示要报告哪些资源的标签字符串。一个标签是一个百分号（%）后跟一个大写字母（无法识别的标签将作为文本打印）：

- time

- %D 使用的未共享数据空间的平均量（千字节）。
- %E 命令执行的经过时间（墙钟时间）。
- %F 缺页。
- %I 块输入操作次数。

