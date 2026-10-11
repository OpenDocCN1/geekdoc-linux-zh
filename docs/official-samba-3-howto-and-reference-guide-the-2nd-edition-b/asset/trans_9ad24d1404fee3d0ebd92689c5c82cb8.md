

# idmap uid (G)

默认值：无

idmap uid 参数指定了用于将 UNIX 用户映射到 NT 用户 SID 时分配的用户 ID 范围。该 ID 范围内不应存在现有的本地或 NIS 用户，否则可能会出现奇怪的冲突。

# include (G)

默认值：无

示例：include = /usr/local/samba/lib/admin.smb.conf

这允许你将一个配置文件包含在另一个配置文件中。该文件将被原样包含，就像就地输入一样。

它接受标准替换字符，但不包括 %u、%P 和 %S。

# inherit acls (S)

默认值：inherit acls = no

此参数可用于确保如果父目录上存在默认 ACL（访问控制列表），在创建子目录时始终会遵守这些默认 ACL。默认行为是使用创建目录时指定的模式。启用此选项会将模式设置为 0777，从而保证默认目录 ACL 能够向下传播。

# inherit owner (S)

默认值：inherit owner = no

新文件和目录的所有权通常由连接用户的*有效用户 ID*决定。此选项允许 Samba 管理员指定新文件和目录的所有权应由父目录的所有权来控制。

这种行为在实施“投递箱”时很有用，在这种情况下，用户可以创建和编辑文件但不能删除它们；同时也确保用户漫游配置文件目录中新创建的文件实际上由该用户所有。

# inherit permissions (S)

默认值：inherit permissions = no

新文件和目录的权限通常由*创建掩码*、*目录掩码*、*强制创建模式*和*强制目录模式*决定，但布尔型 inherit permissions 参数会覆盖这些设置。

新目录继承父目录的模式，包括 setgid 等位。新文件从父目录继承其读/写位。其执行位仍由*map archive*、*map hidden*和*map system*按常规方式决定。

# interfaces (G)

默认值：*192.168.3.10/255.255.255.0* 所有具有广播能力的活动接口（除 127.0.0.1 外）

示例：*interfaces = 这将配置三个网络接口，分别对应 eth0 设备以及 IP 地址 192.168.2.10 和 192.168.3.10。后两个接口的子网掩码将被设置为 255.255.255.0，即 eth0 192.168.2.10/24 和 192.168.3.10/255.255.255.0*

此选项允许你覆盖 Samba 用于浏览、名称注册和其他 NBT 流量的默认网络接口列表。默认情况下，Samba 会向内核查询所有活动接口的列表，并使用除 127.0.0.1 之外所有具有广播能力的接口。

该选项接受一个接口字符串列表。每个字符串可以采用以下任何形式：

- 网络接口名称（如 eth0）。这可以包含 shell 风格的通配符，因此 `eth*` 将匹配任何以 "eth" 子串开头的接口。
- IP 地址。在这种情况下，子网掩码是从内核获取的接口列表中确定的。
- IP/掩码对。
- 广播/掩码对。

“掩码”参数可以是位长度（例如 C 类网络为 24），也可以是点分十进制形式的全子网掩码。

上述“IP”参数可以是完整的点分十进制 IP 地址，也可以是通过操作系统的正常主机名解析机制查找的主机名。

# invalid users (S)

默认值：*invalid users = no*

示例：*invalid users = root fred admin @wheel*

这是一个不允许登录到此服务的用户列表。这是一个非常*多疑*的检查，旨在绝对确保不当设置不会破坏你的安全性。

以 `@` 开头的名称首先被解释为 NIS 网络组（如果系统支持 NIS），如果在 NIS 网络组数据库中未找到该名称，则解释为 UNIX 组。

以 `+` 开头的名称仅通过查找 UNIX 组数据库来解释。

以 `&` 开头的名称仅通过查找 NIS 网络组数据库来解释（这要求系统中 NIS 处于工作状态）。字符 `+` 和 `&` 可以按任意顺序用于名称的开头，因此值 `+&group` 意味着先查找 UNIX 组数据库，然后查找 NIS 网络组数据库；而值 `&+group` 意味着先查找 NIS 网络组数据库，然后查找 UNIX 组数据库（与 `@` 前缀相同）。

当前服务名称会替换 `%s`。这在 [homes] 段中很有用。

