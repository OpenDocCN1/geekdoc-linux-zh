
此变量是启用 SSL 的 Samba 的部分。只有当你的系统上编译了 SSL 库且在配置时提供了 `--with-ssl` 配置选项时，它才可用。

注意，由于出口控制原因，此代码在任何当前的 Samba 二进制版本中**没有**默认启用。

此变量定义了是否为了与其他 SSL 实现保持兼容。这可能是不需要的，因为目前没有其他 SSL 实现的客户端。

```
默认：ssl compatibility = no
```

### * ssl hosts (G)

查看 "ssl hosts"。

### * ssl hosts resign (G)

变量是启用 SSL 的 Samba 的部分。只有当你的系统上编译了 SSL 库且在配置时提供了 `--with-ssl` 配置选项时，它才可用。

注意，由于出口控制原因，此代码在任何当前的 Samba 二进制版本中**没有**默认启用。

这两个变量定义了 samba 是否进入 SSL 模式。如果定义了其中一个，samba 将仅允许连接。"ssl hosts" 变量（通过 IP 地址、IP 地址范围、组或名称）将强制进入 SSL 模式。这两个变量的语法与 "hosts allow" 和 "hosts deny" 变量相同，不同之处在于是否使用 SSL。"allow hosts" 参数示例要求来自局域网所有主机（即 192.168.*）的连接。

```
默认：ssl hosts = "" ssl hosts resign = ""
示例：ssl hosts resign = 192.168.*
```

### * ssl requirecert (G)

此变量是启用 SSL 的 Samba 的部分。只有当你的系统上编译了 SSL 库且在配置时提供了 `--with-ssl` 配置选项时，它才可用。

注意，由于出口控制原因，此代码在任何当前的 Samba 二进制版本中**没有**默认启用。

如果此变量设置为 "yes"，服务器将不允许来自没有有效证书的客户端。"ssl CA certdir" 或 "ssl CA certFile" 中的目录/文件将用于查找签客户端证书的 CA。如果无法验证证书，连接将终止。如果此变量设置为 "no"，则客户端不需要证书。与 Web 应用不同，我们*应该*要求客户端证书。在客户端数据敏感的环境中，服务器必须证明自己是可信的；在服务器数据敏感的环境中，客户端必须证明自己是可信的。

**默认：**`ssl requirecert = no`

### * ssl requirecert (G)

此变量是启用 SSL 的 Samba 的部分。只有当你的系统上编译了 SSL 库且在配置时提供了 `--with-ssl` 配置选项时，它才可用。

注意，由于出口控制原因，此代码在任何当前的 Samba 二进制版本中**没有**默认启用。

如果此变量设置为 "yes"，smbient 将向服务器请求证书。与服务器的 "ssl requirecert" 相同。

**默认：**`ssl requirecert = no`

### * ssl server cert (G)

此变量是启用 SSL 的 Samba 的部分。只有当你的系统上编译了 SSL 库且在配置时提供了 `--with-ssl` 配置选项时，它才可用。

注意，由于出口控制原因，此代码在任何当前的 Samba 二进制版本中**没有**默认启用。

这是包含服务器证书的文件。服务器必须有一个证书。该文件可能包含服务器的私钥。有关如何创建证书和私钥请见后文。

**默认：**`ssl server cert = ""`

### * ssl server key (G)

此变量是启用 SSL 的 Samba 的部分。只有当你的系统上编译了 SSL 库且在配置时提供了 `--with-ssl` 配置选项时，它才可用。

注意，由于出口控制原因，此代码在任何当前的 Samba 二进制版本中**没有**默认启用。

此文件包含服务器的私钥。如果未定义此变量，则会在证书文件中查找密钥（它可能附加在证书后面）。服务器*必须*有一个私钥，且证书*必须*匹配此私钥。

**默认：**`ssl server key = ""`

### * ssl version (G)

此变量是启用 SSL 的 Samba 的部分。只有当你的系统上编译了 SSL 库且在配置时提供了 `--with-ssl` 配置选项时，它才可用。

注意，由于出口控制原因，此代码在任何当前的 Samba 二进制版本中**没有**默认启用。

# 附录 C: Samba 手页

