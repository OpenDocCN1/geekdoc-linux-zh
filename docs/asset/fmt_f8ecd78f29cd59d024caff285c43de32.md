
在 UNIX 与 DOS/Windows 之间转换文件属性时，另一个问题涉及 CRLF/LF 转换。不幸的是，没有可靠的方法来确定哪些文件需要转换，哪些不需要。您不能依赖 `TXT` 或 `DOC` 等文件名扩展名。Samba 的做法是不会自动修改文件，以确保文件不会因错误的转换而被意外损坏。请注意，像 Linux 这样的某些操作系统可能会根据文件类型自动转换 CD-ROM 文件。使用 `conv=binary` 挂载选项可禁用 Samba 管理的 CDROM 共享的转换。

Jim Barry 编写了一个名为 `fixcrlf` 的出色 Windows 拖放式 CRLF/LF 转换器，可根据需要转换文件。要转换文件，只需将文件从 Windows 资源管理器拖到 `fixcrlf` 图标上。您可以从 Samba 归档站点之一下载 `fixcrlf` 的副本：`ftp://samba.org/pub/samba/contributed/fixcrlf.zip`

## 锁定

在分布式环境中共享文件始终涉及用于序列化和更新通知的锁定机制。Samba 支持两种基本类型，DOS/Windows 共享模式锁定和机会锁（`oplocks`）。由于 UNIX 中没有共享模式操作的通用对应物，共享模式锁定使用共享内存（快速）或文件锁（慢）实现。Samba 实现 `DENY_DOS`、`DENY_ALL`、`DENY_READ`、`DENY_WRITE`、`DENY_NONE` 和 `DENY_FCB` 锁定请求（表 11.5）。

```
share modes = <yes, no>
```

### 表 11.5 Samba 共享模式

| `DENY_DOS` | DOS 兼容模式。允许同一客户端进行额外的打开。 |

| `DENY_FCB` | 文件兼容模式。`DENY_DOS` 打开然后将打开设置为读写。如果第一个打开客户端正在写入，则不允许其他客户端读取。如果第一个客户端为只读，则允许额外的客户端读取。 |

| `DENY_ALL` | 拒绝所有其他打开请求。 |

| `DENY_READ` | 允许只写打开。 |

| `DENY_WRITE` | 允许只读打开。 |

| `DENY_NONE` | 允许额外的打开请求。 |

机会锁定是一种锁定方法，允许 Windows 客户端积极地在本地客户端上缓存文件数据块。LAN Manager 或 Windows 客户端可能会请求三种类型的 `oplocks`。第一种称为独占 `oplock`。这允许客户端获得对文件的独占访问。第二种类型是批处理 `oplock`。使用批处理 `oplock` 锁定的文件允许客户端在客户端上的本地应用程序可能已关闭文件时仍将文件保持在服务器上打开。第三种 `oplock` 类型是二级 `oplock`，允许多个客户端在没有写入者的情况下读取文件。启用 Samba `oplock` 支持（默认）可实现高达 30% 的文件 IO 性能提升。有关锁定参数的详细信息，请参阅 `smb.conf(5)` man 手册。

```
oplocks=<yes, no>
```

Samba 2.0.5 版引入了对二级 `oplocks` 的支持。`level2 oplocks` 允许读写客户端在其他客户端请求访问文件时将其 `oplock` 降级为只读。

```
level2 oplocks = <yes, no>
```

对于您希望允许多个客户端对同一文件请求 `oplocks` 的特定情况，您可以通过启用 `fake oplocks` 参数来指示 Samba 允许多个 `oplock` 请求。请记住，如果此选项在可写共享上被允许，你可能导致数据损坏。允许在只读共享上进行多个 `oplock` 请求可因本地客户端文件缓存而带来显著的性能提升。

```
fake oplocks = <yes, no>
```

如果数据通过非 Samba 控制的接口访问，可能会出现问题。持有 `oplock` 的 Samba 客户端无法感知非 Samba 应用程序的访问。可以通过将一个或多个文件匹配模式指定为 `veto oplocks files` 参数的值来为特定文件关闭 `oplocks` 支持。

```
veto oplocks files = /*.mbx/
```

