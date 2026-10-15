

``` 
34860 172 128 348 25548 3940 pause 1 Ss 0:00.28 -csh
(csh)
35024 16 128 32 16592 2304 - 1 R+ 0:00.00 ps -O
dsiz,ssiz,tsiz,vsz
29019 172 128 348 25548 3976 ttyin 4 Is+ 0:00.31 -csh (csh)
% ps -o dsiz,ssiz,tsiz,lwp,nlwp,wchan,pcpu,pmem,flags,args
DSIZ SSIZ TSIZ LWP NLWP WCHAN %CPU %MEM F COMMAND
172 128 348 100733 NLWP 1 pause 0.0 0.1 10004002 -csh (csh)
16 128 32 100622 1 - 0.0 0.1 10004002 ps -o
dsiz,ssiz,tsiz,lwp,nl
172 128 348 100690 1 ttyin 0.0 0.1 10004002 -csh (csh)
% ps -o user,pid=SON -o ppid=MOM -o args
USER SON MOM COMMAND
sarwar 34860 34857 -csh (csh)
sarwar 35281 34860 ps -o user,pid=SON -o ppid=MOM -o args
sarwar 29019 29016 -csh (csh)
%
```

其中的一些字段和对应的关键字很明显，我们在本章前面已经讨论过其中一些。然而，我们现在要讨论的一些关键字是新的且不明显的。你可以通过使用 ps -L 命令来显示所有关键字，如下所示：

``` 
% ps -L
%cpu %mem acflag acflg args blocked caught class comm command cow
cpu cputime dsiz egid egroup emul etime etimes euid f fib flags
gid group ignored inblk inblock jid jobc ktrace label lim
lockname login logname lstart lwp majflt minflt msgsrcv msgsnd
mwchan ni nice nivcsw nlwp nsigals nsigs nswap nvcs w nvcsw oublk
 oublk paddr pagein pcpu pending pgid pid pmem ppid pri re rigid
rgroup rss rtpr io ruid ruser sid sig sigcatch sigignore sigmask sl
ssiz start stat state svgid svuid systime taddr tdev tdnam time
tpgid tsid tsiz tt tty ucomm uid upr uprocp user usertime usrpri
vsize vsz wchan xstat
%
```

表 10.3 显示了一些常用的关键字及其含义。请注意，这些字段在 ps 命令输出的头部以大写形式显示（例如，command 对应 COMMAND，pid 对应 PID）。

### 表 10.3 ps 命令常用显示字段/关键字的简要说明

| Field | Description | Field | Description |
|---|---|---|---|
| command | Command executed to create process | ppid | Parent's process ID |
| dsiz | Data size in kilobytes | pri | Scheduling priority |
| cpu | Short-term CPU usage for scheduling | rss | Real process size (kilobytes) in memory |
| flags | Flags indicating process states/events | sid | Session ID; PID of the session leader |
| lwp | Lightweight process (thread) ID | ssiz | Stack size in kilobytes |
| majflt | Total page faults (same as PAGEIN) | started | Time the process was started |
| mwchan | Event or lock of the locked/blocked process | stat | Process state |
| nlwp | Number of threads tied to an LWP | time | Time the process has executed for |
| pcpu | CPU utilization up to one previous minute | tsiz | Text (code) size in kilobytes |
| pgid | Process group ID | tt | Terminal the process is attached to |
| pid | Process ID | vsz | Virtual size of the process in kilobytes |
| pmem | Percentage of memory used by process | wchan | Event (or address) on which a process waits |

![](img/02e070097d401d3bf7de4bf1c470b267_389_0.png)

图 10.6 UNIX 进程的内存映像。

数据、栈和文本/代码段是进程内存映像的一部分。UNIX 进程内存映像的另外三个部分是：共享库、堆和环境。图 10.6 显示了 UNIX 进程的内存映像。环境由命令行参数和五个 shell 变量（HOME、PATH、SHELL、USER 和 LOGNAME）组成，可通过指向两个空终止字符串指针数组的指针访问。栈从高内存向低内存增长，而堆从低内存向高内存增长。文本和已初始化数据部分由 exec(2) 系统调用从程序文件中读取，而未初始化数据（bss）段由 exec(2) 初始化为零。

你也可以使用 size 命令来显示可执行程序的文本/代码、已初始化数据和未初始化数据（bss）的大小（以字节为单位）。以下是该命令在 PC-BSD 和 Solaris 上分别以 /usr/bin/sort 为参数的示例运行。在这两种情况下，第四个数是文本和数据段的总大小（即前三个数字之和）以十进制表示。对于 PC-BSD 版本，第五个数是总大小的十六进制表示。

``` 
% size /usr/bin/sort
    text    data    bss dec     hex filename
   52748    2656    468860092  eabc/usr/bin/sort
%
$ size /usr/bin/sort
69657 + 1584 + 44012 = 115253
$
```

下面的语法框简要描述了 Solaris 版本的 ps 命令。

### 语法

``` 
ps [options]
```

常用的显示选项/功能：

- -G 显示具有给定组 ID（GIDs）的进程信息，GIDs 以逗号分隔的列表给出；逗号前后无空格
- -L 显示每个进程中的 LWP（即线程）数量
- -P 显示 LWP 绑定（即在上面执行的）处理器的编号（PSR）
- -c 根据内核和用户组中的优先级显示进程信息；sched 进程始终列在顶部
- -d 显示所有进程，除会话领导者（用户进程的登录 shell 和内核进程的 sched 进程）
- -e 与 -A 选项相同：显示所有进程的信息，包括会话领导者
- -f 显示完整列表，包括进程所有者 ID（UID）、进程 ID（PID）、父进程 ID（PPID）、C（已废弃）、进程启动时间（STIME）、TTY、执行时间（TIME）、完整命令行（CMD）
- -l 显示长列表：状态（S）、UID、PID、PPID、C（已废弃）、PRI、NI、ADDR、SZ、WCHAN、TTY、TIME、CMD
- -t 显示与终端关联的进程列表；例如，console、pts/4、term/a 等
- -u 或 -U 显示属于 UID 或 lognames 列表中的进程，UID 或 lognames 以逗号分隔的列表给出

