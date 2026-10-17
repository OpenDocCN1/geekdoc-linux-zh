
## 第9章 管理 Linux 进程

| PID | USER | NI | VIRT | RES | SHR | S | %CPU | %MEM | TIME | COMMAND |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 0 | root | 20 | 0 | 123636 | 1644 | 1180 | R | 0.7 | 0.1 | 0:00:05 | top |
| 1 | root | 20 | 0 | 51544 | 7348 | 2476 | S | 0.0 | 0.4 | 0:00:98 | systemd |
| 2 | root | 20 | 0 | 0 | 0 | S | 0.0 | 0.0 | 0:00:00 | kthread |
| 3 | root | 20 | 0 | 0 | 0 | S | 0.0 | 0.0 | 0:00:01 | kthreadqd/0 |
| 5 | root | -20 | 0 | 0 | 0 | S | 0.0 | 0.0 | 0:00:00 | kerworker/u12+ |
| 6 | root | 20 | 0 | 0 | 0 | S | 0.0 | 0.0 | 0:00:02 | kerworker |
| 7 | root | rt | 0 | 0 | 0 | S | 0.0 | 0.0 | 0:00:00 | migration/0 |
| 8 | root | 20 | 0 | 0 | 0 | S | 0.0 | 0.0 | 0:00:00 | rc_bh |
| 9 | root | 20 | 0 | 0 | 0 | S | 0.0 | 0.0 | 0:00:34 | rc_sue |
| 10 | root | rt | 0 | 0 | 0 | S | 0.0 | 0.0 | 0:00:00 | watchdog/0 |
| 11 | root | -20 | 0 | 0 | 0 | S | 0.0 | 0.0 | 0:00:00 | khelper |
| 12 | root | 20 | 0 | 0 | 0 | S | 0.0 | 0.0 | 0:00:00 | kdevtmpfs |
| 13 | root | -20 | 0 | 0 | 0 | S | 0.0 | 0.0 | 0:00:00 | netns |
| 14 | root | -20 | 0 | 0 | 0 | S | 0.0 | 0.0 | 0:00:00 | writeback |
| 15 | root | -20 | 0 | 0 | 0 | S | 0.0 | 0.0 | 0:00:00 | kthreadd |
| 16 | root | -20 | 0 | 0 | 0 | S | 0.0 | 0.0 | 0:00:00 | ioset |

注意，`top` 命令显示了许多与 `ps` 命令相同的列，但它在屏幕顶部包含一个摘要段，并在摘要段和进程列表之间有一个光标。从之前的输出中你可以看到 `gnome-shell` 使用了最多的处理器时间，其次是 `top` 自身（top）以及守护进程（systemd）。

你可能会遇到一个在执行过程中遇到错误并持续占用系统资源的进程。这些进程被称为“流氓进程”（rogue processes），并出现在 `top` 生成的列表顶部。`top` 命令还可以用于更改进程的优先级或杀死它们。因此，你可以在识别出进程后立即通过 `top` 命令停止这些进程。优先级和杀死进程将在本章稍后部分讨论。

要获取 `top` 工具中可以使用不同命令的完整列表，请按 `h` 获取帮助屏幕。接下来的示例：

```
Help for Interactive Commands procs-ng version 3.3.12

Window 1: Cumulative mode Off. System: Delay 3.0 secs; Secure Mode Off.
```

```
Z,B,E   Global: 'Z' colors; 'B' bold; 'E/e' summary/task memory scale

1,t,m   Toggle: '1' load avg; 't' task/cpu stats; 'm' memory info

0,1,2,3I Toggle: '0' zeros; '/2/3' cpus or numa nodes views; 'I' Irix mode

f,FX    Fields: 'f/f' add/remove/order/sort; 'X' increase fixed-width
```

```
L,&,>   Locate: 'L/'&' find/again; Move sort column: '</' left/right

R,H,V,J Toggle: 'R' Sort; 'H' Threads; 'F' Forest view; 'J' Num justify

c,i,S,j Toggle: 'c' Cmd name/line; 'i' Id; 'S' Time; 'j' Str justify

X,Y     Highlights: 'x' sort field; 'y' running tasks
```

![](img/255973d66f1869a98dbc624ab00_495_0.png)

z,b . Toggle: 'z' color/mono; 'b' bold/reverse (only if 'x' or 'y')

k,r Manipulate tasks: 'k' kill; 'r' renice or s Set interval
W,Y Write configuration file 'W'; Inspect other output 'Y'
q Quit commands shown with ' require visible task display window)
Press 'h' or '?' for help,
Type 'q' or <Esc> to continue

### Killing Processes

```
[root@server1 ~]#1) SIGHUP 2) SIGINT 3) SIGQUIT 4) SIGILL

5) SIGTRAP 6) SIGABRT 7) SIGBUS 8) SIGFPE

9) SIGKILL 10) SIGUSR 11) SIGSEGV 12) SIGUSR2

13) SIGPIPE 14) SIGRM 15) SIGTERM 16) SIGCHLD

17) SIGCONT 18) SIGSTOP 19) SIGTSTP 20) SIGINFO

21) SIGTOU 22) SIGURG 23) SIGCPU 24) SIGFSZ

25) SIGALRM 26) SIGPROF 27) SIGWINCH 28) SIGIO

29) SIGVTIO 30) SIGPWR 31) SIGSYS 32) SIGRTMIN+3

34) SIGRTMIN+1 35) SIGRTMIN+2 36) SIGRTMIN+3 37) SIGRTMIN+4 38) SIGRTMIN+5

39) SIGRTMIN+6 40) SIGRTMIN+7 41) SIGRTMIN+8 42) SIGRTMIN+9

43) SIGRTMIN+10 44) SIGRTMIN+11 45) SIGRTMIN+12 46) SIGRTMIN+13

47) SIGRTMIN+14 48) SIGRTMIN+15 49) SIGRTMAX-15 50) SIGRTMAX-14

51) SIGRTMAX-13 52) SIGRTMAX-12 53) SIGRTMAX-11 54) SIGRTMAX-10

55) SIGRTMAX-9 56) SIGRTMAX-8 57) SIGRTMAX-7 58) SIGRTMAX-6

59) SIGRTMAX-5 60) SIGRTMAX-4 61) SIGRTMAX-3 62) SIGRTMAX-2

63) SIGRTMAX-1 64) SIGRTMAX

[root@server1 ~]#
```