此枚举变量定义了将使用的 SSL 协议版本。"ssl12or3" 允许 SSL v2 或 v3 的动态协商，“ssl12" 产生 SSL v2，“ssl13" 产生 SSL v3，而 "tls1" 产生 TLS v1。TLS（传输层安全）是 SSL 的（建议的？）新标准。

默认值：`ssl version = "ssl12or3"`

### * stat cache (G)

此参数决定 `smbd` 是否将使用缓存来加速不区分大小写的名称映射。你通常不需要更改此参数。

默认值：`stat cache = yes`

### * stat cache size (G)

此参数决定 stat 缓存中条目的数量。你通常不需要更改此参数。

默认值：`stat cache size = 50`

### * status (G)

此项允许禁用对 `smbtatus` 可以读取的状态文件的连接锁定。如果禁用了此项，`smbtatus` 将无法判断哪些连接是活跃的。你通常不需要更改此参数。

默认值：`status = yes`

### * strict locking (S)

这是一个控制服务器上文件锁处理的布尔值。当此设置为 "yes" 时，服务器将检查每次读写访问是否存在文件锁，如果存在锁则拒绝访问。这在某些系统上可能会很慢。

当 `strict locking` 为 "no" 时，服务器仅在客户端请求锁时才进行文件锁定。

良好的客户端在重要时总是会请求锁，在大多数情况下，“strict locking = no" 是优的。

默认值：`strict locking = no`

示例：`strict locking = yes`

### * strict sync (S)

许多 Windows 应用程序（包括 Windows 98 资源管理器外壳）似乎通过与磁盘同步（sync）将缓冲区内容刷到磁盘。在 UNIX 下，sync 调用会强制进程挂起，直到内核确保内核缓冲区中所有待处理的数据已安全地存储在稳定性存储设备上。这非常慢，应该极少执行。将此参数设置为 "no"（默认值）意味着 `smbd` 忽略 Windows 的 sync 请求。只有在运行 Samba 的操作系统本身崩溃时，才存在丢失数据的可能性，因此此默认值危险很小。此外，它修复了人们报告的关于新 Windows98 资源管理器外壳文件复制的许多性能问题。

# smb.conf (5)

另见“sync always”参数。

```
默认值：strict sync = no
示例：strict sync = yes
```

### - - strip dot (G)

这是一个布尔值，控制是否剥离 UNIX 文件名末尾的点。这有助于那些以单个点结尾的文件名的 CD-ROM。

默认值：`strip dot = no`

示例：`strip dot = yes`

### - - sync always (S)

这是一个布尔参数，控制在写入调用返回之前写入是否总是被写入存储器。如果为 false，则服务器将根据客户端每次写入调用的请求（客户端可以设置一个位来指示特定的写入应该是同步的）。如果为 true，则每次写入后都会跟随一个 `fsync()` 以确保数据写入磁盘。必须将“strict sync”参数设置为“yes”，此参数才能起作用。

另见“strict sync”参数。

默认值：`sync always = no`

示例：`sync always = yes`

### - - syslog (G)

此参数将 Samba 调试消息映射到系统 syslog 日志级别。Samba 调试级别 0 映射到 LOG_ERR，级别 1 映射到 LOG_WARNING，级别 2 映射到 LOG_DEBUG，级别 3 映射到 LOG_INFO。该参数设置了映射的阈值，所有高于此阈值的 Samba 调试消息都会映射到 syslog LOG_DEBUG 消息。

默认值：`syslog = 1`

### - - syslog only (G)

如果设置了此参数，Samba 调试消息将仅记录在系统中，而不是调试日志文件中。

默认值：`syslog only = no`

### - - time offset (G)

此参数是以分钟为单位的设置，用于在普通 GMT 到本地时间的转换上。如果你正在为许多夏令时间处理错误的 PC 提供服务，这非常有用。

默认值：`time offset = 0`

示例：`time offset = 0`

# 附录 C: Samba 手页

### - • time server (G)

此参数决定 `nmbd` 是否将自己作为时间服务器向 Windows 客户端广播。默认值为 False。

```
默认值：time server = False
```

```
示例：time server = True
```
