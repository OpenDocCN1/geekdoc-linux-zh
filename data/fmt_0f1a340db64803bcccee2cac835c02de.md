
| `PATH` | shell 查找命令的目录的冒号分隔列表 |
| `PS1` | 主要 shell 命令行界面的提示字符串 |
| `PS2` | 次要 shell 命令行界面的提示字符串 |

除了默认的 Bourne 环境变量外，Bash shell 还提供了几个它自己的变量，如表 6.2 所示。

#### 表 6.2 Bash Shell 环境变量

| 变量 | 描述 |
| :--- | :--- |
| `BASH` | 执行当前 Bash shell 实例的完整路径名 |
| `BASH_ALIASES` | 当前设置的别名的关联数组 |
| `BASH_ARGC` | 包含传递给子例程或 shell 脚本的参数数量的变量数组 |
| `BASH_ARGV` | 包含传递给子例程或 shell 脚本的参数的变量数组 |
| `BASH_ARGV0` | 包含 shell 名称，或如果在脚本中使用，则包含 shell 脚本名称的变量 |
| `BASH_CMDS` | 包含 shell 已执行的命令位置的关联数组 |
| `BASH_COMMAND` | 当前正在执行或即将执行的 shell 命令 |
| `BASH_COMPAT` | 指定 shell 兼容性级别的值 |
| `BASH_ENV` | 当设置时，每个 Bash 脚本在运行前都会尝试执行由此变量定义的启动文件 |
| `BASH_EXECUTION_STRING` | 使用 `bash` 命令 `-c` 选项传递的命令 |
| `BASH_LINENO` | 包含当前执行 shell 函数的源代码行号的变量数组 |
| `BASH_LOADABLE_PATH` | shell 查找可动态加载内置命令的目录的冒号分隔列表 |
| `BASH_REMATCH` | 包含使用正则表达式比较运算符 `=~` 进行正向匹配的匹配模式及其子模式的只读变量数组 |
| `BASH_SOURCE` | 包含当前执行 shell 函数的源代码文件名的变量数组 |
| `BASH_SUBSHELL` | 当前 `subshell` 环境的嵌套级别（初始值为 0） |
| `BASH_VERSINFO` | 包含当前 Bash shell 实例的独立主版本号和次版本号的变量数组 |
| `BASH_VERSION` | 当前 Bash shell 实例的版本号 |
| `BASH_XTRACEFD` | 如果设置为有效的文件描述符（0, 1, 2），则可以通过重定向将 `set -x` 调试选项生成的跟踪输出重定向；这通常用于将跟踪输出分离到文件中 |
| `BASHOPTS` | 当前启用的 Bash shell 选项列表 |
| `BASHPID` | 当前 Bash 进程的处理程序 ID |
| `CHILD_MAX` | 控制 shell 跟踪的已退出子进程状态值数量的设置 |
| 变量 | 描述 |
| :--- | :--- |
| `COLUMNS` | 包含用于当前 Bash shell 实例的终端的终端宽度 |
| `COMP_CWORD` | 进入包含当前光标位置的变量 `COMP_WORDS` 的索引 |
| `COMP_LINE` | 当前命令行 |
| `COMP_POINT` | 当前光标位置相对于当前命令开头的索引 |
| `COMP_KEY` | 用于调用当前 shell 函数补全的最后一个按键 |
| `COMP_TYPE` | 表示导致调用补全 shell 函数所尝试的补全类型的整数值 |
| `COMP_WORDBREAKS` | 用于执行单词补全的 Readline 库单词分隔字符 |
| `COMP_WORDS` | 包含当前命令行上各个单词的数组变量 |
| `COMPREPLY` | 包含 shell 函数生成的可能补全代码的数组变量 |
| `COPROC` | 持有未命名协程的 I/O 文件描述符的数组变量 |
| `DIRSTACK` | 包含目录堆栈当前内容的数组变量 |
| `EMACS` | 指示 emacs shell 缓冲区正在执行并且行编辑已禁用，当设置为 `t` 时 |
| `EPOCHREALTIME` | 包含自 UNIX 纪元（1970 年 1 月 1 日 00:00:00 UTC）以来的秒数，包括微秒 |
| `EPOCHSECONDS` | 包含自 UNIX 纪元（1970 年 1 月 1 日 00:00:00 UTC）以来的秒数，不包括微秒 |
| `ENV` | 当设置时，在 Bash shell 脚本运行之前执行定义的启动文件（仅当 Bash shell 在 POSIX 模式下被调用时使用） |
| `EUID` | 当前用户的数字有效用户 ID |
| `EXECIGNORE` | 在搜索中使用 `PATH` 时，确定要忽略的可执行文件（如共享库文件）的过滤器的冒号分隔列表 |
| `FCEdit` | `fc` 命令使用的默认编辑器 |
| `FIGNORE` | 执行文件名补全时要忽略的后缀的冒号分隔列表 |
| `FUNCNAME` | 当前执行 shell 函数的名称 |
| `FUNNEST` | 设置允许的最大函数嵌套级别；当设置为大于 0 的数时（如果超过，当前命令中止） |
| `GLOBIGNORE` | 定义文件名扩展要忽略的文件名模式的集合的冒号分隔列表 |
| `GROUPS` | 包含当前用户所属组列表的变量数组 |
| `histchars` | 最多三个控制历史扩展的字符 |
| `HISTCMD` | 当前命令的历史编号 |
| `HISTCONTROL` | 控制哪些命令输入到 shell 历史列表中 |
| `HISTFILE` | 保存 shell 历史列表的文件名（默认为 `.bash_history`） |
| `HISTFILESIZE` | 在历史文件中保存的最大行数 |
| `HISTIGNORE` | 用于确定哪些命令在历史文件中被忽略的模式的冒号分隔列表 |
| `HISTSIZE` | 历史列表中存储的最大命令数 |
| `HISTTIMEFORMAT` | 如果设置且不为空，则用作格式化字符串以在 Bash 历史中打印每个命令的时间戳 |
| `HOSTFILE` | 包含 shell 需要补全主机名时应读取的文件名 |
| `HOSTNAME` | 当前主机的名称 |
| `HOSTTYPE` | 描述 Bash shell 正在运行的机器的字符串 |
| `IGNOREEOF` | shell 在退出之前必须接收的连续 EOF 字符数（如果此值不存在，默认为 1） |
| `INPUTRC` | Readline 初始化文件的名称（默认为 `.inputrc`） |
| `INSIDE_EMACS` | 仅在进程在 Emacs 编辑器 shell 缓冲区中运行时设置，可以禁用行编辑（禁用行编辑还取决于 `TERM` 变量的值） |
| `LANG` | shell 的语言环境类别 |
| `LC_ALL` | 覆盖 `LANG` 变量，定义语言环境类别 |
| `LC_COLLATE` | 设置对字符串值排序时使用的排序顺序 |
| `LC_CTYPE` | 确定用于文件名扩展和模式匹配的字符解释 |
| `LC_MESSAGES` | 确定解释以美元符号开头的双引号字符串时使用的语言环境设置 |
| `LC_NUMERIC` | 确定格式化数字时使用的语言环境设置 |

