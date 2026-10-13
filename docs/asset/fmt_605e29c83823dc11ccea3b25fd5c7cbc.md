
```ini
[homes]
comment = Home Directories
browable = no
read only = no
invalid users = root bin daemon nobody sys ty disk mem kmem users
```

```ini
[tmp]
comment = Temporary File Space
path = /tmp
read only = No
valid users = root bin daemon nobody sys ty disk mem kmem users
```

这告诉 `smb.conf` 文件为此特定的配置设置进行自建：

```ini
server string = R&D of Open Network Architecture Samba Server
```
`t option "server string"` 指定你希望在 Windows 机器的打印管理器注释框中显示给用户看到的字符串，或者在 `"net view"` 命令下向 Windows 显示的 IPC 连接。

```ini
encrypt passwords = True
```
`t option "encrypt passwords"` 如果设置为 `"True"`，则指示 Samba 在与客户端协商时使用加密密码而非明文密码。嗅探程序（Sniffer）在密码加密时无法检测你的密码。出于安全考虑，必须将此选项设置为 `"True"`。

```ini
security = user
```
`t option "security"` 如果设置为 `"user"`，指定客户端必须先使用有效的用户名和密码登录，否则将拒绝连接。这意味着客户端的有效用户名和密码必须存在 Linux 服务器的 `"etc/passwd"` 文件和 Samba 服务器的 `"etc/smbpasswd"` 文件中，否则客户端的连接将失败。请参本文章中的“加固 samba”以获取关于 `"smbpasswd"` 的更多信息。

```ini
smbpasswd file = /etc/passwd
```
`t option "smbpasswd file"` 指定加密的 `"smbpasswd"` 文件路径。`"smbpasswd"` 是 Linux 系统 `"etc/passwd"` 文件的副本，包含了允许连接到 Samba 服务器的客户端有效用户名和密码。Samba 在请求连接时读取此文件 (`smbpasswd`)。

```ini
log file = /var/log/samba/log %m
```
`t option "log file"` 指定 Samba 日志文件的位置和名称。通过文件名扩展名 `"%m"`，允许你为 Samba 服务器上的每个用户或机器分离日志文件（例如 `log.machine1`）。

```ini
socket options = IPT_LOWDELAY TCP_NODELAY
```
`t option "socket options"` 指定你可以包含在 Samba 配置中的参数，用于调优和改进你的 Samba 服务器以获得最佳性能。默认情况下，我们选择用于本地网络的连接，并提高 Samba 服务器传输文件的性能。

### 浏览器与网络选项

`domain master = Yes`

选项 `"domain master"` 指定将 `"nmbd"`（Samba 守护进程）设置为其所在组的主浏览器（master browser）。此选项通常只需要在网络和组中的一个 Samba 服务器上设置为 `"Yes"`，对于所有其他 Samba 服务器均不设置。

`local master = Yes`

选项 `"local master"` 允许 `"nmbd"`（Samba 守护进程）成为本地主浏览器。类似于上面，此选项只需要在一个 Samba 服务器上设置为 `"Yes"`，对于子网内的所有其他 Samba 服务器。

`preferred mask = Yes`

选项 `"preferred master"` 指定 `"nmbd"`（Samba 守护进程）是该组的首选浏览器（preferred browser）。再次，这必须在网络中的一个 Samba 服务器上设置为 `"Yes"`。

`os level = 65`

选项 `"os level"` 通过其值指定 `"nmbd"`（Samba 守护进程）成为广播区域主浏览器的机会。数字 `65` 将优于任何 NT 服务器。如果你网络中有 NT 服务器，并希望你的 Linux 服务器成为广播区域的主浏览器，则必须将 `"os level"` 设置 `65`。此外，此选项只需要在一个 Linux 服务器上设置。

`dns proxy = No`

