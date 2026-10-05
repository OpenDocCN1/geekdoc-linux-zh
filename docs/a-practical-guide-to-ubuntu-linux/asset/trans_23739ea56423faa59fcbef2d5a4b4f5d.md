

# /etc/exports: 包含导出目录层次级列表

/etc/exports 文件是 NFS 客户端挂载的导出目录层次级的访问控制列表；它是你设置 NFS 服务器时唯一需要编辑的文件。exports 实用程序（第 791 页）在更新 /var/lib/nfs（第 789 页）中的文件时会读取此文件，内核使用这些文件来保持其挂载表是最新的。exports 文件控制以下 NFS 特性：

- 哪些客户端可以访问服务器（另见第 776 页的“安全”）
- 每个客户端可以访问服务器上的哪些目录层次级
- 每个客户端如何访问每个目录层次级
- 客户端如何映射到服务器用户名
- 各种 NFS 参数

文件中的每行都遵循以下格式：

```
export-pointclient1 (option-list) [client2(option-list) ... ]
```

其中 `export-point` 是被导出目录层次级根目录的绝对路径。`client-names` 是一个或多个客户端的名称或 IP 地址，用空格分隔，允许挂载 `export-point`。下一节描述的 `option-list` 是适用于前一个客户端的逗号分隔选项列表；它不能包含任何空格。在每个客户端名称与开始选项列表的括号之间不能有空格。

你可以使用 `shares-admin`（第 783 页）对 exports 进行更改，或手动编辑此文件。以下 exports 文件授予 /home 读写权限，并授予 192.168.0.12 上的 jam 和系统 /pl16 的读写权限：

```
$ cat /etc/exports
/home /grape(rw,no_subtree_check)
/pl16 192.168.0.12(rw,no_subtree_check) jam(rw,no_subtree_check)
```

指定的目录位于本地服务器上。在这种情况下，该目录导出的目录层次级被隐式授予访问权限。你可以指定 IP 地址或主机名，并且可以在行内指定多个客户端系统。默认情况下，目录层次级以只读模式导出。当前版本的 exports 在你未指定指定 `subtree_check` 或 `no_subtree_check`（第 78 页）时会发出警告。

## 通用选项

本节的左列列出了默认选项，随后是括号中的非默认选项。更多信息请参阅 exports 手册。

`auth_nlm (no_auth_nlm)` 导致服务器对锁请求进行认证（使用 NLM [NFS 锁管理器] 协议）。发现只有任何人都可以读取的文件才能被锁定时，对客户端使用 `no_auth_nlm`。

## 设置 NFS 服务器

**mountpoint=[path]** 允许仅在目录已挂载时对其进行导出。此选项防止未挂载目录层次级的挂载点被导出，并防止底层的挂载点被导出。还有 **mp**。

**nohide (hide)** 当服务器导出两个目录层次级，且其中一个挂载在另一个上，客户端必须显式挂载两个目录层次级才能访问两者。当第二个（子）目录层次级未显式挂载时，其挂载点显示为空目录且该目录层次级被隐藏。**nohide** 会导致底层的第二个目录层次级在未显式挂载时出现，但此选项并非所有情况下都有效。

**ro (readonly)** 仅允许对 NFS 层次级进行读取请求。**使用 rw** 允许读取和写入请求。

**secure (insecure)** 要求 NFS 源自*特权端口*（第 1160 页），因为没有 *root* 权限运行的程序无法挂载目录层次级。此选项不保证连接的安全。

**no_subtree_check (subtree_check)** 检查有效文件。由于你导出的目录层次级的根目录位于持有它的文件系统的根目录之下（即文件系统的子目录）。当 NFS 服务器接收到该层次级中文件的请求时，它会执行子树检查以确认该文件在导出的目录层次级中。

子树检查可能会导致打开时重命名的文件出现问题，在使用 *no_root_squash* 时，只有具有 *root* 权限运行的进程才能访问。**no_subtree_check** 选项禁用子树检查并在某些情况下提高可靠性。

例如，你可能需要对主目录禁用子树检查。主目录经常是子树（位于 */home/），经常被写入，且内部文件经常被重命名。你可能不需要对包含大多数读取文件的（如 */usr/）的目录层次级禁用子树检查。

由于默认值已更改（现在是 **no_subtree_check**），当你未指定 **subtree_check** 或 **no_subtree_check** 时，exports 会显示警告。

**sync (async)** 指定服务器仅在由请求引起的磁盘更改写入磁盘后才响应请求。**async** 选项指定服务器不需要等待信息写入，可以提高性能，但代价是如果服务器崩溃或连接中断，可能会导致数据损坏。

**wdelay (write delay)** 导致服务器在预判会有另一个相关请求时延迟提交写入请求，从而通过在单个操作中提交多个写入请求来提高性能。**no_wdelay** 选项不延迟提交写入请求，当服务器接收到多个小的、不相关的请求时可以提高性能。

使用 `anonym` 和 `anagid` 选项来覆盖这些值。将来自远程系统 root 的请求映射，使其显示为本地系统上的非特权用户 UID 65534，或由 `anon` 指定。**no_root_squash** 选项关闭此映射，使来自 root 的请求显示为 root。

**all_squash** 不更改向 NFS 服务器发送请求的用户映射映射（all_squash）选项将所有用户（而是 root）映射到匿名账户。将匿名账户的 UID 和 GID 分别设置为 `un` 或 `gn`。当 NFS 不识别传入的 UID 和 GID 且被指示执行这样做时，它会使用这些账户。

## 系统保留挂载信息

服务器持有其可以导出的目录层次级列表。你作为系统管理员使用的列表是 /etc/exports。以下讨论假设本地服务器 plum 正在导出这些目录层次级：

```
$ cat /etc/exports
/home /grape(rw,no_subtree_check)
/pl16 192.168.0.12(rw,no_subtree_check) jam(rw,no_subtree_check)
```

正如第 791 页详细解释的那样，exports 显示导出的目录层次级列表：

```
$ exportfs
/home grape
/pl16 jam
192.168.0.12
```

接下来将描述 NFS 使用的重要文件和伪文件。

/var/lib/nfs/stab (导出表) 在服务器上，列出已导出的目录层次级（可以挂载，但不一定已挂载）以及导出时的选项：

```
$ cat /var/lib/nfs/stab
/home grape(rw,wdelay,hide,nocrossmnt,secure,root_squash,no_all_squash,no_subtree_check,secure_locks,acl,mapping=identity,anouid=65534,anongid=65534)
/pl16 jam(rw,wdelay,hide,nocrossmnt,secure,root_squash,no_all_squash,no_subtree_check,secure_locks,acl,mapping=identity,anouid=65534,anongid=65534)
/pl16 192.168.0.12(rw,wdelay,hide,nocrossmnt,secure,root_squash,no_all_squash,no_subtree_check,secure_locks,acl,mapping=identity,anouid=65534,anongid=65534)
```

stab 文件在系统启动时从 /etc/exports 初始化，在客户端挂载目录层次级时由 plum 读取，并在导出层次级列表发生变化时由 exportfs（第 791 页）进行修改。