你还可以通过修改系统注册表在 Windows 9x 和 Windows NT 中关闭 `oplock` 支持。这不是推荐的做法，因为禁用所有 `oplock` 支持可能会对某些 Windows 应用程序产生不利影响。如果你选择在客户端禁用 `oplocks`，请参考 Samba 发行版文档 `File-Caching.txt`。Samba 发行版中还提供了 Windows 9x 和 Windows NT 的注册表更新文件，`Win9x-CacheHandling.reg` 和 `NT4-Locking.reg`。

另一种处理未知客户端访问问题的方法由某些 UNIX 实现支持的内核级 `oplocks` 提供便利。当像 NFS 这样的其他进程触及已被 Samba `oplock` 的文件时，锁会根据指定的 `oplock` 选项被破坏或降级。

```
kernel oplocks = <yes, no>
```

文件内的字节范围锁定可以通过 `ole locking compatibility` 参数启用/禁用。Samba 通过调用 `fcntl()` 系统调用来实现字节范围锁定。`fcntl()` 使用 32 位有符号整数跟踪位置范围。Windows OLE2 客户端使用范围值的第 32 位作为信号量，这可能导致某些 UNIX 和 NFS 系统的范围值问题。

```
ole locking compatibility = <yes, no>
```

## 符号链接

DOS 和 Windows 客户端不支持类似 UNIX 符号链接的跨文件链接。Samba 通过启用 `follow symlinks` 参数允许客户端跟随 UNIX 符号链接。通过启用 `wide links` 参数，客户端可以访问位于共享目录树之外的符号链接目标。

```
follow symlinks = <yes, no>
```

```
wide links = <yes, no>
```

## 限制负载

当共享对于现有服务器资源来说过于流行时，你可以使用 `max connections` 参数限制并发连接数。此功能对于因许可限制而检查并发访问也可能有用：

```
max connections = <integer>
```

## 摘要

```
[share name]
comment = <text description>
path = <directory path>
```

- 文件共享的最小定义将包括用方括号括起来的共享名称和目录 `path` 参数。描述共享的 `comment` 参数也很理想。
- 特殊的 `[homes]` 文件共享部分允许用户从 SMB 客户端访问其 UNIX `$HOME` 目录。
- 访问控制参数可以应用于文件共享，按主机、用户和权限限制访问。
- `Non-browseable` 和隐藏文件参数会移除共享或文件的可见性，但如果客户端已知共享或文件名，则不会限制访问。
- 文件访问模式和掩码参数必须遵守底层 UNIX 权限。
- DOS/Windows `archive`、`system` 和 `hidden` 属性可以通过 `map archive`、`map system` 和 `map hidden` 参数映射到 UNIX `owner`、`group` 和 `world` 执行位。
- Samba 文件名改写用于将区分大小写的 UNIX 长文件名转换为 DOS 8.3 格式。转换映射可以按文件共享进行定制。
- 自动 CRLF/LF 文件文本转换不受支持，因为 Samba 无法准确确定何时应转换文件。可提供 CRLF/LF 工具以允许客户端根据需要转换文件：`ftp://samba.org/pub/samba/contributed/fixcrlf.zip`
- Samba 支持两种基本锁定机制。DOS `share mode` 锁定和 `windows opportunistic locking (oplocks)`。
- Samba 通过启用 `follow symlinks` 参数提供对 UNIX 符号链接文件的访问。位于共享范围之外的链接目标可以使用 `wide links` 参数使其可访问。

# 第 12 章：打印共享

## 概述

Samba 就像一把真正的瑞士军刀，当谈到打印子系统接口时。打印是一个存在于各种 UNIX 实现之间存在实质性差异的领域：守护进程、配置文件和命令。Samba 在支持大多数流行的 UNIX 打印子系统方面做得非常出色。一旦 Samba 知道操作系统类型，启用 Windows 和 LAN Manager 到本地 UNIX 打印机的打印就像一阵微风（或至少是一阵小旋风）。

## 全局打印参数

首先，当你将 Samba 配置为打印服务器时，识别操作系统类型。这让 Samba 了解将与打印排队系统互操作时使用的命令和配置文件的性质。操作系统类型由全局 `printing` 参数标识。支持的操作系统包括 `AIX`、`BSD`、`HPUX`、`LPRNG`、`PLP`、`QNX`、`SOFTQ` 和 `SYSV`。

```
printing = <os type>
```
