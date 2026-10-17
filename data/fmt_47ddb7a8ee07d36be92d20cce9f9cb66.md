
# 888 类型原型 附录 A

```c
size_t strftime(char *restrict buf, size_t maxsize, const char *restrict format, struct tm *restrict tmptr);
```
`<time.h>`
返回：成功返回数组中的字符数，否则返回 0

p. 192

```c
size_t strftime_r(char *restrict buf, size_t maxsize, const char *restrict format, struct tm *restrict tmptr, locale_t locale);
```
`<time.h>`
返回：成功返回数组中的字符数，否则返回 0

p. 192

```c
char *strptime(const char *restrict buf, const char *restrict format, struct tm *restrict tmptr);
```
`<time.h>`
返回：解析的最后一个字符指针，否则返回 `NULL`

p. 195

```c
char *strsignal(int signo);
```
`<string.h>`
返回：描述信号的指针

p. 380

```c
int symlink(const char *actualpath, const char *sympathy);
```
`<unistd.h>`
返回：成功返回 0，错误返回 -1

p. 123

```c
int symlinkat(const char *actualpath, int fd, const char *sympathy);
```
`<unistd.h>`
返回：成功返回 0，错误返回 -1

p. 123

```c
void sync(void);
```
`<unistd.h>`

p. 81

# 890 函数原型附录 A

```c
long sysconf(int name);
```
`<unistd.h>` p. 42

`name`: `_SC_ARG_MAX`, `_SC_EXIT_MAX`, `_SC_CLOCK_CLK_TCICK`, `_SC_GET_PAGES`, `_SC_HOST_SIZE`, `_SC_HOST_CONFIG_PAGE`, `_SC_LIBC_PAGES`, `_SC_PHYS_PAGES`, `_SC_PAGE_PAGES`, `_SC_PROCESS_PAGES`, `_SC_RSS_SIZE`, `_SC_RT_OPEN_MAX`, `_SC_RT_THREAD_SIZE`, `_SC_RT_MAX_PIDS`, `_SC_RT_MAX_SIGSIG`, `_SC_RT_MAX_PROCESSES`, `_SC_RT_RSS_SIZE`, `_SC_QUEUE_PRI`, `_SC_NODELIMIT`, `_SC_OS_VERSION`, `_SC_OPEN_FTMAX`, `_SC_PID_MAX`, `_SC_STREAMS_SIZE`, `_SC_SYS_CLK_TCICK`, `_SC_SYS_NPROCESS`, `_SC_SYS_PID_MAX`, `_SC_SYS_PHYS_PAGES`, `_SC_SYS_PAGES_TCID_SIZE`, `_SC_GET_TCID`, `_SC_TIME_MAX`, `_SC_TSTAVE_MAX`, `_SC_CLK_SEC`, `_SC_CLK_MIN`, `_SC_AV_SIZE`, `_SC_AV_NPROCESS`, `_SC_AV_MAX_SIG`, `_SC_AV_MAX_PIDS`, `_SC_AV_MAX_PROCESSES`, `___AV_RSS_SIZE`, `_SC_VERSION_MAX`, `_SC_NPROCESS_MAX`, `_SC_NPROCESS_MAX`, `_SC_SHMEM_SIZE`, `_SC_ADDRESS_SIZE`, `_SC_THREAD_SIZE`, `_SC_PAGE_SIZE`, `_SC_USER_P`, `_SC_CLK_SIZE`, `_SC_PAGES_SIZE`, `_SC_TCID_SIZE`, `_SC_TIME_SIZE`

```c
int truncate(const char *path, off_t length);
```
`<unistd.h>`
返回: OK时返回0，错误时返回 -1

```c
char *ttname(int fd);
```
`<unistd.h>`
返回: 路径名的指针，错误时返回 `NULL`

```c
mode_t umask(mode_t cmask);
```
`<sys/stat.h>`
返回: 之前的文件创建掩码

```c
int uname(struct utname *name);
```
`<sys/utsname.h>`
返回: OK时返回非负值，错误时返回 -1

```c
int ungetc(int c, FILE *fp);
```
`<stdio.h>`
返回: OK时返回 `c`，错误时返回 `EOF`

```c
int unlink(const char *path);
```
`<unistd.h>`
返回: OK时返回0，错误时返回 -1

