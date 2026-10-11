
## 禁止缓存的文件

使用示例如下：

```samba
veto oplock files = ./.SEM/
```

## vfs 对象

此参数是 *vfs objects* 的同义词。

## vfs objects (S)

默认值：*无默认值*

示例：*vfs objects = extd.audit recycle*

此参数指定用于 Samba VFS I/O 操作的后端名称。默认情况下使用正常的磁盘 I/O 操作，但可以使用一个或多个 VFS 对象来重载这些操作。

## volume (S)

默认值：*volume = 共享名称*

这允许你为共享返回卷标。对于坚持使用特定卷标的带有安装程序的 CD-ROM 非常有用。

## wide links (S)

默认值：*wide links = yes*

此参数控制服务器是否允许跟随 UNIX 文件系统中的符号链接。指向服务器导出的目录树内部区域的链接始终被允许；此参数仅控制对导出目录树之外区域的访问。

请注意，设置此参数可能会因 Samba 执行链接检查所需的额外系统调用而对服务器性能产生负面影响。

## winbind cache time (G)

默认值：*winbind cache time = 300*

此参数指定 winbindd(8) 守护进程在再次查询 Windows NT 服务器之前缓存用户和组信息的秒数。

> **注意**
> 这不适用于身份验证请求，这些请求始终实时评估。

## winbind enum groups (G)

默认值：*winbind enum groups = yes*

在使用 winbindd(8) 的大型安装环境中，可能需要通过 **setgrent**、**getgrent()** 和 **endgrent()** 系统调用组来禁止组的枚举。如果 `winbind enum groups` 参数设置为 **no**，对 **getgrent()** 系统调用的调用将不返回任何数据。

> **警告**
> 关闭组枚举可能会导致某些程序行为异常。

## winbind enum users (G)

默认值：`winbind enum users = yes`

在使用 winbindd(8) 的大型安装环境中，可能需要通过 **setpwent()**、**getpwent()** 和 **endpwent()** 系统调用组来禁止用户的枚举。如果 `winbind enum users` 参数设置为 **no**，对 **getpwent** 系统调用的调用将不返回任何数据。

> **警告**
> 关闭用户枚举可能会导致某些程序行为异常。例如，finger 程序在搜索匹配的用户名时依赖于访问完整的用户列表。

## winbind nested groups (G)

默认值：`winbind nested groups = no`

如果设置为 **yes**，此参数将启用嵌套组支持。嵌套组也称为本地组或别名。它们的工作方式与其在 Windows 中的对应项类似：嵌套组在任何机器上本地定义（它们通过 SAM 在域控制器之间共享），并且可以包含来自任何受信任 SAM 的用户和全局组。要使用嵌套组，你需要运行 nss_winbind。

请注意，从 3.0.3 版本开始，这是一个新功能，因此请谨慎处理。

## winbind separator (G)

默认值：`winbind separator = \\+`

示例：`winbind separator = +`

此参数允许管理员定义在列出 **DOMAIN\\user** 形式用户名时使用的字符。此参数仅适用于使用 **pam_winbind.so** 和 **nss_winbind.so** 模块进行 UNIX 服务的情况。

请注意，将此参数设置为 + 可能会导致至少基于 glibc 的系统上的组成员身份出现问题，因为在 /etc/group 中，字符 + 被用作 NIS 的特殊字符。

## winbind trusted domains only (G)

默认值：*winbind trusted domains only* = *no*

此参数旨在允许属于 Samba 控制域的 Samba 服务器使用通过 NIS、rsync 或 LDAP 分发的 UNIX 账户作为 winbindd 用户在主机主域中的 uid。因此，用户 DOMAIN\user1 将被映射到 /etc/passwd 中的账户 user1，而不是为其分配新的 uid。

## winbind use default domain (G)

默认值：*winbind use default domain* = *no*

示例：*winbind use default domain* = *yes*

此参数指定 winbindd(8) 守护进程是否应处理用户名中不带域组件的用户。没有域组件的用户被视为 winbind 服务器自身域的一部分。虽然这不会让 Windows 用户受益，但它可以使 SSH、FTP 和电子邮件的功能更接近它们在本地 unix 系统中的工作方式。

## wins hook (G)

默认值：*无默认值*

当 Samba 作为 WINS 服务器运行时，此选项允许你为 WINS 数据库的所有更改调用外部程序。此选项的主要用途是允许动态更新外部名称解析数据库，例如动态 DNS。

wins hook 参数指定将要调用的脚本或可执行文件的名称，调用方式如下：

```
wins hook operation name nametype ttl IP_list
```

