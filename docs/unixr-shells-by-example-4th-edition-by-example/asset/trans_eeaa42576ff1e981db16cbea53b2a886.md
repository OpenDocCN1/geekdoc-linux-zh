

# 表 12.15 内置命令及其功能（续）

| Command | Function |
|---|---|
| set (continued) | （要设置选项，使用 -o 标志；要取消设置选项，使用 +o 标志。） |
| set -o ignoreeof | Options: |
| allexport | 设置此选项后，导出了任何已定义或更改的变量。 |
| bgnice | 以较低优先级运行后台作业；代替 nice 使用。 |
| emacs | 设置 emacs 内置编辑器。 |
| errexit | 当命令返回非零退出状态时，shell 退出。 |
| gmacs | 设置内置 gmacs 编辑器。 |
| ignoreeof | 忽略 EOF（Ctrl-D）键使 shell 终止。必须使用 exit 退出。 |
| keyword | 将命令行上任何位置出现的关键字参数添加到 shell 的环境中。 |
| markdirs | 在文件名展开后得到的所有目录名后加上尾部反斜杠。 |
| monitor | 设置作业控制。 |
| noclobber | 防止使用重定向运算符 > 覆盖文件。使用 >! 强制覆盖。 |
| noexec | 与 ksh -n 相同；读取命令但不执行它们。用于检查 shell 脚本中的语法错误。 |
| noglob | 禁用 ksh 通配符元字符的路径名展开。 |
| nolog | 函数定义不会存储在历史文件中。 |
| nounset | 如果变量未设置，则显示错误。 |
| privileged | 为 setuid 程序打开特权模式。 |
| trackall | ksh 使每个命令都成为跟踪别名；对交互式 shell 自动打开。 |
| verbose | 将输入的每一行回显到标准错误；调试时很有用。 |
| vi | 设置 vi 内置编辑器。 |
| viraw | 指定 vi 逐字符输入。 |
| xtrace | 展开每个命令并在 PS4 提示符中显示它，变量已展开。 |
| shift [ n ] | 将位置参数向左移动 n 次。 |
| times | 打印从此 shell 运行的进程的累计用户时间和系统时间。 |
| trap [ arg ] [ n ] | 当 shell 收到信号 n（0、1、2 或 15）时，执行 arg。 |

| Command | Function |
|---|---|
| type [ command ] | 打印命令的类型；例如，pwd 是内置 shell。在 ksh 中，是 whence -v 的别名。 |
| typeset [ options ] [ var ] | 设置 shell 变量和函数的属性和值。 |
| ulimit [ options size ] | 设置进程的最大限制。 |

**EXAMPLES**

ulimit -a 显示所有限制：
Time (seconds) unlimited.
File (blocks) unlimited.
Data (kbytes) 524280.
Stack (kbytes) 8192.
Memory (kbytes) unlimited.
Core dump (blocks) unlimited.

Other Options:
-c size 将核心转储限制为 size 块。
-d size 将数据大小（可执行文件）限制为 size 块。
-f size 将文件大小限制为 size 块（默认值）。
-m size 将物理内存大小限制为 size K 字节。
-s size 将堆栈区域大小限制为 size K 字节。
-t secs 将进程执行时间限制为 secs 秒。

| umask [ mask ] | 无参数时，打印权限的文件创建掩码。 |
| umask [ octal digits ] | 用户文件创建模式掩码，用于所有者、组和其他用户。 |
| unset [ name ] | 取消变量或函数的值。 |
| wait [ pid#n ] | 等待 PID 号为 n 的后台进程并报告终止状态。 |
| whence [ command ] | 打印有关命令的信息，如 ucb wherein。 |

**EXAMPLES**

whence -v happy happy is a function
whence -v addon addon is an undefined function
whence -v ls ls is a tracked alias for /bin/ls
whence ls /bin/ls

## 12.15 Korn Shell 调用参数

当 Korn shell 被调用时，它可以接受选项来控制其行为。参见表 12.16。

# 表 12.16 ksh 的参数

| Command | Function |
|---|---|
| -a | 自动导出所有变量。 |
| -c cmd | 执行一个命令字符串。 |
| -e | 当命令返回非零状态时退出。 |
| -f | 关闭 globbing，即文件名元字符的展开。 |
| -h | 使命令被视为跟踪别名。 |
| -i | 设置交互模式。 |
| -k | 设置关键字选项。所有命令的关键字参数都将成为环境的一部分。 |
| -m | 使在后台执行的命令在单独的进程组中运行，即使尝试 Ctrl-C 或注销也会继续运行。完成后发送作业已终止的消息。 |
| -n | 可用于调试。命令会被扫描，但不执行。可与 -x 和 -v 选项一起使用。 |
| -o | 允许通过 set 命令使用表 12.15 中列出的名称设置选项。 |
| -p | 打开特权模式。用于运行 setuid 程序。 |
| -r | 设置受限模式。 |
| -s | 从 stdin 读取命令，为默认值。 |
| -t | 导致 shell 在执行 shell 输入中发现的第一个命令并且指定了 -c 选项后退出。 |
| -u | 对未设置变量的任何引用都被视为错误。 |
| -v | 在进行任何解析、变量替换或其他处理之前，打印脚本或标准输入的每一行。输出写入标准错误。用于调试。 |
| -x | 在执行脚本或标准输入的每一行之前打印该行。文件名展开、变量替换和命令替换在输出中显示。所有输出都以 PS4 提示符的值为前缀，即加号后跟空格。行写入标准错误。 |