选项 `"dns proxy"` 如果设置为 `"Yes"`，指定作为 WINS 服务器的 `"nmbd"`（Samba 守护进程）发现未注册 Net BIOS 时，将 Net BIOS 词视为 DNS 名称并代表客户端向 DNS 服务器进行查询。由于我们没有配置 Samba 服务器作为 WINS 服务器，因此不需要将此选项设置为 `"Yes"`。此外，将此选项设置为 `"Yes"` 会降低 Samba 性能。

`name resolver order = hosts host`

选项 `"name resolve order"` 指定用于解析主机到 IP 地址的命名服务及其顺序。我们使用的参数会导致本地 `"hosts"` 文件首先被耗尽。

`interfaces only = True`

选项 `"interfaces only"` 如果设置为 `"True"`，允许你限制哪些接口提供 `"smb"` 请求。这是一个安全功能。配置选项 `"interfaces is 192.168.1.1"` 完成了此选项。

`interfaces = eth0 192.168.1.1`

选项 `"interfaces"` 允许你覆盖 Samba 用于浏览、名称注册和 NBT 流量的默认接口列表。默认情况下，Samba 会查询内核获取除 `(127.0.0.1)` 以外的所有广播能力的接口列表。通过此选项，Samba 将仅在 IP 地址 `192.168.1.1` 的 `eth0` 接口上监听。这是一个安全功能，并完成了上面的配置选项 `"bind interfaces only = True"`。

### 访问控制

`hosts deny = ALL`

选项 `"hosts deny"` 指定不允许访问 Samba 服务的主机列表，除非特定服务了自己的选项来覆盖此项。为了简单起见，我们默认拒绝所有主机，并在下面的 `"hosts ="` 选项中允许特定的主机。

# 服务器软件（文件共享网络服务） | 2

第 1 章

`hosts allow = 192.168.1.4 127.0.0.1`

`"hosts allow"`选项指定允许访问 Samba 服务器的主机。默认情况下，我们允许 IP 类为 `192.168.1.4` 以及本地主机 `127.0.0.1` 的主机访问 samba 服务器。注意，必须设置 localhost，否则你将收到某些错误信息。

`debug level = 1`

`"debug level"`选项允许在 `"smb.conf"` 文件中指定日志级别。如果你将调试级别设置得高于 `2`，性能可能会出现大幅下降。这是因为服务器在每次操作后都会刷新日志文件，这会非常消耗资源。

`create mask = 0644`

`"create mask"`选项根据 DOS 模式到 UNIX 权限的映射，指定并设置必要的权限。当此选项设置为 `0644` 时，从 Windows 系统到 Unix 系统的所有文件复制或创建默认权限都为 `0644`。

`directory mask = 0755`

`"directory mask"`选项指定并设置八进制模式，用于在创建 UNIX 目录时将 DOS 模式转换为 UNIX 模式。当此选项设置为 `0755` 时，从 Windows 系统到 Unix 系统的所有目录复制或创建默认权限都为 `0755`。

`level2 allows = True`

`"level2 allows"`选项如果设置为 `"True"`，将提高许多不常用文件（如 EXE 文件）的访问性能。

`read raw = no`

`"read raw"`选项控制服务器在向客户端传输数据时是否支持读取 SMB 请求。注意，`"read raw"` 操作不使用内存映射。然后你可能会发现，通过使用 `read raw = no` 禁用 `"read raw"`正如我们做的那样），内存映射会更有效。

`write cache size = 262144`

`"write cache size"`选项允许 Samba 在系统成为瓶颈的系统中提高性能。该选项的大小以字节为单位，`262144` 代表每个文件 `256k` 的缓存大小。

### 共享定义

```ini
[tmp]
```

`comment = / 临时文件空间`

`"comment"`选项允许你指定当客户端查询服务器时显示在共享旁边的注释。

`path = /tmp`

`"path"`选项指定用户获得访问的目录。在我们的示例中，是 Linux 服务器的 `"tmp"` 目录。

`read only = No`

`"read only"`选项指定是否允许用户只读文件。在我们的示例中，这是 Linux 服务器 `"tmp"` 目录的配置，用户可以执行比读取文件更多的操作。

`valid users = admin`