```c
int unlinkat(int fd, const char *path, int flag);
```
`<unistd.h>`
`flag`: `AT_REMOVED`
返回: OK时返回0，错误时返回 -1

```c
int unlockpt(int fd);
```
`<stdlib.h>`
返回: 成功时返回0，错误时返回 -1

```c
int setenv(const char *name, const char *value);
```
`<stdlib.h>`
返回: OK时返回0，错误时返回 -1

```c
int utimensat(int fd, const char *path,
struct timespec times[2], int flag);
```
`<sys/stat.h>`
`flag`: `AT_SYMLINK_NOFOLLOW`
返回: OK时返回0，错误时返回 -1

```c
int utimes(const char *path, struct timeval times[2]);
```
`<sys/time.h>`
返回: OK时返回0，错误时返回 -1

# 附录 A

# 函数原型

```c
int vdprintf(int fd, const char *restrict format, va_list arg);
```
`<stdarg.h>`
`<stdio.h>`
返回: OK时返回输出的字符数，输出错误时返回负值

p. 161

```c
int vprintf(FILE *restrict fp, const char *restrict format, va_list arg);
```
`<stdarg.h>`
`<stdio.h>`
返回: OK时返回输出的字符数，输出错误时返回负值

p. 161

```c
int vscanf(FILE *restrict fp, const char *restrict format, va_list arg);
```
`<stdarg.h>`
`<stdio.h>`
返回: 分配的输入项数，输入错误或在任何转换前到达文件结束返回 `EOF`

p. 163

```c
int vprintf(const char *restrict format, va_list arg);
```
`<stdarg.h>`
`<stdio.h>`
返回: OK时返回输出的字符数，输出错误时返回负值

p. 161

```c
int vscanf(const char *restrict format, va_list arg);
```
`<stdarg.h>`
`<stdio.h>`
返回: 分配的输入项数，输入错误或在任何转换前到达文件结束返回 `EOF`

p. 163

```c
int vsnprintf(char *restrict buf, size_t n, const char *restrict format, va_list arg);
```
`<stdarg.h>`
`<stdio.h>`
返回: 如果缓冲区足够大则应存储在数组中的字符数，编码错误时返回负值

p. 161

```c
int vsprintf(char *restrict buf, const char *restrict format, va_list arg);
```
`<stdarg.h>`
`<stdio.h>`
返回: OK时返回存储在数组中的字符数，编码错误时返回负值

p. 161

# 函数原型

```c
int vsscanf(const char *restrict buf, const char *restrict format, va_list arg);
```
`<stdarg.h>`
`<stdio.h>`
返回: 分配的输入项数，输入错误或在任何转换前到达文件结束返回 `EOF`

```c
void vsyslog(int priority, const char *format, va_list arg);
```
`<syslog.h>`
`<stdarg.h>`
平台: FreeBSD 8.0, Linux 3.2.0, Mac OS X 10.6.8, Solaris 10

```c
pid_t wait(int *statloc);
```
`<sys/wait.h>`
返回: OK时返回进程 ID，或错误时返回 -1

```c
int waitid(int_t itype, id_t id, siginfo_t *infop, int options);
```
`<sys/wait.h>`
`itype`: `P_PID`, `P_PGID`, `P_ALL`
`options`: `CONTINUED`, `WEXITED`, `WNOHANG`, `WUNTRACED`, `WSTOPPED`
返回: OK时返回0，或错误时返回 -1
平台: Linux 3.2.0, Solaris 10

```c
pid_t waitpid(pid_t pid, int *statloc, int options);
```
`<sys/wait.h>`
`options`: `CONTINUED`, `WNOHANG`, `WUNTRACED`
返回: OK时返回进程 ID，或错误时返回 -1

```c
pid_t wait3(int *statloc, int options, struct rusage *rusage);
```
`<sys/types.h>`
`<sys/wait.h>`
`<sys/time.h>`
`options`: `WNOHANG`, `WUNTRACED`
返回: OK时返回进程 ID，或错误时返回 -1
平台: FreeBSD 8.0, Linux 3.2.0, Mac OS X 10.6.8, Solaris 10

