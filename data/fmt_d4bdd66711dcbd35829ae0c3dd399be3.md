
# 其他选项（有很多）

- 使用 `-C` 选项通过管道获取信息可能更方便
- `-o` 选项的排序字段在管理部分“标准格式”（这些是）可用
- 使用格式 `-o pid,user=USERNAME,cpu=pmem,comm` 重命名列
- 当列出用户名时，如果长度大于 8 个字符将显示 UID 而不是用户名。
- 像通常使用管道到 `head` 或 `tail` 来考虑列表宽度。
- 使用 `ps` 查询的常用属性：`pid`,`comm`（所有参数），`uname`（用户名），`pmem`（物理内存占比），`pcpu`（CPU 使用率），`nice`（nice 值），`etime`（经过时间），`state`（单字母代码），`stat`（多个进程状态）。

```
[root@localhost] ps aux
USER PID %CPU %MEM VSZ RSS STAT TIME COMMAND
root 1 0.0 0.0 2072 588 S 00:00 init
root 2 0.0 0.0 3534 513 S 00:00 migration
root 3 0.0 0.0 2438 339 S+ 00:00 getty
root 4 0.0 0.0 2448 500 S+ 00:00 dbus-daemon
root 5 0.0 0.0 2511 221 S+ 00:00 audit
root 6 0.0 0.0 2525 445 S+ 00:00 gnome-session
root 7 0.0 0.0 2561 312 S+ 00:00 ssh
```

`"F"` 选项可以像上面一样显示进程：

```
[root@localhost] ps aux
USER PID %CPU %MEM VSZ RSS STAT TIME COMMAND
root 1 0.0 0.0 2072 588 S 00:00 init
root 2 0.0 0.0 3534 513 S 00:00 migration
root 3 0.0 0.0 2438 339 S+ 00:00 getty
root 4 0.0 0.0 2448 500 S+ 00:00 dbus-daemon
root 5 0.0 0.0 2511 221 S+ 00:00 audit
root 6 0.0 0.0 2525 445 S+ 00:00 gnome-session
root 7 0.0 0.0 2561 312 S+ 00:00 ssh
```

`"F"` 选项列出更多信息。`"x"` 选项显示 CPU 和内存的使用情况。

# PS 输出列

`VSZ`=虚拟内存大小，`RSS`=驻内存大小，`STAT`=`(S=睡眠, R=运行, F 代表派生进程数）`，`PPID` 父进程，`CHAN` 是名称

## 状态

+ - 空闲（睡眠）
- `R` - 运行（在运行队列中）
- `S` - 睡眠（等待事件完成）
- `T` - 停止（通过作业控制或跟踪）
- `D` - 不可中断睡眠（通常为 IO）
- `Z` - 标记死亡（僵尸）
- `W` - 分页无效
- `X` - 死亡（不应看到）

## 附加状态码

+ - 处于前台终端
< - 具有 CPU 调度优先级
`N` - 具有 CPU 调度优先级 (`priority(2)`)
> - 已超过内存需求的软限制并正在超过
`A` - 已请求分页
`E` - 进程尝试退出
`I` - 多线程（使用 NPTL 线程）
`L` - 页面锁定在内存中（例如）
`s` - 会话首领

## 示例

显示 5 个 CPU 进程。显示进程的运行时间。实时查看进程输出 PID、命令和 nice 值按 `%cpu` 排序按 mem (KB) 使用量排序。以树样式显示进程层次结构

```
ps aux --sort=pcpu | head -5
ps -e pid,comm,etime
watch -n 1 'ps -o pid,comm,pcpu --sort=mem | head -15'
ps -o pid,comm,cputime -g 594
ps -o rss,args | sed -b -k1,in | pr -TW
ps -f --forest -C apache2
```

显示父进程的列

```
[root@localhost] ps -o pid,uname,comm
PID USER COMMAND
2359 root apache2
4524 www-data apache2
2525 www-data apache2
```

第一个所有 root 的进程是主 apache2 进程，所有其他 apache2 进程都从这里派生。我们现在查询它：

`$ ps --pid 2359`

```
PID TTY TIME CMD
4524 ? 00:00:00 apache2
2525 ? 00:00:00 apache2
```

`pstree` 输出进程树，这可能比 `ps --forest` 更受青睐：

```
[root@localhost ~#] pstree
init-acpid
  ate
  auditd--audispd{auditd}
    └(auditd)
    └automount-[*]
```

## TOP

结合了 `ps`、`uptime`、`free` 并定期更新；默认按 CPU 使用率对任务排序 `kill(k)`, `renice(r)`。

The header:

`top - 00:00:01 up 1 day, 1:23, 1 user, load average: 0.00, 0.01, 0.05`

`Tasks: 116 total, 1 running, 115 sleeping, 0 zombie`

`%Cpu(s0.3us, 0.0sy, 99.7id, 0.0wa, 0.0hi, 0.0si`

`Memory: 103810 total, 101436 used, 20772 free, 137732 buffers`

`Swap: 2097144 total, 0k used, 2097144 free, 64638 cached`

  PID PR NI  USER    %CPU  MEM    VSZ S   TIME COMMAND

     1  25  0 root      0.0   0.6   2072   588 S   00:00 init

     2  -5  0 root      0.0   0.1   3534   513 S   00:00 migration

     3  14  0 root      0.0   0.2   2438   339 S+  00:00 getty

     4  20  0 root      0.0   0.5   2448   500 S+  00:00 dbus-daemon

     5  20  0 root      0.0   0.2   2511   221 S+  00:00 audit

     6  20  0 root      0.0   0.4   2525   445 S+  00:00 gnome-session

     7  20  0 root      0.0   0.3   2561   312 S+  00:00 ssh
