
# 日期处理的一个常见问题是将不同类型的日期和字符串转换为适当的 `datetime` 对象

`datetime` 模块提供的唯一解析函数是 `strptime()`。然而，为了使用它，必须提供精确的格式字符串。例如，解析日期 `s="Aug 23, 2008"`。

## errno

下表将错误码映射到它们的名称。这有助于调试系统错误。

| 错误代码 | 描述 |
| --- | --- |
| EACCES | 拒绝访问。 |
| EAGAIN | 请重试。 |
| EADAVAIL | 地址不可用。 |
| EBADF | 错误的文件描述符。 |
| EBIG | 文件过大 |
| EBUSY | 设备或资源忙 |
| ECHILD | 无子进程 |
| EDEADLK | 死锁。 |
| EDEV | 无此类设备 |
| E2ANGE | 参数超出范围 |
| EDOM | 参数超出定义域 |
| EEXIST | 文件已存在 |
| EFAULT | 损坏的地址 |
| EFSIG | 文件过大 |
| EHOSTDOWN | 主机宕机 |
| EHOSTREACH | 无法到达主机 |
| EILSEQ | 非法序列 |
| EINPROGRESS | 操作正在进行中 |
| EINTR | 系统调用被中断 |
| EINVAL | 无效参数 |
| EIO | I/O 错误 |
| EPIPE | 传输端点已连接 |
| EISDIR | 是目录 |
| ELOOP | 符号链接过多 |
| EMFILE | 打开的文件过多 |
| EMLINK | 链接过多 |
| ENOMEM | 内存不足 |
| ENOPPROTO | 协议不可用 |
| ENOSPC | 设备上没有剩余空间 |
| ENOSYS | 函数未实现 |
| ENOTCONN | 传输端点未连接 |
| ENOTDIR | 不是目录 |
| ENOTEMPTY | 目录不为空 |
| ENOTSOCK | 非套接字上的操作 |
| ENOTTY | 不是终端 |
| ENXIO | 无此类设备或地址 |
| EOPNOTSUPP | 传输端点不支持的操作 |
| EPERM | 操作不允许 |
| EFNOSUPPORT | 不支持的协议族 |
| EPIPE | 管道断开 |
| EPROTOSUPPORT | 协议不支持 |
| EPROTOTYPE | 套接字协议类型错误 |
| ERANGE | 数学结果不可表示 |
| EOTE | 对象是远程 |
| EROFS | 只读文件系统 |
| ESHUTDOWN | 无法发送传输端关闭 |
| ESOCKETNOSUP | 套接字类型不支持 |
| ESPIPE | 非法寻址 |

## Windows 错误代码

下表中的错误代码仅在 Windows 上可用。

| 错误代码 | 描述 |
| --- | --- |
| WSAACCES | 权限拒绝。 |
| WSAADDRINUSE | 地址已占用。 |
| WSAADDROTOAVAIL | 无法分配请求的地址。 |
| WSAEPNGOSUPPORT | 协议族不支持地址族。 |
| WSAELREADY | 操作已进行中。 |
| WSAEBADF | 无效的文件句柄。 |
| WSANABORTED | 软件导致连接中断。 |
| WSAECONREFUSED | 拒绝连接。 |
| WSAECONRESET | 连接被对端重置。 |
| WSAEDESTARDDREQ | 需要目标地址。 |
| WSADISCONN | 远程关闭。 |
| WSAEDQUOT | 磁盘配额超出。 |
| WSAFAULT | 坏地址。 |
| WSAHOSTDOWN | 主机宕机。 |
| WSAHOSTUNREACH | 无法到达主机。 |
| WSAINPROGRESS | 操作正在进行中。 |
| WSAINTER | 系统调用被中断。 |
| WSAINVAL | 无效参数。 |
| WSAEISCONN | 套接字已连接。 |
| WSAELOOP | 无法翻译名称。 |
| WSAEMFILE | 打开的文件过多。 |
| WSAEMSSIZE | 消息过长。 |
| WSAANOMETOOL | 名称过长。 |
| WSAENETDOWN | 网络已关闭。 |
| WSAENETRESET | 网络重置时断开连接。 |
| WSAENETREACH | 网络不可达。 |
| WSAENOBUFS | 无可用缓冲区空间。 |
| WSAENOPTOOPT | 协议选项无效。 |
| WSAECONTCONN | 套接字未连接。 |
| WSAENEMPTY | 无法删除非空目录。 |
| WSAOTSOCK | 对非套接字进行套接字操作。 |
| WSAENOPTSSUP | 不支持的操作。 |
| WSAEPNGOSUPPORT | 协议不支持。 |
| WSAPROCLIM | 进程过多。 |
| WSAPROTOSSUPPORT | 不支持协议。 |
| WSAPROTOTYPE | 套接字协议类型错误。 |
| WSAEREMOTE | 本地项不可用。 |
| WSAESHUTDOWN | 套接字关闭后无法发送。 |
| WSASOCKETNOSUP | 不支持套接字类型。 |
| WSAESTALE | 文件句柄失效。 |
| WSAETIMEOUT | 连接超时。 |

## fcntl 347

| 错误代码 | 描述 |
| --- | --- |
| WSAETOMANYREFS | 对内核对象的引用过多。 |
| WSAUSERS | 配额超出。 |
| WSAWOULDBLOCK | 资源临时不可用。 |
| WSANOTINITISED | 未执行成功的 WSA 启动。 |
| WSASYSNOTREAD | 网络子系统不可用。 |
| WSAVERNOTSUPPORTED | Winsock.dll 版本超出范围。 |

## fcntl

`fcntl` 模块对 UNIX 文件描述符执行文件和 I/O 控制。可以使用文件或套接字对象的 `fileno()` 方法获取文件描述符。`fcntl(fd, cmd, [arg])`

在打开的文件描述符 `fd` 上执行命令 `cmd`。`cmd` 是一个整数命令。`arg` 是一个可选参数，可以是整数或字符串。如果 *arg* 以整数传递，则该函数的返回值为整数。如果 *arg* 是字符串，则它被解释为二进制字符串，且返回值为缓冲区内容转换回字符串对象。在这种情况下，所提供的参数和返回值应小于 1,024 字节，以避免可能的数据损坏。以下是常用命令：

| 命令 | 描述 |
| --- | --- |
| F_DUPFD | 复制文件描述符。`arg` 是新文件描述符可以假设的最小数字。类似于 `os.dup()` 系统调用。 |
| F_SETFD | 将 *close-on-exec*（执行时关闭）标记设置为 `arg` (0 或 1)。如果设置，则在执行 `exec()` 系统调用时关闭文件。 |
| F_GETFD | 返回 *close-on-exec*（执行时关闭）标记。 |
| F_SETFL | 将标记设置为 `arg`，以下内容的按位“或”结果：<br> _NODELAY--非阻塞 I/O (System V) <br> _APPEND--追加模式 (System V) <br> _SYNC--同步写 (System V) <br> FNDELAY--非阻塞 I/O (BSD) <br> FAPPEND--追加模式 (BSD) <br> FASYNC--当 I/O 可用时向进程组发送 SIGIO (BSD) |
| F_GETFL | 获取由 *F_SETFL* 设置的状态标记。 |
| F_GETOWN | 获取进程 ID 或组 ID 以接收 SIGIO 和 SIGURG 信号 (BSD)。 |