# keeplive (G)

默认值：*keeplive = 300*

示例：*keeplive = 600*

该参数的值（一个整数）代表**keeplive** 数据包之间的秒数。如果此参数为零，则不会发送 keeplive 数据包。如果发送了 keeplive 数据包，服务器可以判断客户端是否仍然存在并做出响应。

一般来说，如果套接字默认设置了 SO_KEEPLIVE 属性，则不需要 keeplive。（参见 *socket options*）。基本上，只有在你遇到困难时，才应使用此选项。

# kernel change notify (G)

默认值：*kernel change notify = yes*

此参数指定 Samba 是否应请求内核在目录中进行更改通知，以便 SMB 客户端在服务器上的数据发生变化时能够刷新。

只有当你的内核支持使用 F_NOTIFY fcntl 向用户程序发出更改通知时，才会使用此参数。

# kernel oplocks (G)

默认值：*kernel oplocks = yes*

对于支持基于内核的*oplocks*（当前仅 IRIX 和 Linux 2.1 内核支持）的 UNIX 系统，此参数允许启用或禁用它们的使用。

内核 oplocks 支持允许每当本地 UNIX 进程或 NFS 操作访问 smbd(8) 拥有 oplock 的文件时，破坏 Samba 的*oplocks*。这确保了 SMB/CHFS、NFS 和本地文件访问之间的完全数据一致性（这是一个*非常*酷的功能 :-）。

此参数默认为**开**，但在没有必要内核支持的系统中会转化为空操作。你通常永远不需要调整此参数。

# lanman auth (G)

默认值：*lanman auth = yes*

此参数决定 smbd(8) 是否尝试使用 LANMAN 密码哈希进行用户认证或允许密码更改。如果禁用，只有支持 NT 密码哈希的客户端（例如 Windows NT/2000 客户端、smbclient，但不包括 Windows 95/98 或 MS DOS 网络客户端）才能连接到 Samba 主机。

由于 LANMAN 加密响应对大小写不敏感且算法选择简单，因此很容易被破解。如果没有 Windows 95/98/ME 或 MS DOS 客户端，建议服务器禁用此选项。

与 **encrypt passwords** 选项不同，此参数无法改变客户端行为，LANMAN 响应仍会通过网络发送。请参阅 **client lanman auth** 以禁用 Samba 客户端（如 smbclient）的此功能。

如果此选项和 **ntlm auth** 均被禁用，则只允许 NTLMv2 登录。并非所有客户端都支持 NTLMv2，且大多数客户端需要特殊配置才能使用它。

# large readwrite (G)

默认值：*large readwrite = yes*

此参数决定 smbd(8) 是否支持随 Windows 2000 引入的新 64k 流式读写变体 SMB 请求。请注意，由于 Windows 2000 客户端重定向器的 bug，这需要 Samba 运行在 64 位操作系统上，例如 IRIX、Solaris 或 Linux 2.4 内核。在 Windows 2000 客户端上可提升 10% 的性能。默认为开。未像其他 Samba 代码路径那样经过充分测试。

# ldap admin dn (G)

默认值：*无默认值*

*ldap admin dn* 定义了 Samba 在检索用户帐户信息时用于联系 LDAP 服务器的可分辨名称（DN）。*ldap admin dn* 与存储在 **private/secrets.tdb** 文件中的 admin dn 密码一起使用。有关如何完成此操作的更多信息，请参阅 smbpasswd(8) 手册页。

# ldap delete dn (G)

默认值：*ldap delete dn = no*

此参数指定 ldapsam 中的删除操作是删除完整的条目，还是仅删除特定于 Samba 的属性。

# ldap group suffix (G)

默认值：*无默认值*

示例：*ldap group suffix = ou=Groups,dc=samba,dc=org*

此参数指定当组被添加到 LDAP 目录时使用的后缀。如果未设置此参数，则使用 *ldap suffix* 的值。

# ldap idmap suffix (G)

默认值：*无默认值*

示例：*ldap idmap suffix = ou=Idmap,dc=samba,dc=org*

此参数指定存储 idmap 映射时使用的后缀。如果未设置此参数，则使用 *ldap suffix* 的值。

# ldap machine suffix (G)

默认值：*无默认值*

它指定了机器应该被添加到 LDAP 树的哪个位置。

# ldap passwd sync (G)

默认值：*ldap passwd sync = no*

