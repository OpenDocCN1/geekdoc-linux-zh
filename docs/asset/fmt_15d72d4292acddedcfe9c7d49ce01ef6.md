
```
# /usr/proc/bin/psig 29081
29081: /bin/ksh
HUP caught RESTART
INT caught RESTART
QUIT caught RESTART
ILL caught RESTART
TRAP caught RESTART
ABRT caught RESTART
EMT caught RESTART
FPE caught RESTART
BUS default
SYS caught RESTART
PIPE caught RESTART
ALRM caught RESTART
TERM ignored

USR1     caught RESTART
USR2 caught RESTART
CLD default NOCLDSTOP
PWR default
WINCH default
URG default
POLL default
STOP default
TSTP ignored
CONT default
TTIN default
TTOU
VTALRM default
PROF default
XCPU caught RESTART
KFZ2 ignored
WAITING default
LWP default
FREEZE default
THAW default
CANCEL default
LOST default
RTMIN default
RTMIN+1 default
RTMIN+2 default
RTMIN+3 default
```

还可以使用 `pstack` 命令为每个进程的 `LWP` 打印十六进制堆栈。这在 `truss` 命令中非常有用：

```
# /usr/proc/bin/pstack 29081
29081: /bin/ksh
df05347 waitid (7, 0, 804114, 7) + 63
df0b9d9 waitid (ffffffff, 847224, 4) + 1f
df0b6f1 waitid (ffffffff, 847224, 0)
0805792 waitid (130) = 1ae
0806a4e sh_exec (8072270, 14) + af0
0805e3al ???
0805decd main (1, 847624, 6c) + 705
0804fa78 ???
```
最常用的 `proc` 是 `pfiles` 命令，它显示每个进程打开的文件。对于确定文件和应用程序之间的依赖非常有用：

```
# /usr/proc/bin/pfiles 29081
29081: /bin/ksh
Current rlimit: 64
0: S_IFCHR mode=0620 dev=102,0 ino=31900 uid=6049 gid=7 rdev=24,8 O_DRWR|O_LARGEFILE
1: S_IFCHR mode=0620 dev=102,0 ino=31900 uid=6049 gid=7 rdev=24,8 O_DRWR|O_LARGEFILE
2: S_IFCHR mode=0620 dev=102,0 ino=31900 uid=6049 gid=7 rdev=24,8 O_DRWR|O_LARGEFILE
63: S_IFREG mode=0620 dev=174,2 ino=99089 gid=6049 size=32210 O_RDWR|O_APPEND|O_LARGEFILE FD_CLEXEC
```

此外，可以使用 `pwd` 命令获取目标进程的当前工作目录：

```
# /usr/proc/bin/pwd 29081
/home
```

如果你需要检查包含 `PID` 的所有父进程和子进程的进程树，可以使用 `ptree` 命令实现这对于确定通过查看进程列表无法显而易见的进程之间的依赖关系非常有用：

```
# /usr/proc/bin/ptree 29081
247 /usr/bin/dtlogin -daemon
28950 /usr/bin/dtlogin -daemon
28972 /ksh/usr/bin/dtssession
29012 /usr/bin/sbin_shell -c unset; DISPLAY=:0;
29015 ksh - unset; DISPLAY=:0;
/usr/bin/dt
29026 /usr/bin/dtssession
29032 dterm
29079 /usr/bin/ksh
29085 /usr/local/bin/bash
29230 /usr/bin/ptree
```

在这里，`ptree` 是从 Bourne shell (`bash`) 执行的，该 shell 由 Korn shell (`ksh`) 启动，由 `dterm` 终端派生，再由 `dwin` 管理器派生，以此此类推。

![](img/0ce985fd07a527ed793d64cf4b977d_457_0.png)

> 提示 尽管这些 `proc` 工具可能很晦涩，但在调试与进程相关的应用程序错误时非常有用，特别是在数据库管理系统等大型应用程序中。

## 虚拟内存

