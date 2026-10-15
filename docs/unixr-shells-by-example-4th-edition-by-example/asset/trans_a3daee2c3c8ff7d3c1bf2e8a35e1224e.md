

### 表9.25 tcsh内建命令及其含义（续）

| 命令 | 含义 |
|---|---|
| which command | 显示 shell 在执行替换、路径搜索等操作后将要执行的命令。该内建命令与 which(1) 类似，但它能正确报告 tcsh 别名和内建命令，并且速度快 10 到 100 倍。 |
| while (expr) | 参见第566页的“循环控制命令”。 |

## 9.20.1 特殊的 C/TC Shell 内建变量

内建 shell 变量对 shell 具有特殊含义，用于修改和控制许多 shell 命令的行为方式。它们是局部变量，因此如果要传递给子 C/TC shell 并对其产生影响，其中大多数变量会在 TC shell 的 .tcshrc 文件和 C shell 的 .cshrc 文件中设置。

当 shell 启动时，它会自动设置以下变量：addsuffix、argv、autologout、command、echo_style、edit、gid、group、home、logname、oid、path、prompt、prompt2、prompt3、shell、shlvl、tcsh、term、tty、uid、user 和 version。除非用户决定更改这些变量，否则它们将保持不变。shell 还会跟踪并更改可能需要周期性更新的特殊变量，例如 cwd、dirstack、owd 和 status，并在用户注销时设置 logout 变量。

某些局部变量具有同名的对应环境变量。如果环境变量或局部变量受到用户环境变化的影响，shell 将同步局部变量和环境变量*，以使它们的值始终匹配。交叉匹配变量的示例包括 afsuser、group、home、path、shlvl、term 和 user。（尽管 cwd 和 PWD 含义相同，但它们不进行交叉匹配。即使 path 和 PATH 变量的语法不同，只要其中一个发生变化，它们也会自动交叉匹配。）

### 表9.26 特殊的 C/TC Shell 变量 a b

| 变量 | 含义 |
|---|---|
| addsuffix (+) | 用于文件名补全：当匹配时，在目录末尾添加斜杠，在普通文件末尾添加空格。默认设置。 |
| afsuser (+) | 如果设置了该变量，autologout 的 autolock 功能将使用其值而不是本地用户名进行 Kerberos 认证。 |
| ampm (+) | 如果设置，所有时间都以12小时制 AM/PM 格式显示。 |
| argv | shell 的命令行参数数组；也可表示为 $1、$2 等。 |
| autocorrect (+) | 在每次尝试文件名、命令或变量补全之前调用拼写检查器。 |
| autoexpand (+) | 如果设置，在每次补全尝试之前会自动调用 expand-history 编辑器命令。 |
| autolist (+) | 如果设置，在歧义补全后列出可能的选项。如果设置为 ambiguous，则仅当补全未添加新字符时才列出可能的选项。 |
| autologout (+) | 其参数为自动注销前无活动的分钟数；第二个可选参数为自动锁定导致屏幕锁定前的分钟数。 |
| backslash_quote (+) | 如果设置了该变量，反斜杠将始终用于引用自身、单引号或双引号。 |
| cdpath | 目录列表，当子目录在当前目录中找不到时，cd 应在此列表中搜索子目录。 |
| color (+) | 为内建命令 ls -f 启用彩色显示，并将 --color=auto 传递给 ls。 |
| complete (+) | 如果设置为 enhance，补全将忽略大小写，将句点、连字符和下划线视为单词分隔符，并将连字符和下划线视为等价。 |
| correct (+) | 如果设置为 cmd，命令将自动进行拼写纠正。如果设置为 complete，命令将自动补全。如果设置为 all，则纠正整个命令行。 |
| cwd | 当前工作目录的完整路径名。 |
| dextract (+) | 如果设置，pushd +n 从目录栈中提取第 n 个目录，而不是将其轮转到栈顶。 |
| dirsfile (+) | dirs -S 和 dirs -L 查找历史文件的默认位置。如果未设置，则使用 ~/.cshdirs。 |
| dirstack (+) | 目录栈上所有目录的列表。 |
| dunique (+) | 不允许 pushd 在栈上保留重复的目录项。 |
| echo | 如果设置，每条命令及其参数在执行前都会被回显。由 -x 命令行选项设置。 |
| echo-style (+) | 设置 echo 的风格。如果设置为 bsd，当第一个参数为 -n 时不会回显换行符；如果设置为 sysv，则识别反斜杠转义序列；如果设置为 both，则同时识别 -n 标志和反斜杠转义序列；在默认设置下以及设置为 none 时，两者都不识别。 |
| edit (+) | 为交互式 shell 设置命令行编辑器；默认设置。 |

> 9. 除非该变量是只读变量，否则这是成立的；如果是只读变量，则不会进行同步。

