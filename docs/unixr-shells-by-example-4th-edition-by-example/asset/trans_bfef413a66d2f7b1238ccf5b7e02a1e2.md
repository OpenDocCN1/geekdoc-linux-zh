

## 表 10.11 C Shell 和 TC Shell 内建命令及其含义（续）

| 命令 | 含义 |
|---|---|
| nice [+n|-n] [command] | 将 shell 或命令的进程优先级值增加 n。优先级值越高，进程的优先级越低，运行越慢。如果省略 command，nice 会增加当前 shell 的值。如果未指定增量，nice 将 nice 值设为 4。nice 值的范围为 -20 至 19。n 值超出此范围时，将分别设为下限或上限。+n 将进程优先级值增加 n。-n 将其减少 n。仅超级用户可以使用此参数。 |
| nohup [command] | 运行 command 并忽略 HUP 信号（挂断）。无参数时，在脚本剩余部分忽略 HUP 信号。 |
| notify [%]job | 当当前或指定作业的状态发生变化时，异步通知用户。 |
| onintr [- | label] | 控制 shell 对中断的处理。无参数时，onintr 恢复 shell 对中断的默认行为。 （shell 会终止 shell 脚本并返回到终端命令输入层。）使用减号参数时，shell 忽略所有中断。使用 label 参数时，收到中断或子进程因被中断而终止时，shell 执行 goto label。 |
| popd [+n] | 弹出目录栈并 cd 到新的栈顶目录。目录栈的元素从零开始编号，从栈顶开始。+n 丢弃栈中第 n 个条目。 |
| pushd [+n | dir] | 将目录压入目录栈。无参数时，交换前两个元素。+n 将第 n 个条目旋转到栈顶并 cd 到该目录。dir 将当前工作目录压入栈并切换到 dir。 |
| rehash | 重新计算 path 变量所列目录内容的内部哈希表，以反映新增命令。 |
| repeat count command | 重复执行 command count 次。 |
| set [var [= value]] | 参见第 440 页的“变量”。 |
| setenv [VAR [word]] | 参见第 440 页的“变量”。最常用的环境变量 USER、TERM 和 PATH 会自动导入到并从 csh 变量 user、term 和 path 中导出；对这些变量无需使用 setenv。此外，每当后者发生变化时，shell 都会从 csh 变量 cwd 设置 PATH 环境变量。 |
| shift [variable] | 将 argv 的各分量，或如果提供则为 variable 的各分量向左移动，丢弃第一个分量。variable 未设置或为空值时为错误。 |
| source [-h] name | 从 name 读取命令。source 命令可以嵌套，但嵌套过深时 shell 可能耗尽文件描述符。任何层级的 sourced 文件中的错误都会终止所有嵌套的 source 命令。常用于重新执行 .login 或 .cshrc 文件，以确保变量设置在当前 shell 中处理，即确保 shell 不会创建（fork）子 shell。-h 将文件名中的命令放入历史记录列表但不执行它们。 |
| stop [%job] ... | 停止当前或指定的后台作业 |
| suspend | 停止 shell 的运行，就像它收到了 ^Z 停止信号一样。这最常用于停止由 su 启动的 shell。 |
| switch (string) | 参见第 557 页的“switch 命令”。 |
| time [command] | 无参数时，打印此 shell 及其子进程使用的时间汇总。有可选 command 时，执行 command 并打印其使用的时间汇总。 |
| umask [value] | 显示文件创建掩码。有 value 时，设置文件创建掩码。value 以八进制给出，与文件权限 666 和目录权限 777 进行 XOR 运算，以得出新文件的权限。umask 不能添加权限。 |
| unalias pattern | 丢弃与（文件名替换）pattern 匹配的别名。unalias * 会删除所有别名。 |
| unhash | 禁用内部哈希表。 |
| unlimit [-h] [resource] | 移除 resource 的限制。若未指定 resource，则移除所有资源限制。参见 limit 命令的说明以获取资源名称列表。-h 移除相应的硬限制。仅超级用户可以执行此操作。 |
| unset pattern | 删除名称与（文件名替换）pattern 匹配的变量。unset * 会删除所有变量；这会有明显不愉快的副作用。 |
| unsetenv variable | 从环境中删除变量。不执行如 unset 那样的模式匹配。 |
| wait | 在提示前等待后台作业完成（或等待中断）。 |
| while (expr) | 参见第 564 页的“while 循环”。 |

