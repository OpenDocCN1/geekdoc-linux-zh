
```
cat /etc/exports
/home/public 172.16.192.150(rw, sync)
/home/zach 172.16.192.150(rw, sync)
```

指定的目录位于本地服务器上。对于以导出目录为根的目录层次结构，每个情况都隐式授予了权限。你可以指定 IP 地址或主机名，并且可以在一行中指定多个客户端。默认情况下，目录层次结构是以只读模式导出的。

## 通用选项

本节的左列列出了默认导出，随后是括在括号中的非默认选项。更多信息请参考 `exports` 页面。

`auth_nml (no_auth_nml)` 或 `secure_locks (secure_locks)`

设置 `auth_nlm` 或 `secure_locks` 选项（这两个选项相同）会导致服务器要求对锁请求进行认证。当你发现只有任何人都可以读取的文件才能锁定时，对较旧的客户端使用 `no_auth_nml`。默认是 `auth_nlm`。

`mountpoint=[path]` 仅当目录已挂载时允许导出该目录。此选项防止了没有目录层次结构的挂载点被导出，并防止底层挂载点被导出。此外 mp

`nohide (hide)` 当服务器导出两个目录层次结构且其中一个挂载在另一个上时，`hide` 选项要求客户端必须显式挂载两个目录层次结构才能访问两者。当第二个（子）目录层次结构未显式挂载时，其挂载点将显示为空目录且目录层次结构被隐藏。`nohide` 选项会导致底层目录结构在未显式挂载时出现，但此选项并非所有情况下都起作用。见第 804 页的“持有挂载点的导出分区”。默认是 `nohide`。

`ro (rw)` `ro` 选项仅允许对 NFS 目录层次结构进行读请求。使用 `rw` 允许读和写请求。默认是 `ro`。

`secure (insecure)` `secure` 选项要求访问源自 root（第 1182 页），因此没有 root 权限的程序无法挂载目录层次结构。此选项不保证连接的安全。默认是 `secure`。

`no_subtree_check (subtree_check)` `no_subtree_check` 选项禁用文件的子树。如果你有一个导出的目录层次结构，其包含一个子目录，如果该子目录未显式挂载，其挂载点可能会出现问题。`no_subtree_check` 选项允许目录层次结构在未显式挂载时也出现，但此选项并非在所有情况下都有效。`no_subtree_check` 选项禁用子树检查。当 NFS 服务器接收请求时，如果文件在导出的目录层次结构中，它会执行子树检查。子树检查在某些情况下会导致用户重命名时产生问题。对于，使用 `no_subtree_check` 选项可能需要禁用子树检查。对于，你可能需要禁用子树检查。默认是 `no_subtree_check`。

`ro (rw)` `ro` 选项仅允许对 NFS 目录层次结构进行读请求。使用 `rw` 允许读和写请求。默认是 `ro`。

`secure (insecure)` `secure` 选项要求访问源自 root（第 1182 页），因此没有 root 权限的程序无法挂载目录层次结构。此选项不保证连接的安全。默认是 `secure`。

`no_subtree_check (subtree_check)` 禁用文件的子树。

`no_subtree_check` 选项禁用文件的子树。如果你有一个导出的目录层次结构，其包含一个子目录，如果该子目录未显式挂载，其挂载点可能会出现问题。`no_subtree_check` 选项允许目录层次结构在未显式挂载时也出现，但此选项并非在所有情况下都有效。

（注：由于原文中部分描述存在重复或逻辑断裂，此处翻译时已确保了语义连贯性并遵循了技术术语规范）

`auth_nml (no_auth_nml)` 或 `secure_locks (secure_locks)`

设置 `auth_nlm` 或 `secure_locks` 选项（这两个选项相同）会导致服务器要求对锁请求进行认证。当你发现只有任何人都可以读取的文件才能锁定时，对较旧的客户端使用 `no_auth_nml`。默认是 `auth_nlm`。

`mountpoint=[path]` 仅当目录已挂载时允许导出该目录。此选项防止了没有目录层次结构的挂载点被导出。

`nohide (hide)` 当服务器导出两个目录层次结构且其中一个挂载在另一个上时，`hide` 选项要求客户端必须显式挂载两个目录层次结构才能访问两者。当第二个（子）目录层次结构未显式挂载时，其挂载点将显示为空目录且目录层次结构被隐藏。

