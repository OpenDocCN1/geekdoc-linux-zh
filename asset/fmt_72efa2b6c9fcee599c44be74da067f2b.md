
这是一个文件列表或目录列表，这些文件或目录不可见但可访问。DOS "hidden" 属性将应用于匹配的任何文件或目录。
列表中的每个条目必须由 ` / ` 分隔，这允许条目中包含空格。可以使用 `*` 和 `?` 来指定多个文件或目录，如 DOS 通配符那样。
每个条目必须是 Unix 路径，而不是 DOS 路径，并且不能包含 Unix 目录分隔符 `/`。
请注意，*区分大小写*选项在隐藏文件时是适用的。
设置此参数会影响 Samba 的性能，因为它将被迫在扫描时检查所有文件和目录是否匹配。
上面示例基于 Thursby¹ 提供的 Macintosh SMB 客户端 (DAVE) 为内部使用创建的文件，并且仍然隐藏所有以点开头的文件。
使用此参数的示例是：
```
hide_files = ./* /DesktopFolderDB/TrashFor%m/resource.frk/
```
### hide special files (S)
**默认值：** `hide_special_files = no`
此参数防止客户端在目录列表中看到特殊文件，如套接字、设备和 fifo。
### hide unreadable (S)
**默认值：** `hide_unreadable = no`
此参数防止客户端看到无法读取的文件的存在。默认为关闭。
### hide unwritable files (S)
**默认值：** `hide_unwritable_files = no`
此参数防止客户端看到无法写入的文件的存在。默认为关闭。注意，不可写的目录将照常显示。
### homedir map (G)
**默认值：** *无默认值*
**示例：** `homedir_map = %md.%homedir`
如果 *nis homedir* 为 yes，并且 `smbd(8)` 也充当 Win95/98 *登录服务器*，则此参数指定从中提取用户主目录服务器的 NIS（或 YP）映射。目前，仅支持 Sun auto.home 映射格式。映射的形式为：
```
username server:/some/file/system
```
程序将从第一个空格之前提取服务器名称。应该有一个更好的解析系统，能够处理不同的映射格式，以及 Amd（另一种自动挂载器）映射。
> **注意**
>
> 要使此选项正常工作，系统上需要有一个可用的 NIS 客户端。
### host msdfs (G)
**默认值：** `host msdfs = no`
如果设置为 yes，Samba 将作为 Dfs 服务器，允许支持 Dfs 的客户端浏览托管在服务器上的 Dfs 树。
另请参见 *msdfs root* 共享级别参数。有关在 Samba 上设置 Dfs 树的更多信息，请参阅第 19 章“托管 Microsoft 分布式文件系统树”。
### hostname lookups (G)
**默认值：** `hostname lookups = no`
**示例：** `hostname lookups = yes`
指定 samba 是否应使用（代价高昂的）主机名查找，还是使用 IP 地址。目前使用主机名查找的一个示例位置是在检查 *hosts deny* 和 *hosts allow* 时。
**allow hosts**：此参数是 *hosts allow* 的同义词。
### hosts allow (S)
**默认值：** `hosts allow = 150.203.5.*, myhost.myenet.edu.au` *nont*（即，允许所有主机访问）
**示例：** `hosts allow = 150.203.5.*, myhost.myenet.edu.au`
此参数的同义词是 *allow hosts*。
此参数是一组由逗号、空格或制表符分隔的主机，这些主机被允许访问服务。
如果在 *[global]* 部分中指定，它将适用于所有服务，无论单个服务是否有不同的设置。
你可以通过名称或 IP 号指定主机。例如，你可以使用类似 *allow hosts = 150.203.5.* 的内容将访问限制到 C 类子网上的所有主机。列表的完整语法在手册页 *hosts_access(5)* 中描述。请注意，你的系统上可能没有此手册页，因此这里也会给出简要描述。
请注意，本地主机地址 127.0.0.1 始终允许访问，除非被 *hosts deny* 选项明确拒绝。
如果系统支持 netgroups，你还可以通过网络/子网掩码对和 netgroup 名称来指定主机。也可以使用 *EXCEPT* 关键字来限制通配符列表。以下示例可能提供一些帮助：
示例 1：允许 150.203.* 中的所有 IP，除了一个
```
hosts allow = 150.203.* EXCEPT 150.203.6.66
```
示例 2：允许匹配给定网络/子网掩码的主机
```
hosts allow = 150.203.15.0/255.255.255.0
```
示例 3：允许几个主机
```
hosts allow = lapland, arvoskar
```
示例 4：只允许 NIS netgroup "foonet" 中的主机，但拒绝某个特定主机的访问
```
hosts allow = @foonet
hosts deny = pirate
```
> **注意**
>
> 请注意，访问仍然需要适当的用户级密码。
参见 `testparm(1)` 以测试你的主机访问是否按预期工作。
**deny hosts**：此参数是 *hosts deny* 的同义词。
### hosts deny (S)
**默认值：** `hosts deny = none`（即，没有明确排除的主机）
**示例：** `hosts deny = 150.203.4.badhost.mynet.edu.au`
*hosts allow* 的反义 - 此处列出的主机**不被**允许访问服务，除非特定服务有自己的列表来覆盖此列表。当列表冲突时，*allow* 列表优先。
### hosts equiv (G)
**默认值：** `hosts equiv = /etc/hosts.equiv`
**示例：** `hosts equiv = /etc/hosts.equiv`
如果此全局参数是非空字符串，它指定了一个文件名，用于读取允许在不指定密码的情况下访问的主机名和用户名。
不要将此与 *hosts allow* 混淆，后者关于主机对服务的访问，对客户服务更实用。*hosts equiv* 对于不向 Samba 提供密码的 NT 客户端可能很有用。
> **注意**
>
> 使用 **hosts equiv** 可能是一个重大的安全漏洞。这是因为你信任 PC 提供正确的用户名。让 PC 提供错误的用户名非常容易。我建议仅在你真的知道自己在做什么时，或者可能在家庭网络中（你信任你的配偶和孩子）时才使用 **hosts equiv** 选项。而且仅当你*真的*信任他们时 :-)
### idmap backend (G)
**默认值：** *无默认值*
- **示例：** `idmap backend = ldap:ldap://ldapSlave.example.com`
- **示例：** `idmap backend = idmap.rid:DOMAIN=1000-10000000`
`idmap backend` 参数的目的是允许 idmap 不使用本地 idmap tdb 文件来获取 SID 到 UID / GID 的映射，而是从通用的 LDAP 后端获取。这样，所有域成员和控制器将具有相同的 UID 和 GID 到 SID 映射。这避免了 UID / GID 在不通过 SMB/CIFS 以外的协议（即：NFS）共享信息的 UNIX / Linux 系统之间不一致的风险。
使用 `idmap.rid` 插件可以实现另一种 SID 到 UID / GID 映射方法。此插件使用账户 RID 通过将从指定基准值添加到 RID 中来推导 UID 和 GID。此实用程序必须指定参数“allow trusted domains = No”，因为它不兼容于多域环境。还必须指定 `idmap uid` 和 `idmap gid` 范围。
**winbind gid**：此参数是 *idmap gid* 的同义词。
### idmap gid (G)
**默认值：** *无默认值*
- **示例：** `idmap gid = 10000-20000`
`idmap gid` 参数指定了一组用于将 UNIX 组映射到 NT 组 SID 的组 ID 范围。该组 ID 范围中不应包含任何现有的本地或 NIS 组，否则可能会发生奇怪的冲突。
`idmap gid` 范围的可用性对于所有组映射的正确运行都是必不可少的。
**winbind uid**：此参数是 *idmap uid* 的同义词。
### idmap uid (G)
**默认值：** *无默认值*
- **示例：** `idmap uid = 10000-20000`
# idmap uid (G)
默认值：无
