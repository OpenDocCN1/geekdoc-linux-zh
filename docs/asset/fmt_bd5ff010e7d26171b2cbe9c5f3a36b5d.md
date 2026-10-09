
# `socket.h`

```c
int shutdown(int sd, int how);
```

- `how`：`SHUT_RD`、`SHUT_WR`、`SHUT_RDWR`
- 返回：成功返回 `0`，错误返回 `1`

---

# `sig2str`

```c
int sig2str(int signo, char *str);
```

- 头文件：`<signal.h>`
- 返回：成功返回 `0`，错误返回 `1`
- 平台：Solaris 9

---

# `sigaction`

```c
int sigaction(int signo, const struct sigaction *restrict act, struct sigaction *restrict oacl);
```

- 头文件：`<signal.h>`
- 返回：成功返回 `0`，错误返回 `1`

---

# `sigaddset`

```c
int sigaddset(sigset_t *set, int signo);
```

- 头文件：`<signal.h>`
- 返回：成功返回 `0`，错误返回 `1`

---

# `sigdelset`

```c
int sigdelset(sigset_t *set, int signo);
```

- 头文件：`<signal.h>`
- 返回：成功返回 `0`，错误返回 `1`

---

# `sigemptyset`

```c
int sigemptyset(sigset_t *sel);
```

- 头文件：`<signal.h>`
- 返回：成功返回 `0`，错误返回 `1`

---

# `sigfillset`

```c
int sigfillset(sigset_t *sel);
```

- 头文件：`<signal.h>`
- 返回：成功返回 `0`，错误返回 `1`

---

# `sigismember`

```c
int sigismember(const sigset_t *set, int signo);
```

- 头文件：`<signal.h>`
- 返回：真返回 `1`，假返回 `0`，错误返回 `1`

---

# `siglongjmp`

```c
void siglongjmp(siglongjmp_buf env);
```

- 头文件：`<setjmp.h>`
- 返回：直接调用时返回 `0`，从 `longjmp` 调用返回时返回 `0`

---

# `signal`

```c
void (*signal(int signo, void (*func)(int)));
```

- 头文件：`<signal.h>`
- 返回：成功返回信号处置，错误返回错误

---

# `sigproc`

```c
int sigproc(sigset_t *set);
```

- 头文件：`<signal.h>`
- 返回：成功返回 `0`，错误返回 `1`

---

# `sigprocmask`

```c
int sigprocmask(int how, const sigset_t *set, sigset_t *old);
```

- 头文件：`<signal.h>`
- `how`：`SIG_BLOCK`、`SIG_UNBLOCK`、`SIG_SETMASK`
- 返回：成功返回 `0`，错误返回非零

---

# `sigsuspend`

```c
int sigsuspend(const sigset_t *mask);
```

- 头文件：`<signal.h>`
- 返回：返回 `1` 且 `errno` 设置 `EINTR`

---

# `sigwait`

```c
int sigwait(const sigset_t *set, int *signop);
```

- 头文件：`<signal.h>`
- 返回：成功返回 `0`，错误返回 `1`

---

# `sigwaitinfo`

```c
int sigwaitinfo(const sigset_t *set, struct siginfo *info);
```

- 头文件：`<signal.h>`
- 返回：成功返回 `0`，错误返回 `1`

---

# `stat`

```c
int stat(const char *restrict pathname, struct stat *restrict buf);
```

- 页码：`p. 87`
- 头文件：`<sys/stat.h>`
- 返回：如果正常返回 `0`，错误返回 `1`

---

# `str2sig`

```c
int str2sig(const char *str, int *signop);
```

- 页码：`p. 353`
- 头文件：`<signal.h>`
- 返回：如果正常返回 `0`，错误返回 `1`
- 平台：Solaris 9

---

# `strerror`

```c
char *strerror(int err);
```

- 页码：`p. 15`
- 头文件：`<string.h>`
- 返回：消息字符串的指针

---

# `strftime`

```c
size_t strftime(char *restrict buf, size_t max, const char *restrict format, const struct tm *restrict tm);
```

- 页码：`p. 176`
- 头文件：`<time.h>`
- 返回：如果空间足够，返回存储在数组中的字符数，否则返回 `0`

---

# `strsignal`

```c
char *strsignal(int signo);
```

- 头文件：`<string.h>`
- 返回：描述信号的字符串指针

---

# `symlink`

```c
int symlink(const char *actualpath, const char *sympath);
```

- 头文件：`<unistd.h>`
- 返回：如果正常返回 `0`，错误返回 `1`

---

# `sync`

```c
void sync(void);
```

- 头文件：`<unistd.h>`

---

# `sysconf`

```c
long sysconf(int name);
```

