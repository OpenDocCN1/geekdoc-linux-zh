

由于信号处理程序除了信号编号之外不能有任何参数，或者在较新的 `sa_sigaction()` 风格处理程序的情况下内核传递给它的结构，因此它们与程序其余部分共享数据的唯一方式是通过全局变量。例如，如果 SIGALRM 信号处理程序必须更新屏幕上对象的位置，那么处理程序需要对存储对象当前位置的变量具有读写访问权限。该变量必须是处理程序内的静态变量，或程序中的全局变量。如果变量需要在处理程序之外被程序的其他部分访问，则它必须是全局变量。在任何一种情况下，变量都不能驻留在运行时栈上，因为如果它在那里，它会在处理程序的每次调用之间被销毁。如果变量的内容在处理程序的每次调用之间被销毁，就无法对对象进行动画处理。

通常，使用必须访问全局数据或非栈上数据的信号处理程序是危险的。如果在我们的视频程序中正确处理，风险很小，但如果将同样的策略用于一般程序，可能导致不可靠且不安全的程序。它会打开潘多拉魔盒，带来与处理程序本身可能出现竞态条件相关的一系列问题。这是因为在处理程序处于活动状态时可能会有另一个信号到来，从而导致处理程序被重新进入。例如，如果处理程序使用 `SA_NODEFER` 标志注册，那么它可能在执行中间被中断，并且处理程序使用的变量因此可能处于不一致的状态。更糟的是，在某些情况下，入侵者可能会找到方法向程序发送适当的信号序列，迫使其核心转储，并利用这些转储获得 root 访问权限（参见 Zalewski [3]）。

第二个问题涉及某些系统调用和库函数。某些系统调用和库函数被标记为安全，其余的则不安全。如果信号处理程序调用库函数或系统调用，并且在处理程序处于该调用期间时，另一个信号导致其被重新进入（因为信号未被屏蔽或阻塞），则信号处理程序的第二次调用也可能进入同一个函数。如果是这样，则该函数也会被同一进程重新进入。如果该函数不安全，则处理程序的数据状态将被破坏，其执行不再可预测。例如，在以下处理程序中

```
void sighandler(int signum)
{
    ...
    printf("Running with uid=%d euid=%d\n", getuid(), geteuid());
    ...
}
```

如果在第一次调用处于 `printf()` 函数时第二个信号到来，则两次调用都将使用 `printf()` 代码，而 `printf()` 不是可重入的，因此不安全。这意味着 `printf()` 的输出可能被破坏。更糟糕的情况也可能发生，使系统容易受到攻击。POSIX.1-2004 要求以下函数可以在信号处理程序中安全调用：

```
_Exit(), _exit(), abort(), accept(), access(), aio_error(), aio_return(),
aio_suspend(), alarm(), bind(), cfgetispeed(), cfgetospeed(), cfsetispeed(),
cfsetospeed(), chdir(), chmod(), chown(), clock_gettime(), close(), connect(),
creat(), dup(), dup2(), execle(), execve(), fchmod(), fchown(), fcntl(),
fdatasync(), fork(), fpathconf(), fstat(), fsync(), ftruncate(), getegid(),
geteuid(), getgid(), getgroups(), getpeername(), getpgrp(), getpid(),
getppid(), getsockname(), getsockopt(), getuid(), kill(), link(), listen(), lseek(), lstat(), mkdir(), mkfifo(), open(), pathconf(), pause(), pipe(), poll(), posix_trace_event(), pselect(), raise(), read(), readlink(), recv(), recvfrom(), recvmsg(), rename(), rmdir(), select(), sem_post(), send(), sendmsg(), sendto(), setgid(), setpgid(), setsid(), setsockopt(), setuid(), shutdown(), sigaction(), sigaddset(), sigdelset(), sigemptyset(), sigfillset(), sigismember(), signal(), sigpause(), sigpending(), sigprocmask(), sigqueue(), sigset(), sigsuspend(), sleep(), socket(), socketpair(), stat(), symlink(), sync(), tcdrain(), tcflow(), tcflush(), tcgetattr(), tcgetpgrp(), tcsendbreak(), tcsetattr(), tcsetpgrp(), time(), timer_getoverrun(), timer_gettime(), timer_settime(), times(), umask(), uname(), unlink(), utime(), wait(), waitpid(), write().
```

POSIX.1-2008 从前述列表中删除了 fpathconf()、pathconf() 和 sysconf()，并向其中添加了以下函数：

```
execl(), execv(), faccessat(), fchmodat(), fchownat(), fexecve(), fstatat(), futimens(), linkat(), mkdirat(), mkfifoat(), mknod(), mknodat(), openat(), readlinkat(), renameat(), symlinkat(), unlinkat(), utimensat(), utimes()
```

通常，除了 read() 和 write() 之外的 I/O 函数都不安全，不能在信号处理程序中调用。

不可重入函数是指不能安全地被调用、中断，然后在第一次调用完成前再次调用而不导致内存损坏的函数。一种简单地思考函数是否可重入的方法是，该函数使用的每个变量都存储在运行时栈上，包括任何返回值。它不使用静态变量也不使用全局变量。每次调用时，新调用都有自己的一组变量。

如果信号处理程序包含对不安全函数的调用，则它必须完全消除被中断的可能性。这是不现实的。如果一个不安全函数在执行中间时信号到来，而该信号的处理程序也调用了一个不安全函数，那么执行的結果就变得未定义，意味着关于会发生什么一切皆有可能。这也是避免在处理程序中使用不安全函数的更令人信服的理由。

根据 Wheeler[2] 的建议，在设计信号处理程序时，尽可能遵循以下三条通用规则：

- 1. 在可能的情况下，让你的信号处理程序无条件地设置一个特定的标志，并且不做其他任何事情。
- 2. 如果你必须有更复杂的信号处理程序，仅使用专门指定为可在信号处理程序中使用的安全调用。特别是，不要在 C 中使用 malloc() 或 free()（在大多数系统上它们不受信号保护），也不要使用依赖于它们的许多函数（如 printf() 系列和 syslog()）。你可以尝试用对全局标志的检查来“包装”对不安全库调用的调用（以避免重新进入），但我不推荐这样做。
- 3. 在程序中的所有非原子操作期间阻塞信号传递，并在信号处理程序内部阻塞信号传递。

