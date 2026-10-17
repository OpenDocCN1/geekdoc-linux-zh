
| `2>&-` | 关闭标准错误。 |

# C Shell $argv 符号

| 符号 | 描述 |
|---|---|
| `$argv` | 统计命令行参数的数量。 |
| `$*` | 显示所有参数。 |
| `$argv` | 显示所有参数。 |
| `$argv[1-3]` | 显示参数 1 到 3。 |

# 参考表 491

| 符号 | 描述 |
|---|---|
| `$0` | 显示运行 shell 脚本的命令。 |
| `$argv [n]` | 第 n 个参数。 |
| `$argv [S#argv]` |最后一个参数。 |

# 引用

| 字符 | 术语 | 描述 |
|---|---|---|
| `\` | 反斜杠 | 取消后续 shell 元字符的特殊含义，包括另一个反斜杠。 |
| `` ` `` | 反引号 | 将反引号内命令的输出替换为命令本身。更多信息请参阅 shell 手页。 |
| `'` | 单引号 | 取消除感叹号 (!)、反斜杠（\）和单引号本身（'）之外的所有字符的特殊含义。单引号比双引号更严格，不允许变量或反引号扩展。 |
| `"` | 双引号 | 取消除感叹号 (!)、反引号（`）和美元符号（$）之外的所有特殊字符的特殊含义。允许变量和反引号扩展。 |

# 元字符 shell 语法

| 特性 | Bourne 和 Korn | C |
|---|---|---|
| 单字符通配符。 | `?` | `?` |
| 任意数量字符。 | `*` | `*` |
| 字符集中任意一个字符。 | `[abc]` | `[abc]` |
| 字符范围内的任意一个字符。 | `[a-c]` | `[a-c]` |

# 492 参考表与示例脚本

| 特性 | Bourne 和 Korn | C |
|---|---|---|
| 不在指定字符范围内的任意一个字符 | `[!a-c]` | N/A |

# Shell 变量语法

| 特性 | Bourne | Korn | C |
|---|---|---|---|
| 分配普通变量 | `x=1` | `x=1` | `set x = 1` |
| 访问普通变量 | `echo $x` | `echo $x` | `echo $x` |
| 分配数组 | N/A | `y[0]=1; y[1]=2` | `set y=(1 2)` |
| 访问数组元素 | N/A | `echo $y ${y[1]}` | `echo $y[2]` |
| 访问整个数组 | N/A | `echo ${y[*]}` | `echo $y` |
| 导出变量（设为全局） | `export var` | `export var` | `setenv command` |
| 命令行参数 | N/A | N/A | `$argv, $argv, $argv(1)` |
| 位置参数 | `$*, $#, $1` | `$*, $#, $1` | `$*, $1` |
| 设置位置参数 | `set a b c` | `set a b c` | N/A |

# I/O 重定向与管道

| 特性 | Bourne | Korn | C |
|---|---|---|---|
| STDOUT 重定向到文件 | `> filename` or `1> filename` | `> filename` or `1> filename` | `> filename` |
| STDIN 从文件输入 | `< filename` or `0< filename` | `< filename` or `0< filename` | `< filename` |
| STDERR 重定向到文件 | `2> filename` | `2> filename` | N/A |

### 参考表

| 特性 | Bourne | Korn | C |
|---|---|---|---|
| 输出和错误重定向到文件 | `2>&1` | `2>&1` | `>& filename` |
| 输出到下一个命令 | `cmd` | `cmd` | `cmd` |
| 输出和错误重定向到下一个命令 | `2>&1` | `2>&1` | `&` |

# 输出到屏幕

| 特性 | Bourne | Korn | C |
|---|---|---|---|
| 显示文本和变量 | `echo` | `print` or `echo` | `echo` |

# 从键盘读取

| 特性 | Bourne | Korn | C |
|---|---|---|---|
| 读取键盘输入 | `read name2` | `read name2` | `set var = $<` |

# 数学与计算

| 特性 | Bourne | Korn | C |
|---|---|---|---|
| 执行计算 | `var=`expr a + b`` | `let var=a + b` | `@ var = (a + b)` |
| 测试关系条件 | `var=`expr a < b`` | `let var=a < b` | `@ var = (a < b)` |

# 命令替换

| 特性 | Bourne | Korn | C |
|---|---|---|---|
| 命令替换 | `` `command` `` | `$(command)` or `` `command` `` | `` `command` `` |

# 波浪号(~)扩展

| 特性 | Korn | C |
|---|---|---|
| 波浪号代表用户主目录 | `~loginid` | `~loginid` |
| 波浪号代表当前和上一个目录 | `~+ ~-` | N/A |

# 别名语法

| 特性 | Korn | C |
|---|---|---|
| 创建新别名 | `alias name=value` | `alias name value` |
| 显示当前值列表 | `alias` | `alias` |
| 从列表中移除别名 | `unalias name` | `unalias name` |

# 历史记录语法

| 特性 | Korn | C |
|---|---|---|
| 历史记录 | `automatic` | `set history = num` |
| 显示历史列表 | `history` or `fc -1` | `history` |
| 显示部分列表 | `history n m` `history -n` | `history n` |
| 重执行命令 | `r string` `r number` `r` | `!string` `!number` `!!` |

# 函数语法

| 特性 | Bourne 和 Korn | C |
|---|---|---|
| 创建函数 | `func() {commands}` | `function func {commands}` |
| 使用函数 | 将 `func` 作为命令使用 | 将 `func` 作为命令使用 |

# 编程语句语法

| 特性 | Bourne 和 Korn | C |
| --- | --- | --- |
| if 条件判断 | `if command` | `if (cond) then` |
|  | `then commands` `elif command commands` | `else if (cond) commands` |
|  | `else` | `endif` |
|  | `fi` |  |
| switch 和 case 模式 | `case variable in (pattern) commands;; *)` | `switch (variable)` `case pattern:` `commands` `default:` `commands` |
|  | `commands;; esac` | `endsw` |
| while 循环 | `while command do commands done` | `while (cond) commands end` |
| for/foreach 循环 | `for variable in list do commands done` | `foreach variable(list) commands end` |

# 测试与 C Shell 内置测试

| 测试内容 | 测试命令 | C Shell 内置 |
| --- | --- | --- |
| 是否为块设备 | `-b file` | N/A |
| 是否为字符设备 | `-c file` | N/A |
| 是否为目录 | `-d file` | `-d file` |
| 文件或目录是否存在 | `-e file` (Korn shell only) | `-e file` |
| 是否为普通文件 | `-f file` | `-f file` |

# 500 参考表与示例脚本
