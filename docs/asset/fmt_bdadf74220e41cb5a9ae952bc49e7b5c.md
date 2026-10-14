
执行的操作取决于参数 `cmd`。在文件 `<fcntl.h>` 中定义了一系列常量：

- `F_DUPFD`：这等于原语 `dup2`。输入/输出描述符 `fd` 在描述符 `arg` 中复制。
- `F_GETFD`：返回标记 `'close-on-exec'`。如果该标志为零，则当当前进程调用执行新程序的原语时，文件将保持打开；否则，文件在调用 `exec` 时会自动关闭。
- `F_SETFD`：设置标记 `'close-on-exec'`。
- `F_GETFL`：返回状态标志位。
- `F_SETFL`：修改状态标志位。
- `F_GETOWN`：返回文件的所有者。
- `F_SETOWN`：设置文件的所有者。

当执行原语 `fcntl` 发生错误时，变量 `errno` 可以取以下值：

| 错误代码 | 含义 |
|---|---|
| `EACCES` | 进程对 `pathname` 指定的文件没有写权限 |
| `EFAULT` | `buf`, `typ` 或 `pathname` 包含无效地址 |
| `EINVAL` | `cmd` 或 `arg` 指定了无效值 |
| `EPERM` | 进程没有必要的权限 |

### 6.4.7 锁

#### 6.4.7.1 文件锁

原语 `flock` 允许对文件进行完全锁定。其语法如下：

```c
#include <sys/file.h>
```

```c
int flock (int fd, int operation);
```

`flock` 锁定或解锁通过参数 `fd` 传递的文件描述符。参数 `operation` 指定要执行的操作。在 `<sys/file.h>` 中定义了几个常量：

| 选项 | 含义 |
|---|---|
| `LOCK_SH` | 请求对文件的共享锁。多个进程可以同时拥有共享锁 |
| `LOCK_EX` | 请求对文件的排斥锁。只有一个进程可以拥有排斥锁 |
| `LOCK_UN` | 释放共享锁或排斥锁 |

发生锁定请求，调用进程可能会挂起。然而，如果指定了选项 `LOCK_NB`，则进程不会挂起；如果无法应用锁，原语 `flock` 将返回错误。
发生错误时，变量 `errno` 可以取以下值：

| 错误代码 | 含义 |
|---|---|
| `EBADF` | 指定的输入输出描述符无效 |
| `EINVAL` | `operation` 指定了无效值 |
| `EWOULDBLOCK` | 文件已锁定且指定了选项 `LOCK_NB` |

#### 6.4.7.2 锁定文件部分

第 6.4.5 节中描述的原语 `fcntl` 允许对文件的某个部分进行锁定。对于该原语的应用，参数 `arg` 应该包含 `flock` 结构体的地址，该结构在文件 `<fcntl.h>` 中定义，并包含以下字段：

| 类型 | 描述 |
|--- |--- |
| `off_t` | `l_start` 锁在文件中的位置 |
| `off_t` | `l_len` 锁定区域的长度 |
| `short` | `l_type` 锁的类型 |
| `short` | `l_whence` 位置类型 (`SEEK_SET`, `SEEK_CUR`, `SEEK_END`) |
| `pid_t` | `l_pid` 获取锁的进程编号 |

可以执行若干操作：

- `F_SETLK`：根据传递的 `flock` 结构体中的信息设置或释放锁。结构类型可以是 `F_RDLOCK` 实现共享锁，`F_WRLCK` 实现排他锁，以及 `F_UNLC` 释放锁。如果无法立即启用锁，`fcntl` 返回错误 `EACCES`。
- `F_SETKW`：类似于 `F_SETLK`。唯一的区别是，如果无法立即获取锁，调用进程将挂起等待。
- `F_GETLK`：获取现有锁的描述。如果已经存在与 `flock` 结构体中指定的锁冲突的锁，则修改后者的内容，并将描述现有锁的特征信息放置在其中。

`lockf` 函数为 `fcntl` 的锁定选项提供了一个更简单的接口。语法如下：

```c
#include <fcntl.h>
#include <unistd.h>
int lockf(int fd, int cmd, off_t len);
```

参数 `fd` 指定文件描述符，`len` 表示相对于当前设置的锁的大小，`cmd` 可以取以下值：

| 选项 | 含义 |
|--- |--- |
| `F_UNLOCK` | 解锁之前锁定的区域 |
| `F_TLOCK` | 锁定一个区域。如果无法立即获取，则返回错误 `EACCES` |
| `F_LOCK` | 锁定一个区域，挂起调用进程等待锁。 |
| `F_TEST` | 测试指定区域是否存在锁：如果存在锁，则返回错误 `EACCES` |

### 6.4.8 文件系统的挂载

Linux 提供了两个系统调用，允许对文件系统进行挂载和卸载。换句话说，文件系统在逻辑上与文件树结构连接或断开连接。这些调用留给具有超级用户权限的进程使用。

`mount` 和 `unmount` 原语的语法如下：

```c
#include <sys/mount.h>
#include <linux/fs.h>
int mount (const char *specialfile, const char *dir,
           const char *filesystemtype, unsigned long rwflag,
           const void *data);
```

```c
int unmount (const char *specialfile);
```

```c
int unmount (const char *dir);
```