- 头文件：`<unistd.h>`
- `name`：`_SC_ARG_MAX`、`_SC_ATEXIT_MAX`、`_SC_CHILD_MAX`、`_SC_CLK_TCK`、`_SC_COLL_WEIGHTS_MAX`、`_SC_HOST_MAX`、`_SC_IOV_MAX`、`_SC_JOB_CONTROL`、`_SC_LINE_MAX`、`_SC_LOGIN_NAME_MAX`、`_SC_GROUPS_MAX`、`_SC_OPEN_MAX`、`_SC_PAGESIZE`、`_SC_READER_WRITER_LOCKS`、`_SC_RECUR_MAX`、`_SC_SAVED_IDS`、`_SC_SHELL`、`_SC_STREAM_MAX`、`_SC_SYMLINK_MAX`、`_SC_TTY_NAME_MAX`、`_SC_TZNAME_MAX`、`_SC_VERSION`、`_SC_XOPEN_CRYPT`、`_SC_XOPEN_LEGACY`、`_SC_XOPEN_REALTIME`、`_SC_XOPEN_REALTIME_THREADS`、`_SC_XOPEN_VERSION`
- 返回：如果正常返回对应值，错误返回 `1`

---

# `syslog`

```c
void syslog(int priority, char *format, ...);
```

- 头文件：`<syslog.h>`

---

# `system`

```c
int system(const char *cmdstring);
```

- 头文件：`<stdlib.h>`
- 返回：`shell` 的终止状态

---

# `tcdrain`

```c
int tcdrain(int tfd);
```

- 头文件：`<termios.h>`
- 返回：如果正常返回 `0`，错误返回 `1`

---

# `tcflow`

```c
int tcflow(int tfd, int action);
```

- 头文件：`<termios.h>`
- `action`：`TCOOFF`、`TCOON`、`TCIOFF`、`TCION`
- 返回：如果正常返回 `0`，错误返回 `1`

---

# `tcflush`

```c
int tcflush(int tfd, int queue);
```

- 头文件：`<termios.h>`
- `queue`：`TCIFLUSH`、`TCOFLUSH`、`TCIOFLUSH`
- 返回：如果正常返回 `0`，错误返回 `1`

---

# `tcgetattr`

```c
int tcgetattr(int tfd, struct termios *termios);
```

- 头文件：`<termios.h>`
- 返回：如果正常返回 `0`，错误返回 `1`

---

# `tcgetpgrp`

```c
pid_t tcgetpgrp(int fd);
```

- 页码：`p. 273`
- 头文件：`<unistd.h>`
- 返回：如果正常返回前台进程组的进程组 ID，错误返回 `1`

---

# `tcsgetsid`

```c
pid_t tcsgetsid(int fd);
```

- 页码：`p. 274`
- 头文件：`<termios.h>`
- 返回：如果正常返回会话领导者的进程组 ID，错误返回 `1`

---

# `tcsendbreak`

```c
int tcsendbreak(int fd, int duration);
```

- 页码：`p. 653`
- 头文件：`<termios.h>`
- 返回：如果正常返回 `0`，错误返回 `1`

---

# `tcsetattr`

```c
int tcsetattr(int fd, int opt, const struct termios *termios);
```

- 页码：`p. 643`
- 头文件：`<termios.h>`
- `opt`：`TCSANOW`、`TCSADRAIN`、`TCSAFLUSH`
- 返回：如果正常返回 `0`，错误返回 `1`

---

# `tcsetpgrp`

```c
int tcsetpgrp(int fd, pid_t pgrpid);
```

- 头文件：`<unistd.h>`
- 返回：如果正常返回 `0`，错误返回 `1`

---

# `direldir`

```c
long direldir(DIR *dir);
```

- 头文件：`<dirent.h>`
- 返回：与 `dir` 关联的目录中的当前位置

---

# `tempnam`

```c
char *tempnam(const char *directory, const char *prefix);
```

- 头文件：`<stdio.h>`
- 返回：唯一路径的指针

---

# `time`

```c
time_t time(time_t *calptr);
```

- 头文件：`<time.h>`
- 返回：如果正常返回时间值，错误返回 `1`

---

# `times`

```c
clock_t times(struct time *buf);
```

- 头文件：`<sys/time.h>`
- 返回：如果正常返回时钟周期内的已壁钟时间，错误返回 `1`

---

# `tmpfile`

```c
FILE *tmpfile(void);
```

- 头文件：`<stdio.h>`
- 返回：如果正常返回文件指针，错误返回 `NULL`

---

# `tmpnam`

```c
char *tmpnam(char *name);
```

- 页码：`p. 155`
- 头文件：`<stdio.h>`
- 返回：唯一路径的指针

---

# `truncate`

```c
int truncate(char *pathname, off_t length);
```

- 页码：`p. 105`
- 头文件：`<unistd.h>`
- 返回：如果正常返回 `0`，错误返回 `1`

---

# `ttyname`

```c
char *ttyname(int fd);
```

- 页码：`p. 65`
- 头文件：`<unistd.h>`
- 返回：终端的指针

---

# `umask`

```c
mode_t umask(mode_t mask);
```

- 页码：`p. 97`
- 头文件：`<sys/stat.h>`
- 返回：文件模式

---

# `uname`

```c
int uname(struct uds *name);
```

- 页码：`p. 171`
- 头文件：`<utsname.h>`
- 返回：如果正常返回非负值，错误返回错误

