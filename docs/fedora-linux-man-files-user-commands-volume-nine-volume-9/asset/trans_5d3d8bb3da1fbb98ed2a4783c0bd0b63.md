

## 线程显示

- H
  将线程显示为进程。
- -L
  显示线程，可能包含 LWP 和 NLWP 列。
- m
  在进程之后显示线程。
- -m
  在进程之后显示线程。
- -T
  显示线程，可能包含 SPID 列。

## 其他信息

- help*section*
  打印帮助信息。section 参数可以是 *simple、list、output、threads、misc* 或 *all* 中的一个。该参数可以缩短为以下带下划线字母之一：s|l|o|t|m|a。
- info
  打印调试信息。
- L
  列出所有格式说明符。
- V
  打印 procps-ng 版本。
- -V
  打印 procps-ng 版本。
- version
  打印 procps-ng 版本。

## 备注

此 **ps** 通过读取 /proc 中的虚拟文件来工作。此 **ps** 无需设置为 setuid 或拥有任何特权即可运行。请勿赋予此 **ps** 任何特殊权限。

此 **ps** 需要访问 nalist 数据以正确显示 WCHAN。对于 2.6 之前的内核，必须安装 System.map 文件。

当前 CPU 使用率表示为进程整个生命周期内运行所占的百分比。这并不理想，且不符合 **ps** 在其他方面所遵循的标准。CPU 使用率不太可能恰好加起来等于 100%。

SIZE 和 RSS 字段未计入进程的某些部分，包括页表、内核栈、struct thread_info 和 struct task_struct。这通常至少是 20 KiB 的常驻内存。*SIZE* 是进程的虚拟大小（代码+数据+栈）。

标记为 <defunct> 的进程是死进程（所谓的“僵尸”进程），因为它们没有被父进程正确销毁而保留下来。如果父进程退出，这些进程将由 (8) 销毁。

如果用户名长度超过显示列的长度，则改为显示数字用户 ID。

诸如 **ps -aux** 等命令选项并不推荐，因为这是两种不同标准的混淆。根据 POSIX 和 UNIX 标准，上述命令要求显示所有具有 TTY 的进程（通常是指用户正在运行的命令）以及所有由用户 nad 和 “x” 拥有的进程。如果该用户不存在，则 **ps** 会认为你确实想要 “*ps aux*”。

## 进程标志

这些值的总和显示在 “F” 列中，该列由 **flags** 输出说明符提供：

- 1 已 fork 但未 exec
- 4 使用了超级用户权限

## 进程状态代码

以下是 s、stat 和 state 输出说明符（标题为 “STAT” 或 “S”）将显示的不同值，用于描述进程的状态：

- D 不可中断睡眠（通常是 IO）
- R 正在运行或可运行（在运行队列中）
- S 可中断睡眠（等待事件完成）
- T 被作业控制信号停止
- t 在跟踪期间被调试器停止
- W 换页（在 2.6.xx 内核中不再有效）
- X 死亡（绝不应看到）
- Z 失效（“僵尸”）进程，已终止但未被其父进程回收

在 BSD 格式以及使用 stat 关键字时，可能会显示额外的字符：

- < 高优先级（对其他用户不友好）
- N 低优先级（对其他用户友好）
- L 已将页锁定到内存中（用于实时和自定义 IO）
- s 是会话领导者
- 1 是多线程的（使用 CLONE_THREAD，就像 NPTL pthreads 那样）
- + 属于前台进程组

## 过时的排序键

这些键由 BSD **O** 选项使用（当用于排序时）。GNU —`sort` 选项不使用这些键，而是使用下文 STANDARD FORMAT SPECIFIERS 部分中描述的说明符。请注意，排序使用的值是 `ps` 使用的内部值，而不是输出格式字段中使用的“煮熟”值（例如，按 tty 排序是按设备 `nuer` 排序，而不是按显示的终端 `na` 排序）。如果你希望按“煮熟”值排序，请将 `ps` 输出管道传输到 `(1)` 命令。

