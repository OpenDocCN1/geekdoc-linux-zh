

# sh, jsh

kill [-signal] %jobid

kill 的内置版本，用于为由 %jobid 标识的进程提供 kill 命令的功能。

stop %jobid...

停止后台作业的执行。

suspend

停止当前 shell 的执行（但如果它是登录 shell 则不停止）。

wait [%jobid...]

等待由 %jobid 指定的后台进程并报告其终止状态。如果省略了 %jobid，wait 的行为如第 1274 页的“特殊命令”部分描述的那样。

> 注意 — 由于 shell 在同一个进程组中同时实现了前台和后台作业，它们会接收到相同的信号，这可能导致意料之外的行为。因此，建议你使用其他作业控制类的 shell，特别是在交互式环境中。

# 大文件行为

参阅 largefile(5) 了解 sh 和 jsh 在遇到大于或等于 2 Gbytes (31 字节) 文件时的行为描述。

# 退出状态

shell 检测到的错误（如语法错误）将返回非零退出状态。如果你在非交互模式下使用 shell，则将放弃 shell 文件的执行。否则，shell 将返回最后执行命令的退出状态（另见 exit 命令）。

# jsh 专用

如果你以 jsh 启动 shell 并在存在已停止作业时尝试退出，shell 会发出一个警告。

存在已停止的作业。

> 这是唯一的消息。如果你尝试退出且作业仍处于停止状态，作业将收到来自内核的 SIGHUP 信号，shell 将退出。

# 文件

```
$HOME/.profile
/dev/null
/etc/profile
/tmp/sh*
```

# 属性

参阅 attributes(5) 了解以下属性的描述：

# shell_builtins

/usr/bin/sh /usr/bin/jsp

| 属性类型 | 属性值 |
| --- | --- |
| 可用性 | SUNwcsu |
| CSI | 已启用 XPG4

/usr/xpg4/bin/sh

| 属性类型 | 属性值 |
| --- | --- |
| 可用性 | SUNwxcu4 |
| CSI | 已启用

# 另有

bc(1), echo(1), getoptcvt(1), intro(1), kill(1), ksh(1), login(1), newgrp(1), ps(1), pwd(1), set(1), shell_builtins(1), stty(1), test(1), umask(1), wait(1), rsh(1), su(1), swap(1), sysdef(1M), dup(2), exec(2), fork(2), getlimit(2), pipe(2), ulimit(2), setlocale(3C), signal(3HEAD), passwd(4), profile(4), attributes(5), environ(5), largefile(5), XPG4(5)

# 诊断

如果你收到错误信息 cannot fork, many processes，尝试使用 wait(1) 命令清理你的后台进程。如果这没有帮助，可能是系统进程表已满，或者你有太多活跃的前台进程。你的登录限制了进程 ID 的数量，系统跟踪的数量也有限。

当 shell 执行尝试执行不存在的解释器的 shell 脚本时，shell 会返回一个错误的诊断消息，提示该 shell 文件不存在。

# 警告

出于安全考虑，强烈建议不要使用内置脚本。

# shell_builtins — Shell 命令解释器内置函数

# 描述

sh(1)、csh(1) 和 ksh(1) shell 解释器具有特殊的内置函数，这些函数被 shell 解释为命令。许多内置命令由多个 shell 实现，而某些是特定 shell 特有的。命令列于下表。

| 命令 | Bourne Shell | Korn Shell | C Shell |
| --- | --- | --- | --- |
| alias | | X | X |
| bg | X | X | X |
| break | X | X | X |

| 命令 | Bourne Shell | Korn Shell | C Shell |
| --- | --- | --- | --- |
| case | x | x | x |
| cd | x | x | x |
| chdir | x | | x |
| continue | x | x | x |
| dirs | | | x |
| echo | x | x | x |
| eval | x | x | x |
| exec | x | x | x |
| exit | x | x | x |
| export | x | x | |
| fc | | x | |
| fg | x | x | x |
| for | x | x | |
| foreach | | | x |
| function | | x | |
| getopts | x | x | |
| glob | | | x |
| goto | | | x |
| hash | x | x | |
| hashstat | | | x |
| history | | | x |
| if | x | x | x |
| jobs | x | x | x |
| kill | x | x | x |
| let | | x | |
| limit | | | x |
| login | x | x | x |
| logout | x | x | x |
| nice | | | x |
| newgrp | x | x | |

| 命令 | Bourne Shell | Korn Shell | C Shell |
| --- | --- | --- | --- |
| notify | | | x |
| onintr | | | x |
| popd | | | x |
| print | | | x |
| pushd | | | x |
| pwd | x | x | |
| read | x | x | |
| readonly | x | x | |
| rehash | | | x |
| repeat | | | x |
| select | | | x |
| set | x | x | |
| setenv | | | x |
| shift | x | x | |
| source | x | x | |
| stop | x | x | |
| suspend | x | x | |
| switch | | | x |
| test | x | x | |
| time | x | x | |
| times | x | x | |
| trap | x | x | |
| typeset | x | x |
| u ulimit | | | | |
| unalias | | | x |
| unhash | | | x |
| unlimit | | | x |

| 命令 | Bourne Shell | Korn Shell | C Shell |
| --- | --- | --- | --- |
| unset | X | X | |
| unsetenv | | | | |
| until | X | X |
| wait | X | X |
| whence | | | |
| while | | | | |

# Bourne Shell 特殊命令

输入输出重定向是允许的。这些命令对文件描述符 1 进行执行。

- 退出状态是最后一个执行命令的状态。

# C Shell 特殊命令

输入输出重定向是允许的。这些命令对文件描述符 1 进行执行。

- 如果指定任何参数，它们将成为位置参数。否则，保持参数不变。

# Korn Shell 特殊命令

输入输出重定向是允许的。这些命令对文件描述符 1 进行执行。

- 错误信息：cannot fork, many processes。
- 当不发生语法错误时，其退出状态为 0。
- 变量赋值后执行。
- 只有在非交互模式执行。
- 符号替换后执行。
- 变量赋值规则。
- 波浪号替换执行。
- 解释器不存在。
- 扩展参数。

