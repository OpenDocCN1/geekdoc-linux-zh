
```
#define _XOPEN_SOURCE 600
#include <stdlib.h>
#include <fcntl.h>
#include "pty_master.h" /* 声明 ptyMasterOpen() */
#include <unistd.h>

int
ptyMasterOpen(char *slaveName, size_t snLen)
{
    int masterFd, savedErrno;
    char *p;

    masterFd = open(..., O_RDWR | O_NOCTTY); /* 打开 pty master */
    if (masterFd == -1) {
        return -1;
    }

    if (grantpt(masterFd) == -1) { /* 给从设备 pty 访问权限 */
        savedErrno = errno;
        close(masterFd);
        errno = savedErrno; /* 可能会改变 'errno' */
        return -1;
    }

    if (unlockpt(masterFd) == -1) { /* 解锁从设备 pty */
        savedErrno = errno;
        close(masterFd);
        errno = savedErrno; /* 可能会改变 'errno' */
        return -1;
    }

    p = ptsname(masterFd); /* 获取从设备 pty 名称 */
    if (p == NULL) {
        savedErrno = errno;
        close(masterFd);
        errno = savedErrno; /* 可能会改变 'errno' */
        return -1;
    }

    if (strlen(p) < snLen) {
        strncpy(slaveName, p, snLen);
    } else { /* 如果缓冲区太小则返回错误 */
        close(masterFd);
        errno = ENOFLOW;
        return -1;
    }

    return masterFd;
}
```

## 64.4 使用伪终端连接进程：`ptyFork()`

我们现在准备好实现一个函数，它可以完成使用伪终端建立两个进程之间连接的所有工作，如图 64-2 所示。`ptyFork()` 函数创建一个子进程，该子进程通过伪终端对与父进程连接。

```c
#include <pty.h>

pid_t ptyFork(int masterFd, char *slaveName, size_t snLen
    const struct termios *slaveTermios, const struct winsize *slaveWs);
```

父进程：返回子进程进程 ID，错误时返回 -1；

子进程：创建成功：返回 0

`ptyFork()` 的实现见列表 64-2。该函数执行以下步骤：

- 使用 `ptyMasterOpen()` 打开一个伪终端主设备（列表 64-1）

- 如果 `slaveName` 参数不为 NULL，则将伪终端的名称复制到 slave 中（如果 `slaveName` 不为 NULL，则它必须指向一个至少有 `snLen` 字节的缓冲区）。如果合适，调用者可以使用此名称来更新登录计费文件（第 40 节）。更新登录计费文件对于提供登录服务的应用程序（如 `ssh`、`login` 和 `telnet`）是合适的。另一方面，像 `script`（第 64.6 节）这样的程序不会更新登录计费文件。

- `Fork()` 创建子进程 ③③

- 父进程在 `fork()` 之后所做的所有工作是将伪终端主设备的文件描述符返回给 `masterFd` 指向的整数 ④

- fork 之后，子进程执行以下步骤：

- 调用 `setsid()` 创建一个新的会话（第 34.3 节） ⑤ 子进程成为新会话的首进程并丢失其控制终端（如果有的话）。

- 关闭伪终端主设备的文件描述符 ⑥，因为子进程中不需要。

- 打开伪终端从设备 ⑦ 由于子进程在上一步丢失了控制终端，此步骤使伪终端成为子进程的控制终端。

- 如果定义了 `TIOCSCTTY` 宏，则对伪终端从设备的文件符执行 `TIOCSCTTY` `ioctl()` 操作 ⑧。此代码允许我们的 `ptyFork()` 在 BSD 平台上运行，这些平台上只有通过显式的 `TIOCSCTTY` 操作才能获取控制终端（参见第 34.4 节）。

- 如果 `slaveName` 参数不为 NULL，则调用 `tcsetattr()` 根据该参数指向的 `termios` 结构设置从设备的属性 ⑤。使用该参数对于某些交互式程序（例如 `script`）是一种便利，这些程序使用伪终端并需要将从设备的属性设置为与程序运行的终端相同。

- 如果 `slave` 不为 NULL，则执行 `ioctl` `TIOCWINZ` 操作，根据该参数指向的 `winsize` 结构设置伪终端的窗口大小 ⑥。执行此步骤的原因与上一步。

- 使用 `dup2()` 将从设备的文件描述符复制到标准输入、输出和错误流 ⑦。此时，子进程现在可以执行任意程序，该程序可以使用标准描述符与伪终端通信。该程序执行了所有在传统终端上可以执行的常规终端操作。

```c
mfd = ptyMasterOpen(slname, MAX_SNAME);
if (mfd == -1)
  return -1;
```

```c
if (slaveName != NULL) { /* 将从端名称返回给调用者
  if (strlen(slaveName) < snlen)
    strcpy(slaveName, slname, snlen);
```

```c
} else { /* 'slaveName' 空间太小 */
  close(mfd);
  errno = EOVERFLOW;
  return -1;
}
```

```c
childPid = fork();

if (childPid == -1) { /* fork() 失败 */
  savedErrno = errno; /* close() 可能会改变 'errno' */
  close(mfd);
  errno = savedErrno; /* 防止泄露文件描述符 */
  return -1;
}
```

```c
if (childPid != 0) { /* 父进程 */
  *masterFd = mfd; /* 父进程获取 master fd */
  return childPid; /* 类似于 fork(*) 的父进程 */
}
```

/* 子进程继续执行到这里 */

```c
if (setsid() == -1) /* 开启新会话 */
  err_exit("ptyfork:setsid:%s");
```

```c
close(mfd); /* 子进程不需要 */
```

```c
slaveFd = open(slname, O_RDWR);
if (slaveFd == -1)
  err_exit("ptyfork:open-slave:%s");
```

```c
#ifdef TIOCSCTTY /* 在 BSD 上获取控制 tty */
if (ioctl(slaveFd, TIOCSCTTY, 0) == -1)
  err_exit("ptyfork:ioctl-TIOCSCTTY:%s");
#endif
```

```c
if (slaveTermios == NULL) /* 设置从端 tty 属性 */
  if (tcsetattr(slaveFd, TCSANOW, slaveTermios) == -1)
    err_exit("ptyfork:tcsetattr:%s");
```

```c
if (slaveWS == NULL) /* 设置从端 tty 窗口大小 */
  if (ioctl(slaveFd, TIOCSWINZ, slaveWS) == -1)
    err_exit("ptyfork:ioctl-TIOCSWINZ:%s");
```
