

## 表 21.1 非线程安全函数

| asctime() | fcvt() | getpwnam() | nl_langinfo() |
| basename() | ftw() | getpwuid() | ptsname() |
| catgets() | gcvt() | getservbyname() | putc_unlocked() |
| crypt() | getdate_unlocked() | getservbyport() | putchar_unlocked() |
| ctime() | getchar_unlocked() | getservent() | putenv() |
| dbm_clearerr() | getdate() | getutxent() | pututxline() |
| dbm_close() | getenv() | getutxid() | rand() |
| dbm_delete() | getgrent() | getutxline() | readdir() |
| dbm_error() | getgrgid() | gmtime() | setenv() |
| dbm_fetch() | getgrnam() | hcreate() | setgrent() |
| dbm_firstkey() | gethostbyaddr() | hdestroy() | setkey() |
| dbm_nextkey() | gethostname() | hsearch() | setpwent() |
| dbm_open() | gethostent() | inet_ntoa() | setutxent() |
| dbm_store() | getlogin() | l64a() | strerror() |
| dirname() | getnetbyaddr() | lgamma() | strtok() |
| dlerror() | getnetbyname() | lgammaf() | ttyname() |
| drand48() | getnetent() | lgammaf() | unsetenv() |
| ecvt() | getopt() | localeconv() | wcstombs() |
| encrypt() | getprotobyname() | localtime() | wctomb() |
| endgrent() | getprotobynumber() | lrand48() |  |
| endpwent() | getprotobyname() | mrand48() |  |
| endutxent() | getpwent() | nftw() |  |

关于 pthread 编程和/或 UNIX 系统编程的资料更全面地讨论了这些主题。

## 21.4 后台运行进程：守护进程

我们在第 10 章详细讨论了后台进程和守护进程的执行。提供服务给用户或进程的系统进程被称为守护进程。守护进程的常见用途是在服务器进程中。一些常见的守护进程示例有 http（Web）服务器（httpd）、安全 Shell 服务器（sshd）、UNIX 超级服务器（inetd）、打印机服务器（lpd）和分页服务器（pageda）。

在本节中，我们讨论如何编写代码，使进程在执行时自动成为守护进程。守护进程的一个特征是它们与标准文件断开连接。创建守护进程相当简单。问题归结为创建子进程，让父进程退出，并允许子进程继续并成为守护进程。以下会话中的 daemon.c 程序说明了这一概念。父进程退出后，子进程现在作为守护进程，在进入无限循环读取客户端请求并响应之前显示其 PID。

```
% cat daemon.c
#include <unistd.h>
#define SIZE 32
```

```
int main(void)
{
    pid_t pid;
    char buf[SIZE];

    pid = fork();
    if (pid == -1) {
        perror("Fork failed");
        exit(1);
    }
    /* Parent process */
    if (pid > 0) {
        exit(0);
    }
    /* Child process: Continues and becomes the server */
    /* process running forever as a daemon */
    (void) sprintf(buf, "Daemon PID: %d\n", getpid());
    (void) write(1, buf, strlen(buf));
    while (1) {
        /* Wait for a client request */
        /* Serve the client request */
        sleep(10);    /* Dummy code */
    }
}
```

```
% gcc46 -w daemon.c -o daemon
% ./daemon
Daemon PID: 97272
% ps
  PID TT  STAT      TIME COMMAND
93220 1  Ss   0:00.69 -csh (csh)
97272 1  S    0:00.00 daemon
97273 1  R+   0:00.01 ps
% kill -9 97272
% ps
  PID TT  STAT      TIME COMMAND
93220 1  Ss   0:00.69 -csh (csh)
97273 1  R+   0:00.01 ps
%
```

## 练习 21.1

提供 10 个 UNIX 守护进程的名称及其用途。

## 练习 21.2

编译并运行前面的 daemon.c 程序，以确保它在你的系统上按预期工作。

## 21.5 忽略信号

我们在第 20 章详细讨论了信号和信号处理问题。在本节中，我们强调当你为服务器进程编写代码时，必须适当处理信号。

有时，你需要编写可以利用基于文本的配置文件初始化其数据结构的服务器进程，并且希望此类服务器能够在不停止的情况下动态重新配置。你可以通过向进程发送特定类型的信号并调用重新配置服务器的函数来实现这一点。UNIX 超级服务器 inetd 就是一个在收到 SIGHUP 时重新配置自身的服务器进程示例。因此，它包含类似以下的代码行：

```
signal(SIGHUP, sig_hup);
```

其中 sig_hup() 函数重新配置 inetd 的内部数据结构。inetd 的配置文件是 /etc/inetd.conf。

## 21.6 更改 UMASK

在服务器进程中设置 umask 很重要，这样服务器进程创建的所有文件，包括日志文件，都具有期望的访问权限，而不管 open() 或 creat() 系统调用中指定的模式如何。你可以通过使用 umask() 系统调用来实现，如下所示：

```
(void) umask(027);
```

我们在第 5 章详细讨论了在命令行设置 umask 以及新创建文件的权限位是如何设置的。在以下会话中，我们展示了在包含信号处理并设置 umask 之后 daemon.c 的代码。在 PC-BSD 系统上编译和运行该程序表明程序工作正确，并且在我们使用 kill 命令向其发送 SIGHUP 和 SIGINT 信号时守护进程不会终止。最终，我们使用 kill -9 16624 命令终止 daemon。该代码在 Solaris 机器上也能按预期工作。

```
% cat daemon.c
#include <unistd.h>
#include <sys/signal.h>

#define SIZE 32

int main(void)
{
    pid_t pid;
    char buf[SIZE];
    pid = fork();
    if (pid == -1) {
```

