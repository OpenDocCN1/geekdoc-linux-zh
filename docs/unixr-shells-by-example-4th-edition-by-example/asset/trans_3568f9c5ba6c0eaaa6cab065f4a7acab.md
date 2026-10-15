

## 表 13.27 shopt 命令选项（续）

| 选项 | 含义 |
|---|---|
| execfail | 非交互式 shell 在无法执行作为 exec 内建命令参数指定的文件时不会退出。交互式 shell 在 exec 失败时也不会退出。 |
| expand_aliases | 别名会被展开。默认启用。 |
| extglob | 扩展的模式匹配功能（用于文件名展开的源自 Korn shell 的正则表达式元字符）已启用。 |
| histappend | 当 shell 退出时，历史记录列表会追加到 HISTFILE 变量指定的文件中，而不是覆盖该文件。 |
| histreedit | 如果正在使用 readline，则用户有机会重新编辑失败的历史替换。 |
| histverify | 如果设置，且正在使用 readline，则历史替换的结果不会立即传递给 shell 解析器。相反，结果行会被加载到 readline 编辑缓冲区中，允许进一步修改。 |
| hostcomplete | 如果设置，且正在使用 readline，bash 会尝试在包含 @ 的单词补全时执行主机名补全。默认启用。 |
| huponexit | 如果设置，bash 在交互式登录 shell 退出时会向所有作业发送 SIGHUP（挂断信号）。 |
| interactive_comments | 允许以 # 开头的词在交互式 shell 中导致该词及该行剩余字符被忽略。默认启用。 |
| lithist | 如果启用，且 cmdhist 选项已启用，多行命令会以嵌入换行符的方式保存到历史记录中，而不是在可能的情况下使用分号分隔。 |
| mailwarn | 如果设置，且 bash 检查邮件的文件自上次检查以来已被访问，则会显示消息 The mail in mailfile has been read。 |
| nocaseglob | 如果设置，bash 在执行文件名展开时以不区分大小写的方式匹配文件名。 |
| nullglob | 如果设置，bash 允许匹配不到任何文件的模式展开为空字符串，而不是自身。 |
| promptvars | 如果设置，提示符字符串在展开后会进行变量和参数扩展。默认启用。 |
| restricted_shell | shell 在受限模式下启动时会设置此选项。值不可更改。在执行启动文件时不会重置此选项，允许启动文件发现 shell 是否受限。 |
| shift_verbose | 如果设置，shift 内建命令在移位计数超过位置参数数量时会打印错误消息。 |
| sourcepath | 如果设置，source 内建命令会使用 PATH 的值来查找作为参数提供的文件所在的目录。默认启用。 |
| source | dot（.）的同义词。 |

## 13.20 Shell 内建命令

shell 有许多命令已内置在其源代码中。由于命令是内置的，shell 不必在磁盘上定位它们，从而使执行速度更快。bash 提供的 help 功能可为任何内置命令提供在线帮助。内置命令列于表 13.28 中。

## 表 13.28 内建命令

| 命令 | 其作用 |
|---|---|
| : | 无操作命令；返回退出状态零。 |
| . | 在当前进程上下文中执行程序；与 source 相同。 |
| . file | dot 命令从 file 中读取并执行命令。 |
| break | 跳出最内层的循环。 |
| break [n] | 参见第 919 页的“break 命令”。 |
| alias | 列出并创建现有命令的“昵称”。 |
| bg | 将作业置于后台。 |
| bind | 显示当前键和函数绑定，或将键绑定到 readline 函数或宏。 |
| builtin [sh-builtin [args]] | 运行 shell 内建命令，将 args 传递给它并返回零退出状态。如果函数和内建命令同名则很有用。 |
| cd [arg] | 如果没有 arg 则更改目录到主目录，或更改到 arg 的值。 |