---

# `ungetc`

```c
int ungetc(int c, FILE *fp);
```

- 头文件：`<stdio.h>`
- 返回：如果正常返回 `c`，错误或文件结束前返回 `EOF`

---

# `unlink`

```c
int unlink(const char *pathname);
```

- 头文件：`<unistd.h>`
- 返回：如果正常返回 `0`，错误返回 `1`

---

# `unlock`

```c
int unlock(int fd);
```

- 头文件：`<stdlib.h>`
- 返回：FreeBSD 5.2, Solaris 9

---

# `unsetenv`

```c
void unsetenv(const char *name);
```

- 头文件：`<stdlib.h>`

---

# `utime`

```c
int utime(const char *pathname, struct utimbuf *times);
```

- 头文件：`<utime.h>`
- 返回：如果正常返回 `0`，错误返回 `1`

---

# `vscanf`

```c
int vscanf(FILE *fp, const char *format, va_list arg);
```

- 头文件：`<stdarg.h>`、`<stdio.h>`
- 返回：分配的项目数，输入错误或文件结束返回 `EOF`

---

# `vprintf`

```c
int vprintf(FILE *fp, const char *format, va_list arg);
```

- 头文件：`<stdarg.h>`、`<stdio.h>`
- 返回：如果正常返回字符数，错误返回负值

---

# `vsnprintf`

```c
int vsnprintf(char *buf, size_t n, const char *format, va_list arg);
```

- 头文件：`<stdarg.h>`、`<stdio.h>`
- 返回：如果空间足够返回存储在数组中的字符数，错误返回负值

---

# `vsprintf`

```c
int vsprintf(char *buf, const char *format, va_list arg);
```

- 头文件：`<stdarg.h>`、`<stdio.h>`
- 返回：如果空间足够返回存储在数组中的字符数，错误返回负值

---

# `syslog`

```c
void syslog(int priority, const char *format, va_list arg);
```

- 头文件：`<syslog.h>`、`<stdarg.h>`

---

# `wait`

```c
pid_t wait(int *status);
```

- 头文件：`<sys/wait.h>`
- 返回：如果正常返回进程 ID，返回 `0` 或 `1`

---

# `waitid`

```c
int waitid(type_t itype, id_t id, siginfo_t *infop, int options);
```

- 头文件：`<sys/wait.h>`
- `type`：`P_ID`、`PID`、`PGID`、`P_ALL`
- `options`：`WCONTINUED`、`WEXITED`、`WNOHANG`、`NOWOWAY`、`WSTOPPED`
- 返回：如果正常返回 `0`，错误返回 `1`
- 平台：Solaris 9

---

# `waitpid`

```c
pid_t waitpid(pid_t pid, int *status, int options);
```

- 头文件：`<sys/wait.h>`
- `options`：`0`、`WCONTINUED`、`WNOHANG`、`WUNTRAC`
- 返回：如果正常返回进程 ID，返回 `0` 或 `1`

---

# `wait3`

```c
pid_t wait3(int *status, int options, struct rusage *usage);
```

- 头文件：`<sys/wait.h>`
- 返回：如果正常返回 `0`，错误返回 `1`

---

## 我们自己的函数的原型

```c
char *path_alloc(int);
long open_max(void);
void clr_int(int);
void set_flint(int);
void pr_ext(int);
void pr_mask(const char *);
Sigfunc sigsignal_int(int, Sigfunc);
int ty_break(int);
int ty_raw(int);
int ty_reset(int);
void ty_atext(void);
#ifdef "_tty_void"
#include "my_types.h"
#endif
#endif
```

* 图 2.15
* 图 2.16
* 图 3.11
* 图 3.11
* 图 8.5
* 图 10.14
* 图 10.19
* 图 18.20
* 图 18.20
* 图 18.20
* 图 18.20

---

## 网络读写相关函数

```c
void sleep_unsigned(int);
size_t read(int fd, void *, size_t);
size_t write(int fd, const void *, size_t);
void daemonce(const char *);
```

* 练习 14.6
* 图 14.29
* 图 14.29
* 图 13.1

---

## 管道和套接字相关函数

```c
int *s_pipe(int);
int recv(int fd, void *, size_t);
const void *;
int send(int fd, const void *, size_t);
int err_int(int);
const char *;
int listen(int fd, const char *);
int accept(int fd, uid_t *);
```

* 图 17.6 和 17.13
* 图 17.21 和 17.23
* 图 17.20 和 17.22
* 图 17.19
* 图 17.10 和 17.15
* 图 17.11 和 17.16

---

## 客户端连接和参数缓冲函数

```c
int cli_conn(const char *);
int buf_args(char *, int (*func)(char *));
```

* 图 17.12 和 17.17
* 图 17.32

---

## 伪终端和进程派生函数

```c
int pytm_open(char *);
int pys_open(char *);
#ifdef TIOCWIGNS
pid_t pid_fork(int, int, const const struct *);
```

* 图 19.8, 19.9, 和 19.10
* 图 19.8, 19.9, 和 19.10
* 图 19.11
