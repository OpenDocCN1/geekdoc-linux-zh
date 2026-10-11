
然而，鉴于 POSIX 采用保存的 set-user ID 模型以及 `seteuid()` 和 `setegid()` 函数，在新代码中不应使用 BSD 函数。甚至 4.4 BSD 文档也将这些函数标记为过时，建议改用 `seteuid()`/`seteuid()` 和 `setegid()`/`setgid()`。

## 11.6.3 使用 setuid 和 setgid 位

存在一些重要情况，要求以 root 身份运行的程序必须不可撤销地将其真实、有效和保存的 set-user ID 全部更改为普通用户的 ID。最明显的例子是登录程序，你每次登录到 GNU/Linux 或 Unix 系统时（无论是直接登录还是远程登录）都会使用它。存在一个程序层级结构，如*图 11.1*所述。

![](img/766b5597246d532412fad21b1c59ccec_451_0.png)

login 的代码过于复杂，无法在此展示，因为它涉及许多与当前讨论无关的任务。但我们可以概述登录时发生的步骤，如下所示：

1.  `init` 是原始进程。它的 PID 为 1。所有其他进程都源自它。内核在启动时手工创建进程 1 并在其中运行 `init`。它以真实 UID 和有效 UID 均设置为 0 的方式运行，即以 root 身份运行。
2.  `init` 读取 `/etc/inittab`，该文件除其他内容外，还告诉 `init` 应在哪些硬件设备上启动 `getty` 进程。对于每个此类设备（例如 GNU/Linux 系统上的控制台、串行终端或虚拟控制台），`init` 会 fork 出一个新进程。这个新进程随后使用 `exec()` 运行 `getty`（“get tty”，即终端）。在许多 GNU/Linux 系统中，此命令名为 `mingetty`。该程序打开设备，重置其状态，并打印 `login:` 提示符。
3.  在读到登录名后，`getty` exec 运行 `login`。登录程序在密码文件中查找用户名，提示输入密码并验证密码。如果匹配，登录进程继续执行。
4.  `login` 切换到用户的家目录，设置初始环境，然后设置初始的打开文件集。它关闭所有文件描述符，打开终端，并使用 `dup()` 将终端的文件描述符复制到 0、1 和 2。这就是已打开的标准输入、输出和错误文件描述符的来源。
5.  然后 `login` 使用 `setgroups()` 设置辅助组集，使用 `setgid()` 将真实、有效和保存的 set-group ID 设置为用户的值，最后使用 `setuid()` 将真实、有效和保存的 set-user ID 的所有三个值都设置为正在登录用户的值。注意，`setuid()` 的调用必须放在最后，以便其他两个调用能够成功。
6.  最后，`login` exec 运行用户的登录 shell。Bourne 风格的 shell 随后读取 `/etc/profile` 和 `$HOME/.profile`（如果这些文件存在）。最后，shell 打印提示符。

请注意，一个进程如何从系统进程转变为用户进程。`init` 的每个子进程最初都是 `init` 的副本。通过使用 `exec()`，同一进程执行不同的任务。通过调用 `setuid()` 从 root 更改为普通用户，该进程最终直接为用户工作。当你退出 shell（通过 CTRL-D 或 `exit()`）时，该进程 simply 死亡。然后 `init` 重启循环，生成一个新的 `getty`，它打印一个新的 `login:` 提示符。

> 注意：即使进程更改了其任何或所有 UID 或 GID，打开的文件仍保持打开且可用。因此，setuid 程序应预先打开所有必要的文件，将它们的 ID 更改为真实用户的值，并在没有额外特质的情况下继续执行其余任务。

*表 11.1* 总结了操作 UID 和 GID 值的六个标准函数。

### *表 11.1*
设置真实 ID 和有效 ID 的 API 摘要

| 函数 | 设置 | 永久性 | 普通用户 | Root |
| :--- | :--- | :--- | :--- | :--- |
| `setuid()` | E | 否 | 来自 R, E, S | 任意值 |
| `setegid()` | E | 否 | 来自 R, E, S | 任意值 |
| `setgid()` | Root: R, E, S<br>其他: E | Root: 是<br>其他: 否 | 来自 R, E | 任意值 |
| `setgid()` | Root: R, E, S<br>其他: E | Root: 是<br>其他: 否 | 来自 R, E | 任意值 |
| `setreuid()` | E, 可能设置 R | 否 | 来自 R, E | 任意值 |
| `setregid()` | E, 可能设置 R | 否 | 来自 R, E | 任意值 |