```c
pid_t wait4(pid_t pid, int options, struct rusage *rusage);
```
`<sys/types.h>`
`<sys/wait.h>`
`<sys/time.h>`
`<sys/resource.h>`
`options`: `WNOHANG`, `WUNTRACED`
返回: OK时返回进程 ID，或错误时返回 -1
平台: FreeBSD 8.0, Linux 3.2.0, Mac OS X 10.6.8, Solaris 10

```c
ssize_t write(int fd, const void *buf, size_t nbytes);
```
`<unistd.h>`
返回: OK时返回写入的字节数，错误时返回 -1

p. 72

```c
ssize_t writev(int fd, struct iovec *iov, int iovcnt);
```
`<sys/uio.h>`
返回: OK时返回写入的字节数，错误时返回 -1

p. 521

# 附录 B

# 杂项源码

## B.1 头文件

文中大多数程序都包含图 B1所示的 `utils.h`。它定义了常量（如 `MAXLINE`）和函数的原型。我们的头文件自动包含了这些头文件：`<stdio.h>`, `<stdlib.h>`（用于 `exit` 函数）以及 `<unistd.h>`（用于标准原型）。这减少了文中所有列表的大小。

```c
#ifndef _UTILS_H
#define _UTILS_H

#define POSIX_C_SOURCE 200809
#if defined(SOLARIS)
#define _XOPEN_SOURCE 600
else
#define _XOPEN_SOURCE 700
#endif

#include <sys/types.h>
#include <sys/stat.h>
#include <sys/termios.h>
#if defined (MACOS) || !defined(TIOCGWIN)
#include <ioctl.h>
#endif
#include <stdio.h> /* 为了方便 */
#include <stdlib.h> /* 为了方便 */
#include <stddef.h> /* 用于 offset */
#include <string.h> /* 为了方便 */
#include <unistd.h> /* 为了方便 */
#include <signal.h> /* 用于 SIG */
```

```c
#define MAXLINE 4096  /* 行长度 */

/* 新文件的默认权限。 */

#define FILE_MODE (S_IRUSR | S_IWUSR | S_IRGRP | S_IROTH)

/* 新目录的默认权限。 */

#define DIR_MODE (S_IRWXUSR | S_IXGRP | S_IXOTH)

typedef void signal(int);   /* 信号处理器 */

#define min(a,b) ((a) < b) ? (a) : (b)

#define max(a,b) ((a) > b) ? (a) : (b)
```

```c
char *path_alloc(size_t *);   /* 图 B.16 */
open(void);               /* 图 B.17 */
int set_cl(int);          /* 图 B.9 */
void clr_fl(int, int);        /* 图 B.12 */
void set_fl(int, int);
void pr_exit(int);         /* 图 B.5 */
void pr_mask(const char *);  /* 图 B.14 */
void *signal_intr(int, sig *); /* 图 B.19 */
void daemonize(const char *);   /* 图 B.1 */
void sleep_us(unsigned int);  /* 练习 B.5 */
size_t readn(int, void *, size_t);  /* 图 B.24 */
size_t written(int, const void *, size_t); /* 图 B.24 */
int fd_pipe(int *);      /* 图 B.2 */
int recv_fd(int, size_t (*func)(int, const void *, size_t));  /* 图 B.14 */
```

## B.1 我们的头文件 897

```c
int send_fd(int, int);               /* 图 B.13 */

int send_err(int, int, const char *);                     /* 图 B.12 */

int serv_list(const char *);                     /* 图 B.8 */

int serv_accept(int, uid_t *);                    /* 图 B.9 */

int cli_conn(const char *);                      /* 图 B.10 */

int buf_args(char, int (*func)(int, char *));                           /* 图 B.23 */

int tty_cbreak(int);                                 /* 图 B.20 */

int tty_raw(int);                                  /* 图 B.20 */

int tty_reset(void);                               /* 图 B.20 */

void tty_atexit(void);                             /* 图 B.20 */

struct termios*termios(char *, int);

int ptym_open(char *, int);                        /* 图 B.9 */

int ptys_open(char *);                           /* 图 B.9 */

#ifdef TIOCGWINZ

pid_t fork(int *, char *, int, const struct termios *const winsize *);             /* 图 B.10 */

#endif

int lock_reg(int, int, off_t, off_t);      /* 图 B.14.5 */
```