`swap` 命令用于向系统添加虚拟 `RAM`。虚拟 `RAM` 通常用于在物理内存耗尽时为进程执行提供内存。磁盘块使用一种用户不可见的接口来模拟物理内存位置。用户无需担心其进程所访问的 `RAM` 类型。虽然虚拟内存允许用户的有效容量是其物理容量的许多倍，但它的速度比物理 `RAM` 得多。当系统遇到内存峰值需求，导致虚拟内存被使用时，这会对性能有显著影响。当虚拟内存被大量使用时，所谓的“磁盘抖动”`disk thrashing` 可能会发生。

> 提示 `disk thrashing` 是一种常见现象，虚拟内存应该对系统进行调优。因此，对于 `256MB` 的系统，虚拟内存应该被初始化为 `512MB`。为了添加虚拟内存，应该使用 `mkfile` 命令创建所需大小的文件。

# Sun 认证 Solaris 9.0 系统和网络管理员合一考试指南

为了确保此分区在启动期间被作为交换分区 `swap` 添加，需要在 `/etc/vfstab` 文件中输入以下条目：

```bash
#device      device mount FS fsck mount mount
#to mount    to fs point type pass atboot ops
/dev/dsk/clt11d2s1 swap no no
```

要从交换池中移除一个文件 `或` 设备，必须在命令行上传递 `-d` 选项。然后，如果使用 `/u1/swap` 和 `/dev/dsk/clt11d2s1` 作为交换池，将使用以下命令：

```bash
# -d /u1/swap
# -d /dev/dsk/clt11d2s1
```

现在可以安全地删除 `/u1/swap` 文件，并且只要 `/etc/vfstab` 存在，就可以始终选择 `/dev/dsk/clt11d2s1` 用于其他分区。

## 总结

在本章中，我们学习了如何确保分区在启动时作为交换分区添加 `通过编辑 /etc/vfstab 文件`。此外，还学习了如何从交换池中移除文件或设备 `使用 -d 选项`。

## 练习

1. 系统的挂载点是？

A. `/process`

B. `/dev`

C. `/proc`

D. `/etc`

2. `PR_ISSYS` 标志是？

A. 系统进程标志

B. `vfork` 子父标志

C. 继承分区标志

D. 运行

3. `PR_VFORKP` 标志是？

A. 系统进程标志

B. `vfork` 子父标志

C. 继承分区标志

D. 运行

4. `PR_FORK` 标志的意思是？

A. 系统进程标志

B. `vfork` 子父标志

C. 继承分区标志

D. 运行

5. `PR_RLC` 标志是？

A. 系统进程标志

B. `vfork` 子父标志

C. 继承分区标志

D. 运行

6. `PR_KLC` 标志是？

A. 系统进程标志

B. `vfork` 子父标志

C. 继承分区标志

D. 运行

7. `PR_ASYNC` 标志的意思是？

A. 系统进程标志

B. `vfork` 子父标志

C. 继承分区标志

D. 运行

8. `PR_MSACCT` 标志的意思是？

A. 系统进程标志

B. `vfork` 子父标志

C. 继承分区标志

D. 运行

9. `FORK` 标志是？

A. 系统进程标志

B. `vfork` 子父标志

C. 继承分区标志

D.

10. `-a` 命令的目的是？

A. 添加交换空间

B. 总结交换使用情况

C. 列出交换使用情况

D. 删除交换空间

11. `-s` 命令的目的是？

A. 添加交换空间

B. 总结交换使用情况

C. 列出交换使用情况

D. 删除交换空间

12. `-l` 命令的目的是？

A. 添加交换空间

B. 总结交换使用情况

C. 列出交换使用情况

D. 删除交换空间

13. `-d` 命令的目的是？

A. 添加交换空间

B. 总结交换使用情况

C. 列出交换使用情况

D. 删除交换空间

14. 文件和分区都可以用于交换吗？

A. 是

B. 否

C. 取决于系统

D. 不确定
