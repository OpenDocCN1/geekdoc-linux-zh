
![](img/902515e97eef28cac8083866e00a6f4c_619_0.png)

兼容性规则适用于不同进程发出的锁请求，而不适用于单个进程发出的多个锁请求。如果一个进程对文件的某个范围已有一个锁，随后该进程尝试在相同范围内放置锁将用新锁替换现有的锁。因此，如果一个进程对文件的第 1632 字节拥有写锁，然后尝试对第 1632 字节放置读锁，该请求将成功（假设我们没有与任何试图锁定文件相同部分的其他进程发生竞争），并且写锁将被读锁替换。

要获取读锁，文件描述符必须以读模式打开；要获取写锁，描述符必须以写模式打开。

现在我们描述 `flock` 函数的三个命令。

`F_GETLK`：确定由 `flock` 描述的锁是否被其他锁阻塞。如果存在阻止我们创建锁的锁，则会提供该排他锁与 `flockptr` 指向的信息重叠的信息。如果不存在阻止我们创建锁的锁，则指向的结构将保持不变，但 `l_type` 成员外，它会被设置为 `F_UNLCK`。

## `F_SETLK`

如果我们尝试锁定一个 `F_type`（`F_RDLOCK` 类型）且系统的兼容性要求不满足条件（如 [图 14.3]() 所示），则 `fcntl` 立即返回并将 `errno` 设置为 `EACCES` 或 `EAGAIN`。

此外，POSIX 允许实现返回错误代码，本文描述的所有实现实现在无法满足锁请求时都会返回 `EAGAIN`。

此命令也用于通过 `flock`（`F_UNLCK` 类型）清除锁。

## `F_SETLKW`

此命令是 `F_SETLK` 的阻塞版本。请注意，在 `F_GETLK` 和尝试放置锁之间，POSIX 不保证状态保持不变。如果我们使用 `F_SETLKW`，进程将睡眠直到锁可用或被信号中断。

## 图 14.4. 文件范围锁

![](img/902515e97eef28cac8083866e00a6f4c_620_0.png)

![](img/902515e97eef28cac8083866e00a6f4c_621_0.png)

## 请求和释放锁的示例

为了避免在所有元素中手动分配 `flock` 结构，图 14.5 中的 `lock_reg` 处理了这些。

由于大多数锁定或解锁区域的操作（`F_GETLK` 命令很少使用），我们通常使用以下宏，它们定义在 `as` 中：

```c
#define read_lock(fd, offset, whence, len)
lock_reg(fd, F_SETLK, F_RDLOCK, (offset, whence, len))
#define read_lock(fd, offset, whence, len)
lock_reg(fd, F_SETKW, F_RDLOCK, (offset, whence, len))
#define write_lock(fd, offset, whence, len)
lock_reg(fd, F_SETLK, F_WRLOCK, (offset, whence, len))
#define write_lock(fd, offset, whence, len)
lock_reg(fd, F_SETKW, F_WRLOCK, (offset, whence, len))
#define un_lock(fd, offset, whence, len)
lock_reg(fd, F_SETLK, F_UNLCK, (offset, whence, len))
```

我们按照 `lseek` 函数相同的顺序正确定义了这些宏的前三个参数。

## 图 14.5. 锁定或解锁文件区域的函数

```c
#include "as.h"
#include <fcntl.h>

int
lock_reg(int fd, int cmd, int type, off_t offset, int whence, off_t len)
{
    struct flock lock;

    lock.l_type = type; /* F_RDLCK, F_WRLCK, F_UNLCK */
    lock.l_start = offset; /* 相对于 l_whence 的字节偏移量 */
    lock.l_whence = whence; /* SEEK_SET, SEEK_CUR, SEEK_END */
    lock.l_len = len; /* 字节（0 表示 EOF） */

    return(fcntl(fd, cmd, &lock));
}
```

# 锁的测试示例

图 14.6 定义了 `lock_test` 函数，我们将用它来测试锁。

如果锁会阻塞参数所请求的请求，该函数返回持有该锁的 ID。否则，函数返回 0（假）。通常，我们通过两个宏（在 `apue.h` 中定义）调用此函数：

```c
#define is_read_lockable(fd, offset, whence) \
    (lock_test(fd), F_RDLCK, (offset), (whence), len)) == 0
#define is_write_lockable(fd, offset, whence) \
    (lock_test(fd), F_WRLCK, (offset), (whence), len)) == 0
```