## 11.7 处理所有三个 ID：`getresuid()` 和 `setresuid()` (Linux)

Linux 提供了额外的系统调用，允许你直接操作真实、有效和保存的用户和组 ID：

```c
#include <sys/types.h>
#include <unistd.h>

int getresuid(uid_t *ruid, uid_t *euid, uid_t *suid);
int getresgid(gid_t *rgid, gid_t *egid, gid_t *sgid);
int setresuid(uid_t ruid, uid_t euid, uid_t suid);
int setresgid(gid_t rgid, gid_t egid, gid_t sgid);
```

这些函数如下：

```c
int getresuid(uid_t *ruid, uid_t *euid, uid_t *suid)
```

获取真实、有效和保存的 set-user ID 值。成功时返回 0，出错时返回 -1，并由 `errno` 指示问题所在。

```c
int getresgid(gid_t *rgid, gid_t *egid, gid_t *sgid)
```

获取真实、有效和保存的 set-group ID 值。成功时返回 0，出错时返回 -1，并由 `errno` 指示问题所在。

```c
int setresuid(uid_t ruid, uid_t euid, uid_t suid)
```

分别设置真实、有效和保存的 set-user ID 值。当参数值为 -1 时，对应的 UID 保持不变。

当进程以 root 身份运行时，参数可以是任意值。（但是，使用非零值作为 `euid` 会导致永久且不可撤销地丧失 root 特权。）否则，参数必须是当前真实、有效或保存的 set-user ID 值之一。

```c
int setresgid(gid_t rgid, gid_t egid, gid_t sgid)
```

分别设置真实、有效和保存的 set-group ID 值。当参数值为 -1 时，对应的 GID 保持不变。

此函数类似于 `setresuid()`。

`setresuid()` 和 `setresgid()` 函数特别有价值，因为其语义定义明确。程序员可以确切知道调用的效果。

此外，这些调用是“全或无”的操作：它们要么完全成功，实现所需的更改；要么完全失败，保持当前状态不变。这提高了可靠性，因为同样可以确切知道发生了什么。

## 11.8 穿越安全雷区：setuid root

穿越真实的雷区很困难，但并非不可能。然而，这不是未经训练或经验就应轻易尝试的事情。

同样，编写以 setuid root 方式运行的程序也是一项艰巨的任务。有许多需要知晓的问题，几乎任何方面都可能产生意外的安全后果。此类尝试应谨慎进行。

特别是，花时间阅读关于 Linux/Unix 安全问题并学习如何编写 `setuid` `root` 程序是值得的。如果你在读了这本书且没读其他东西后就直接投身于这样的挑战中，请相信你的系统会被轻松且立即入侵。不太可能你或你的客户会对此感到满意。

以下是一些指导原则：

- 尽可能少地以 `root` 身份执行操作。谨慎使用你的超级权限，仅在其绝对需要时使用。

- 正确设计你的程序。将你的程序模块化，以便所有 `root` 操作都可以预先完成，而程序的其余部分以普通用户身份运行。

- 在更改或放弃特权时，如果拥有 `setresuid()` 请使用它。否则请使用 `setreuid()`，因为这两个函数具有最清晰的语义。仅在你希望更改是永久时才使用 `setuid()`。

- 以正确的顺序从 `root` 切换到普通用户：先设置组集和 GID 值，然后设置 UID 值。

- 对 `fork()` 和 `exec()` 特别小心；除非你显式更改它们，否则真实和有效 UID 在这些调用中不会改变。

- 考虑为你的应用程序使用 `setgid` 权限和一个特殊组。如果可行，这将为你省去许多麻烦。

- 考虑丢弃继承的环境变量。如果你必须保留一些环境变量，请尽可能保留得少。确保为 `PATH` 和 `IFS` 环境变量提供合理的值。

- 避免使用依赖 `PATH` 环境变量值的 `execl()` 和 `execvp()`（虽然如果你自己重置了 `PATH`，这个问题会较少）。

这些仅仅是穿越这个以陷阱、诡雷和地雷著称的危险区域的众多战术中的少数几个。有关其他信息来源的指引，请参见下一节。

## 11.9 建议阅读

Unix（因此包括 GNU/Linux）安全是一个需要知识和经验才能妥善处理的主题。在互联网时代，这一主题变得更加困难，而不是更容易。