| 键 | 长键 | 描述 |
|---|---|---|
| c | cmd | 可执行文件的简单 `na` |
| C | pcpu | cpu 利用率 |
| f | flags | 长格式 `F` 字段中的标志 |
| g | pgpr | 进程组 `ID` |
| G | pggid | 控制 `tty` 的进程组 `ID` |
| j | cuti | 累计用户 `ti` |
| J | csti | 累计系统 `ti` |
| k | uti | 用户 `ti` |
| m | min_flt | 次要缺页中断的 `nuer` |
| M | maj_flt | 主要缺页中断的 `nuer` |
| n | cmin_flt | 累计次要缺页中断 |
| N | cmaj_flt | 累计主要缺页中断 |
| o | session | 会话 `ID` |
| p | pid | 进程 `ID` |
| P | ppid | 父进程 `ID` |
| r | rss | 常驻集大小 |
| R | resedent | 常驻页 |
| s | size | `mory` 大小（以千字节为单位） |
| S | share | 共享页的数量 |
| t | tty | 控制 `tty` 的设备 `nuer` |
| T | start_ti | 进程启动时的 `ti` |
| U | uid | 用户 `ID` `nuer` |
| u | user | 用户 `na` |
| v | vsi | 总 VM 大小（以 `KiB` 为单位） |
| y | priority | 内核调度优先级 |

## AIX 格式描述符

此 ps 支持 AIX 格式描述符，它们的工作方式有点像 (1) 和 (3) 的格式化代码。例如，正常的默认输出可以用此命令产生：ps -eo “%p %y %x %c”。**NORMAL** 代码在下一节中描述。

| 代码 | NORMAL | 标题 |
|---|---|---|
| %C | pcpu | %CPU |
| %G | group | GROUP |
| %P | ppid | PPID |
| %U | user | USER |
| %a | args | COMMAND |
| %c | comm | COMMAND |
| %g | rgroup | RGROUP |
| %n | nice | NI |
| %p | pid | PID |
| %r | pgid | PGID |
| %t | eti | ELAPSED |
| %u | ruser | RUSER |
| %x | ti | TIME |
| %y | tty | TTY |
| %z | vsz | VSZ |

## 标准格式说明符

以下是可用于控制输出格式（例如，使用选项 **-o**）或使用 GNU 风格的 —**sort** 选项对选定进程进行排序的不同关键字。
例如：**ps -eo pid;user;args —sort user**
此版本的 **ps** 试图识别 *ps* 的其他实现中使用的绝大多数关键字。

以下用户定义的格式说明符可能包含空格：
**args,cmd,comm,command,fna,ucmd,ucomm, lstart,bsdstart,start.**
因此，关键字可能无法用于排序。

| 代码 | 标题 | 描述 |
|:---|:---|:---|
| %cpu | %CPU | 进程的 cpu 利用率，格式为 "##.#"。目前，它是使用的 CPU 时间除以进程运行时间（cpu/实际时间比率），以百分比表示。除非你运气好，否则它不会加起来等于 100%。（别名 **pcpu**）。 |
| %m | %MEM | 进程的常驻集大小与机器物理内存的比率，以百分比表示。（别名 **pm**）。 |
| args | COMMAND | 包含所有参数的命令字符串。可能会显示参数的修改。此列中的输出可能包含空格。标记为 `<defunct>` 的进程部分已死，等待被其父进程完全销毁。Sotis 之后，进程参数将不可用；当这种情况发生时，**ps** 将改为在方括号中打印可执行文件的 na。（别名 **cmd,command**）。另见 **comm** 格式关键字、**-f** 选项和 **c** 选项。如果最后指定，此列将扩展到显示边缘。如果 **ps** 无法确定显示宽度（例如，当输出被重定向（管道）到文件或另一个命令时），则输出宽度是不确定的（可能是 80，无限，由 **TERM** 变量确定，等等）。**COLUMNS** 环境变量或 —**cols** 选项可用于在此情况下准确确定宽度。**w** 或 **-w** 选项也可用于调整宽度。 |
| blocked | BLOCKED | 被阻止信号的掩码，参见 (7)。根据字段宽度，以十六进制格式显示 32 位或 64 位掩码。（别名 **sig_block,sigmask**）。 |
| bsdstart | START | 命令启动的时间。如果进程是在 24 小时前启动的，输出格式为 "HH:MM"，否则为 " Mmm:SS"（其中 Mmm 是月份的三个字母）。另见 **lstart,start,start_ti** 和 st i。 |
| bsdstart | | 累积的 cpu 时间，用户 + 系统。显示格式通常是 |