# 第 6 章：使用 Linux 环境变量

| 变量 | 描述 |
| :--- | :--- |
| `LC_TIME` | 确定格式化日期和时间时使用的区域设置 |
| `LINENO` | 当前正在执行的脚本中的行号 |
| `LINES` | 定义终端上可用的行数 |
| `MACHTYPE` | 定义系统类型（cpu-厂商-系统格式）的字符串 |
| `MAILCHECK` | Shell 检查新邮件的频率（以秒为单位，默认值为 60） |
| `MAILFILE` | 当未指定数组变量名时，存储从 `mailfile` 命令读取文本的数组变量 |
| `OLDPWD` | Shell 中之前使用的工作目录 |
| `OPTERR` | 如果设置为 1，Bash shell 将显示由 `getopts` 命令生成的错误 |
| `OSTYPE` | 定义 Shell 所运行的操作系统的字符串 |
| `PIPESTATUS` | 包含前馈管道中进程退出状态值列表的变量数组 |
| `POSIXLY_CORRECT` | 如果设置，Bash 将以 POSIX 模式启动。 |
| `PPID` | Bash shell 父进程的流程 ID（PID） |
| `PROMPT_COMMAND` | 如果设置，这是在显示主要提示符之前要执行的命令 |
| `PROMPT_DIRTRIM` | 一个整数，用于指示使用 `\` 和 `\W` 提示符转义时显示的尾部目录名称数量（被移除的目录名称将替换为一组省略号） |
| `PS0` | 如果设置，交互式 Shell 在命令输入后但执行前显示其内容 |
| `PS3` | 用于 `select` 命令的提示符 |
| `PS4` | 如果使用 Bash `-x` 参数，在命令行被回显之前显示的提示符 |
| `PWD` | 当前工作目录 |
| `RANDOM` | 返回 0 到 32767 之间的随机数（为此变量赋值会设置伪随机数生成器的种子） |