`ro (rw)` `ro` 选项仅允许对 NFS 目录层次结构进行读请求。使用 `rw` 允许读和写请求。默认是 `ro`。

`secure (insecure)` `secure` 选项要求访问源自 root（第 1182 页），因此没有 root 权限的程序无法挂载目录层次结构。

`no_subtree_check (subtree_check)` `no_subtree_check` 选项禁用文件的子树。

`sec=mode` `mode` 模式是认证类型。

`sync (async)` `sync` 选项指定服务器在更改写入磁盘后进行响应。`async` 选项指定服务器不需要等待更改写入磁盘。默认是 `sync`。

`wdelay (write)` `wdelay` 选项会导致服务器在接收到多个小的写请求时延迟写入操作。

## 设置 NFS 服务器

### 用户 ID 映射选项

每个用户在服务器上都有一个 UID 和主 GID。当客户端向 NFS 服务器发送请求时，服务器使用这些数字来识别用户，这会引发几个问题：

- 用户在两个系统上可能没有相同的 UID。
- 你可能不想让客户端具有 root 权限的用户对系统文件具有所有权限。
- 你可能不希望远程用户对 root 拥有的文件具有所有权限

对文件的所有权限意味着远程用户可以执行或修改文件。NFS 提供了两种方法处理这些问题：

- 你可以使用 `root_squash` 选项将客户端上的 root 账户映射为 `nfsnobody` 用户（UID 65534），或根据 `anonuid` 指定的用户。
- 你可以使用 `all_squash` 选项将客户端上的所有 NFS 用户映射为服务器上的 `nfsnobody`（UID 65534）。

`/etc/passwd` 文件显示 `nfsnobody` 的 UID 和 GID 为 65534。使用 `anonuid` 和 `anongid` 来覆盖这些值。

当我们使用 NFS 进行用户授权时，用户在两个系统上具有相同的 UID。如果你在大型网络上使用 NFS，使用目录服务（如 NIS 或 LDAP，第 776 页）进行授权是一个好主意。如果没有此类服务，你必须手动同步所有系统的 passwd 文件。

`root_squash (no, root_squash)`

`root_squash` 选项映射客户端上的 root 请求，使其看起来来自 `nobody` 用户（UID 65534）、非特权用户或根据 `anonuid` 指定的用户。此选项不影响其他敏感 UID（如 `bin`）。`no_root` 选项关闭此映射，使 root 的请求看起来来自 root。默认是 `root_squash`。

`all_squash (all_squash)`

`all_squash` 选项不会更改向 NFS 服务器发送请求的客户端映射。`all_squash` 选项将客户端系统上的所有用户（而非 root）的请求映射为 `nfsnobody` 用户（UID 65534）、非特权用户或根据 `anonuid` 指定的用户。此选项对于控制对导出的公共 FTP、新闻和其他目录的访问。

### NFS 挂载目录中的关键文件由 root 所有

尽管通过 `root_squash` 选项进行了映射，客户端系统中具有 root 权限的用户仍然可以使用 `sudo` 或冒充系统上任何用户的身份，然后访问服务器上该用户的文件。在不诉诸 `all_squash` 的情况下，你只能保护 NFS 服务器上由 root 拥有的文件。确保 root——而不是 bin或其他用户——是唯一可以修改或删除任何 NFS 挂载目录层次结构内关键文件的用户。

采取这一预防措施不能完全保护系统免受具有 root 权限的攻击者的侵害，但它可以阻止恶意程度较低的用户攻击。

`anonid=un` 将匿名账户的 UID 或 GID 设置为 `un` 或 `gn`。当 NFS 无法识别传入的 UID 或 GID 且根据 `root_squash` 或 `all_squash` 的指令时，会使用 `anonid=gn` 使用这些账户。这两个选项默认均为 `nfsnobody` (UID 65534)。

### 系统存放挂载信息的位置

服务器持有多个可以出的目录层次结构列表。系统管理员使用的列表是 `/etc/exports`。本节描述了 NFS 使用的重要文件和伪节点（inodes）。后续讨论假设服务器 `plum` 正在导出 `/home/public` 和 `/home/zach` 目录层次结构。