注意，当一个进程当前持有某个锁定文件的部分时，它无法使用 `lock_test` 函数。`F_GETLK` 命令的定义规定，返回给现有锁的信息将阻止我们创建自己的锁。`F_SETLK` 和 `F_SETKW` 命令如果发现存在现有锁，则总是替换该锁；我们永远不会在自己的锁上阻塞；因此，`F_GETLK` 命令永远不会报告我们自己的锁。

# 图 14.6. 测试锁条件的函数

```c
#include "apue.h"
#include <fcntl.h>

pid_t
lock_test(int fd, int type, off_t offset, int whence, off_t len)
{
    struct flock lock;
    lock.l_type = type; /* F_RDLCK 或 F_WRLCK */
    lock.l_start = offset; /* 相对于 l_whence 的字节偏移 */
    lock.l_whence = whence; /* SEEK_SET, SEEK_CUR, SEEK_END */
    lock.l_len = len; /* 字节（0 表示 EOF） */

    if (fcntl(fd, F_GETLK, &lock) < 0)
        err_sys("fcntl error");

    if (lock.l_type == F_UNLCK)
        return(0); /* 假，区域未被另一个进程锁定 */
    return(lock.l_pid); /* 真，返回锁所有者的 pid */
}
```

# 死锁示例

当两个进程都在等待另一个进程已锁定的资源时，就会发生死锁。如果控制锁的进程在尝试锁定另一个由不同进程控制的资源时进入睡眠，就存在死锁的可能性。

图 14.7 显示了死锁的示例。子进程锁定字节 0，父进程锁定字节 1。然后，子进程尝试锁定另一个另一个被锁定的字节。通过使用第 8.9 节产生的同步结果（`TELL_WAIT`/`WAIT`），使得每个进程都能等待另一个进程解锁。运行图 14.7 中的程序将得到：

```bash
$ .out
parent: got the lock, byte 1
child: got the lock, byte 0
child: write_lock error: Resource already avoided
parent: got the lock, byte 0
```

当检测到死锁时，内核必须选择一个进程来接收错误返回。在这个示例中，选择了子进程，但这是一个实现细节。在某些系统上，子进程总是接收错误。在其他系统上，父进程总是获取错误。在某些系统上，由于进行了多次锁定尝试，你甚至看到错误分布在子进程和父进程之间。

# 图 14.7. 死锁检测示例

```c
#include <apue.h>
#include <fcntl.h>

static void
lockbyte(const char *name, int fd, off_t offset)
{
    if (write_lock(fd, offset, SEEK_SET, 1) < 0)
        err_sys("%s: write_lock error", name);
    printf("%s: got the lock, %ld:\n", name, offset);
}

int
main(void)
{
    int fd;
    pid_t pid;

    /*
    创建一个文件并向写入两个字节。
    */
    if ((fd = create("templock", FILE_MODE)) < 0)
        err_sys("%s:create error");
    if (write(fd, "ab", 2) != 2)
        err_sys("%s:write error");

    TELL_WAIT();
    if ((pid = fork()) < 0)
        err_sys("%s:fork error");
    } else if (pid == 0)   /* 子进程 */ {
        lockbyte("child", fd, 0);
        TELL_PARENT(getppid());
        WAIT_PARENT();
        lockbyte("child", fd, 1);
    } else { /* 父进程 */
        lockbyte("parent", fd, 1);
        TELL_CHILD(pid);
        WAIT_CHILD();
        lockbyte("parent", fd, 0);
        exit(0);
    }
}
```

# 实现锁的继承与释放

三条规则支配记录锁的自动继承和释放。

1. 锁与进程和文件相关。这有两个含义。第一个是显而易见的：当进程终止时，其所有的锁都会被释放。第二个并不显而易见：当描述符关闭时，该描述符所引用文件的任何锁都会被释放。这意味着如果我们

```c
fd1 = open(pathname, ...);
read_lock(fd1, ...);
fd2 = dup(fd1);
```

关闭 `fd1` 后，对该文件的任何锁都会被释放。`F_GETLK` 命令定义规定，返回给现有锁的信息将阻止我们创建自己的锁。`F_SETLK` 和 `F_SETKW` 命令如果存在现有锁，则总是替换该锁；我们永远不会在自己的锁上阻塞；因此，`F_GETLK` 命令永远不会报告我们自己的锁。
