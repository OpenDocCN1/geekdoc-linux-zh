
列表 60-5 的前几行由开头的 `#` 字符注释掉了；我们现在显示它们，是因为稍后我们将引用到 echo 服务。

`/etc/inetd.conf` 的每行由以下字段组成，并用空格分隔：

- 服务名称（Service name）：指定来自 `/etc/inetd` 文件的服务的名称。结合协议字段，这用于查找 `/etc/services` 以确定 `inetd` 应该为该服务监控哪个端口号。
- Socket 类型（Socket type）：指定该服务使用的 socket 类型——例如 `stream`（流式）或 `dgram`（数据报）。
- 协议（Protocol）：指定该服务使用的协议。此字段可以包含 `/etc/protocols` 文件列出的任何 `inetd` 协议（在 `protocols(5)` 手册页中有记录），但几乎每个服务都使用 `tcp`（用于 TCP）或 `udp`（UDP）。
- 标志（Flags）：此字段包含 `wait` 或 `nowait`。此字段指定由 `inetd` 启动的服务器是否（临时）接管该服务的 socket 的管理。如果启动的服务器管理 socket，则该字段指定为 `wait`。这会导致 `inetd` 在启动的服务器退出时从其监控的 `select()` 文件描述符中移除该 socket（`inetd` 通过 `SIGCHLD` 的处理程序检测到这一点）。我们将在下文中提到这一点。
- 登录名称（Login name）：此字段由来自 `/etc/passwd` 的用户名组成，可选地跟着一个点 (`.`) 和来自 `/etc/group` 的组名。这些决定了启动的服务所属的用户和组 ID。（由于 `inetd` 以 root 的有效 ID 运行，其子进程也具有特权，并根据需要调用 `setuid()` 和 `setgid()` 来更改凭据。）
- 服务器程序（Server program）：指定要执行的服务器程序的路径。
- 服务器程序参数（Server program arguments）：此字段指定一个或多个用空格分隔的参数，在执行服务器程序时作为参数列表使用。第一个对应启动程序中的 `argv[0]`，通常与服务器程序名称的基本文件名相同。下一个参数对应 `argv[1]`，依此类推。

由于 SUSv3 未规定 `inetd` 的顺序和其配置文件的格式，因此在 `inetd.conf` 字段中可以指定的值上存在一些（通常是微小的）差异。大多数版本的 `inetd` 都提供了我们在正文中描述的语法。欲需更多详细信息，请参阅 `inetd.conf(8)` 手册页。

出于效率考虑，`inetd` 自身实现了一些简单的服务，而不是通过执行服务器来完成任务。UDP 和 TCP echo 服务是 `inetd` 实现的服务的示例。对于此类服务，相应的 `/etc/inetd.conf` 记录被指定为 `internal`，并省略了服务器程序参数。（在 60-5 的示例行中，我们看到 echo 服务被注释掉了。要启用 echo 服务，）

每当我们更改 `/etc/inetd.conf` 文件时，我们需要向 `inetd` 发送 `SIGHUP` 信号，请求其重新读取该文件：

```bash
# killall -HUP inetd
```

# 示例：通过 inetd 调用 TCP echo 服务

我们之前提到 `inetd` 简化了服务器的编程，特别是当前的（通常是 TCP）服务器。它是通过代表其调用的服务器执行以下步骤来实现的：

- 执行所有与 相关的初始化，调用 `socket()`、`bind()` 和（对于 TCP 服务器）`listen`。
- 对于 TCP 服务，对新连接执行 `accept()`。
- 创建一个新进程来处理传入的 UDP 数据报或 TCP 连接。该进程会被设置为守护进程。`inetd` 程序通过 `fork()` 处理进程创建的所有细节，并通过诸如 `SIGCHLD` 的处理程序来回收死去的子进程。
- 将 UDP 套接字或连接的 TCP 套接字的文件描述符复制到文件描述符 0、1 和 2 上，并关闭所有其他文件描述符（因为它们在执行服务器程序时未被使用）。
- 执行服务器程序。

（在上述步骤的描述中，我们假设通常的情况是：`/etc/inetd.conf` 中服务条目的 `flags` 字段对于 TCP 服务指定为 `nowait`，对于 UDP 服务指定为 `wait`。）

关于 `inetd` 如何简化 TCP 服务的编程的一个示例，我们在列表 60-6 中展示了列表 60-4 中 TCP 服务器的 `inetd` 调用等效实现。由于 `inetd` 执行了上述所有步骤，子进程执行的处理客户端请求的剩余代码都可以从文件描述符 0 (`STDIN_FILENO`) 读取。

如果服务器位于 `/bin` 目录（例如），我们需要在 `/etc/inetd.conf` 中创建条目，以便 `inetd` 调用该程序：

`echo tcp nowait /bin/is_echo_inetd_sv is_echo_inetd_sv`

## 列表 60-6: 设计用于由 inetd 用的 TCP echo 服务器

```c
#include <syslog.h>
#include "tlpi_hdr.h"
#define BUF_SIZE 4096
int
main(int argc, char *argv[])
{
    char buf[BUF_SIZE];
    ssize_t numRead;
    while ((numRead = read(STDIN_FILENO, buf, BUF_SIZE)) > 0) {
        if (write(STDOUT_FILENO, buf, numRead) != numRead) {
            syslog(LOG_ERR, "write failed: %s", strerror(errno));
            exit(EXIT_FAILURE);
        }
    }
    if (numRead == -1) {
        syslog(LOG_ERR, "Error from read(): %s", strerror(errno));
        exit(EXIT_FAILURE);
    }
    exit(EXIT_SUCCESS);
}
```