- 第一个参数是操作，它是 "add"、"delete" 或 "refresh" 之一。在大多数情况下，可以忽略该操作，因为其余参数提供了足够的信息。请注意，有时即使名称之前尚未添加，也可能调用 "refresh"，在这种情况下应将其视为添加操作。
- 第二个参数是 NetBIOS 名称。如果名称不是合法名称，则不会调用 wins hook。合法名称仅包含字母、数字、连字符、下划线和句点。
- 第三个参数是 NetBIOS 名称类型，表示为两位十六进制数。
- 第四个参数是该名称的 TTL（生存时间），以秒为单位。
- 第五个及后续参数是为该名称当前注册的 IP 地址。如果此列表为空，则应删除该名称。

Samba 源代码的 examples 目录中提供了一个调用 BIND 动态 DNS 更新程序 *nsupdate* 的示例脚本。

## wins proxy (G)

默认值：`wins proxy = no`

这是一个布尔值，控制 nmbd(8) 是否代表其他主机响应广播名称查询。你可能需要将此设置为 **yes** 以配合某些旧客户端使用。

## wins server (G)

默认值：`无默认值`

示例：`wins server = mary:192.9.200.1 fred:192.168.3.199 marv:192.168.2.61`

在此示例中，当查询特定名称时，将首先询问 192.19.200.1，如果它没有响应，则询问 192.168.2.61。如果其中任何一个都不知道该名称，则会查询 192.168.3.199。

示例：`wins server = 192.9.200.1 192.168.2.61`

这指定了 nmbd(8) 应向其注册的 WINS 服务器的 IP 地址（或用于优先级的 DNS 名称：IP 地址）。如果你的网络中有 WINS 服务器，则应将其设置为该 WINS 服务器的 IP 地址。

如果你的网络是多子网网络，你应该将此指向你的 WINS 服务器。

如果你希望在多个命名空间中工作，你可以为每个 wins 服务器分配一个“标签”。对于每个标签，仅查询一个（可用的）服务器以获取名称。标签应使用冒号与 IP 地址分隔。

> **注意**
> 如果你有多个子网并希望跨子网浏览正确工作，需要设置 Samba 指向 WINS 服务器。

参见第 9 章，“网络浏览”。

## wins support (G)

默认值：`wins support = no`

此布尔值控制 Samba 中的 nmbd(8) 进程是否作为 WINS 服务器运行。除非你有多个子网网络并希望特定的 **nmbd** 成为你的 WINS 服务器，否则你不应该将此设置为 **yes**。请注意，你绝不应该在网络中的多台机器上将此设置为 **yes**。

## workgroup (G)

默认值：`workgroup = WORKGROUP`

示例：`workgroup = MYGROUP`

这控制当客户端查询时你的服务器将显示为何工作组。请注意，此参数还控制与 `security = domain` 设置一起使用的域名。

## writable

此参数是 *writeable* 的同义词。

## writeable (S)

默认值：*无默认值*

*read only* 的反义词。

## write cache size (S)

默认值：*write cache size = 262144 表示每个文件 256k 的缓存大小*

示例：*write cache size = 262144 表示每个文件 256k 的缓存大小*

如果将此整数参数设置为非零值，Samba 将为每个加锁的文件创建内存缓存（它*不会*为非加锁文件这样做）。如果可能，客户端发出的所有未请求直接刷写至磁盘的写入操作都将存储在此缓存中。当传入的写入偏移量不适合缓存或当客户端关闭文件时，缓存将刷写到磁盘。如果数据存储在缓存中，对该文件的读取请求也由此缓存提供。

此缓存允许 Samba 将客户端写入合并为对 RAID 磁盘更高效的写入大小（即写入可以调整为 RAID 条带大小），并可以提高磁盘子系统是瓶颈但用户空间程序有可用内存的系统的性能。

该整数参数指定此缓存（每个加锁文件）的大小（以字节为单位）。

## write list (S)

默认值：*无默认值*

示例：*write list = admin, root, @staff*

这是一个被授予对服务读写访问权限的用户列表。如果连接的用户在此列表中，无论 *read only* 选项设置为何，他们都将获得写入权限。列表可以使用 `@group` 语法包含组名。

请注意，如果用户同时在读取列表和写入列表中，他们将获得写入权限。

在 Samba 3.0 中，此参数与 `security = share` 配合无效。这是有意设计的。

## write raw (G)

默认值：*write raw = yes*

此参数控制服务器在从客户端传输数据时是否支持 raw write SMB。你绝对不需要更改此参数。

## wtmp directory (G)

默认值：*无默认值*

