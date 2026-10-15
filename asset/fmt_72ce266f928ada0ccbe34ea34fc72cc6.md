
| `sort` | 摘要：`sort [-options] [field-specifiers] [file-list]`  
排序或合并文件。 | b, c, d, f, m, n, r, t, u | 217 |

| `source` | 摘要：`source` 命令  
在当前 shell 中执行命令。 | | 777 |

| `stop` | 摘要：`stop [job_number]`  
停止（挂起）后台作业。 | | 167 |

| `stty` | 摘要：`stty`  
设置或取消选定的终端输入/输出选项。 | a, g | 25 |

| `switch` | 摘要：`switch (expression)`  
在备选项之间进行选择。 | | 732 |

| `tail` | 摘要：`tail [-options] [file]`  
显示文件末尾的行（默认为 10 行）。 | -N, +N, b, c, l, r | 208 |

| `talk` | 摘要：`talk user-id [terminal]`  
用于在登录到同一或不同系统的两个用户之间创建聊天环境。 | | 257 |

| `tee` | 摘要：`tee [-option] file-list`  
将标准输入复制到标准输出，同时复制到一个或多个文件。 | a | 153 |

# 834 • 附录 F · UNIX 命令

| 命令 | 描述 | 选项 | 页码 |

| --- | --- | --- | --- |

| `telnet` | 摘要：`telnet`  
将用户连接到由参数（域名名）定义的远程计算机。 | | 276 |

| `test` | 摘要：`test 参数`  
评估关系、逻辑或文件表达式。 | | 561 |

| `tr` | 摘要：`tr [-options] [string1] [string2]`  
将一组字符（string1）翻译（替换）为另一组（string2）。 | c, d, s | 230 |

| `trap` | 摘要：`trap "action" signals`  
在接收信号时执行命令。 | | 638 |

| `tty` | 摘要：`tty`  
显示终端名称。 | | 24 |

| `typeset` | 摘要：`typeset -attribute variable`  
`typeset +attribute variable`  
将数据属性（如数字和对齐）与变量关联（-）或取消关联（+）。 | | 512 |

| `umask` | 摘要：`umask [mask]`  
显示或设置新创建的文件或目录的默认权限。 | a | 133 |

| `unalias` | 摘要：`unalias alias-list`  
删除某些或所有别名。 | (Korn and Bash) | 173 |

| `uname` | 摘要：`uname`  
显示系统数据。 | a, n, r, s, sr | 28 |

| `uniq` | 摘要：`unique [-options] [input_file]`  
显示文件中唯一的行。 | u, c, d | 233 |

| `unset` | 摘要：`unset 变量`  
`unset选项`  
取消变量的值或取消一个选项。 | #C shell | 182 |

| `unsetenv` | 摘要：`unsetenv 变量`  
在 C shell 中，取消环境变量的值。 | | 182 |

| `until` | 摘要：`until 命令`  
`do`  
`body`  
`done`  
在命令成功（退出状态为 0）为止重复执行 body。 | | 573 |

| `vi` | 摘要：`vi [-options] [file-name]`  
用于创建新文件或编辑现有文件。 | R | 42, 292 |

| 命令 | 描述 | 选项 | 页码 |

| --- | --- | --- | --- |

| `wc` | *摘要:`wc [-options] [file-list]`*  
显示文件的行数、单词和字符数。 | c, l, w | 237 |

| `while` | *摘要:`while (expression)` body end*  
在表达式成功（退出状态为 0）时重复执行 body。 | | 571, 736 |

| `who` | *摘要:`who [-options] [am i]`*  
显示当前登录到系统的所有用户。 | H, u | 18 |

| `whoami` | *摘要:`whoami`*  
显示用户的 ID。 | | 20 |

| `write` | *摘要:`write user-id [terminal]`*  
用于向登录到同一或不同系统的接收者发送消息。 | | 260 |

# 特殊字符

shell 使用的特殊字符。

| 字符 | 含义 |

| --- | --- |

| `*` | 通配符 |

| `$` | 变量引用 |

| `<` | 重定向 |

| `>` | 重定向 |

| `!` | 历史记录 |

| `&` | 后台执行 |

| `;` | 命令分隔符 |

| 空格 | 命令分隔符 |

| `\` | 转义字符 |

| `'` | 单引号 |

| `"` | 双引号 |

| `~` | 目录 |

# Korn 和 C shell

Korn shell 和 C shell 之间的差异。

# 变量

shell 中使用的变量。

| 特性 | Korn | C |

| --- | --- | --- |

| 存储（设置） | `variable=value` |

| 引用 | `$(variable)` | `$variable` |

| 取消 | `unset variable` |

| 只读 | `readonly variable` |

| 导出 | `export variable` |

| 属性（设置） | `typeset -attribute variable` | `typeset +attribute` |

# 命令编辑

命令行编辑的摘要。

| 特性 | Korn | C |

| --- | --- | --- |

| 设置 | `set -o` | |

| 取消 | `set +o` | |

# 命令替换

命令替换的摘要。

# 别名

别名的摘要。

| 特性 | Korn | C |

| --- | --- | --- |

| 定义 | `alias name=command` | `alias` |

| 参数 | | |

| 列出单个 | `alias name` | `alias` |

| 列出全部 | `alias -a` | `unalias` |

| 删除单个 | `unalias name` | `unalias` |

# 输入/输出

输入/输出命令的摘要。

| 特性 | Korn | C |

| --- | --- | --- |

| 输入 | `read [-ru]` | |

| 输出 | `print [-n]` | |

# 环境变量

环境变量的摘要。

| 特性 | Korn | C |

| --- | --- | --- |

| 列表 | 查看第 13 章第 575 页 | 查看第 16 章第 840 页 |

| 设置 | `setenv variable` | `set variable` |

| 取消 | `unsetenv variable` | `unset variable` |

| 显示单个 | `print $variable` | `echo $variable` |

| 显示全部 | `set -o` | `set` |

# 启动文件

启动文件的摘要。

| 特性 | Korn | C |

| --- | --- | --- |

| 系统（shell） | `/etc/profile` | `/etc/csh.login` |

| 系统（环境变量） | | `/etc/cshrc` |

| 用户（shell） | `$HOME/.profile` | `$HOME/.login` |

| 用户（环境变量） | | `$HOME/.cshrc` |

# 退出文件

退出文件的摘要。

| 特性 | Korn | C |

| --- | --- | --- |

| 系统 | `/etc/ch.logout` |

| 用户 | | `$HOME/.logout` |

# 选项和开关变量

选项和开关变量的摘要。注意在 C shell 中，开关变量作为选项使用。

| 特性 | Korn | C (开关变量) |

| --- | --- | --- |

| 列表 | 查看第 13 章第 583 页 | 查看第 16 章第 839 页 |

| 设置 | `set -o option` | `set variable` |

| 取消 | `set +o option` | `unset variable` |

| 显示单个 | | `echo $variable` |

| 显示全部 | `set -o` | `set` |

# 参数

参数的摘要。

| 特性 | Korn | C |

| --- | --- | --- |

| 位置 | `$1, $2, ..., $9` | `$argv[1], $argv[2], ..., $argv[9]` |

| 特殊 | `$0, $$, $*, -$0` | `$0, $argv#, $argv` |

# H.12 特殊变量

特殊变量汇总于表 H.12。

表 H.12 特殊变量
