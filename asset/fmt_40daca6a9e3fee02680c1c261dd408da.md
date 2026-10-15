
`fstab` 中的以下行将 grape 的 `/gc1` 文件系统挂载到 `/grade.gc1` 挂载点：

```
grade:/gc1  /grade.gc1  nfs  rsize=8192,wsize=8192  0 0
```

挂载点应该是一个空本地目录。（当目录层次结构挂载到挂载点时，挂载点中的文件将被隐藏）。使用 NFS 挂载的文件系统类型始终为 false，无论其在本地系统上的类型为何。你可以通过增加 `rsize` 和 `wsize` 选项来提高性能。请参阅第 780 页的“提高性能”。

`fstab` 的下一个示例挂载了来自 dog 的文件系统：

```
dog:/export  /dog.export  nfs  timeout=50,hard  0 0
```

由于本地系统通过慢速连接到 dog，因此 `timeout` 增加到 5 秒（50 个十分之一秒）。请参阅第 780 页的“超时”。此外，设置 `hard` 是为了确保 NFS 在发生严重超时后继续尝试与服务器通信。请参阅第 780 页的“hard/soft”。

`fstab` 的最后一个示例显示了远程挂载的家目录。由于 dog 是本地服务器且通过可靠的高速连接，因此缩短了时间并大幅增加了 `rsize` 和 `wsize`：

```
dog:/home /dog.home nfs time=4,rsize=16384,wsize=16384 0 0
```

# 设置 NFS 服务器

## 前提条件

安装：安装以下软件包：

- `nfs-kernel-server`

`portmap` 工具是 `portmap` 软件包的一部分，并在安装 `nfs-kernel-server` 时作为依赖项安装；必须运行第 406 页提到的可靠的文件锁定。

当你安装 `nfs-kernel-server` 软件包时，`dpkg postinst` 脚本会启动 `init nfsd`（nfs 内核守护进程）。配置完成后，调用 `nfs-kernel-server` 脚本重新导出目录层次结构并重启 NFS 守护进程：

```
$ sudo service nfs-kernel-server restart
- Stopping nfs kernel daemon [ OK ]
- Unexporting directories for NFS kernel daemon... [ OK ]
- Exporting directories for NFS kernel daemon... [ OK ]
- Starting nfs kernel daemon [ OK ]
```

在运行中的服务器上更改 NFS 配置后，使用 `reload` 代替 `restart` 以便在不断开客户端连接的情况下重新导出目录层次结构。

### 允许的主机

![](img/c8ae2cd4d550a81142a3ed64b0f61f6a_835_0.png)

**图 22-4** 允许的主机窗口

你可以忽略提及 subtree_check 的错误消息。有关此参数的更多信息，请参阅第 787 页。

执行不带任何选项的 `exportfs` 命令可以显示导出目录层级列表以及它们各自导出的系统：

```
$ exportfs
/p16 192.168.0.12
```

有关 `exportfs` 的更多信息请参阅第 791 页。

## 手动导出目录层级

导出目录层级允许指定的系统通过网络挂载该层级。“导出”并不意味着“挂载”：当一个目录层级被导出时，它会被放入目录层级列表中，该导出的目录层级可以在任何时间被挂载（或不挂载）。

## 导出符号链接和设备文件

> 提示：当你导出包含符号链接的目录层级时，请确保链接的对象在客户端（远程）系统上可用。如果链接的对象在客户端系统上不存在，你必须连同导出的链接一起导出并挂载。否则，链接将无法指向它原本指向的文件。

设备文件指的是 Linux 内核接口。当你导出设备文件时，你导出的是该接口。如果客户端系统没有相同类型的设备，该设备将无法工作。为了提高客户端的安全性，你可以使用 `mount` 的 `nodev` 选项（第 777 页），防止挂载目录层级中的设备文件被当作设备使用。

挂载点位于导出分区内的挂载目录层级不会随分区一起导出。你必须显式地导出每个想要导出的目录层级，即使它位于一个已经导出的目录层级内部。例如，假设两个目录层级 `/opt/apps` 和 `/opt/apps/oracle` 位于两个分区上。你必须显式地导出每个目录层级，尽管 oracle 是 apps 的子目录。大多数其他子目录和文件都会自动导出。

## `/etc/exports`：存储导出目录层级列表

`/etc/exports` 文件是 NFS 客户端可以挂载的导出目录层级的访问控制列表；它是设置 NFS 服务器时唯一需要编辑的文件。`exports` 实用（第 791 页）在更新 `/var/lib/nfs`（第 789 页）中的文件时会读取此文件，内核使用它来保持挂载表更新。exports 策略控制以下 NFS 特性：

- 哪些客户端可以访问服务器（另请参见第 776 页的“安全性”）
- 每个客户端可以访问服务器上的哪些目录层级
- 每个客户端如何访问每个目录层级
- 客户端用户名如何映射到服务器用户名
- 各种 NFS 参数

exports 文件中的每行具有以下格式：

```
export-point client1(option-list) [client2(option-list) ...]
```

其中 `export-point` 是要导出目录层级根目录的绝对路径。`client-n` 是一个或多个客户端的名称或 IP 地址，用空格分隔，允许挂载 `export-point`。在下一节描述的 `option-list` 是适用于前一个客户端的逗号分隔的选项列表；它不能包含任何空格。在客户端名称和开始选项-列表的左括号之间不能有空格。

[可以使用 `shares-admin`（第 783 页）来更改 exports 或手动编辑此文件。以下 exports 文件赋予 grape 对 `/home` 的读写权限，并赋予位于 192.168.0.12 上的 jam 对 `/pl6` 的读写权限：]

```
$ cat /etc/exports
/home grape(rw,no_subtree_check)
/pl6 192.168.0.12(rw,no_subtree_check) jam(rw,no_subtree_check)
```

指定的目录位于本地服务器上。在每种情况下，以导出目录为根的目录层级都会隐式授予访问权限。你可以指定 IP 地址或主机名，并可以在同一行中指定多个客户端。默认情况下，目录层级以只读模式导出。当前版本的 exports 在你未指定 *subtree_check*（第 787 页）之一时会发出警告。

## 通用选项

本节的左列列出了默认选项，随后是括号括出的非默认选项。更多信息请参阅 exports 手页。

`auth_nlm (no_auth_nlm)` 或 `secure_locks (secure_locks)`

导致服务器对锁请求进行认证（使用 NLM [NFS 锁管理器] 协议）。当你发现只有任何人都可以读取的文件被锁定时，对旧客户端使用 `no_auth_nlm`。

## 设置 NFS 服务器

`mountpoint[path]`

仅当目录已挂载时才允许导出。此选项防止了没有挂载目录层级的挂载点被导出，并防止底层的挂载点被导出。也是 `mp`。

`nohide (hide)`：当服务器导出两个目录层级且其中一个挂载在另一个上，客户端必须显式挂载两个目录层级才能访问两者。当第二个（子）目录层级未被显式挂载时，其挂载点将显示为空目录且目录层级被隐藏。`nohide` 选项导致底层的第二个目录层级在未显式挂载时也会显示。

`ro (rw)`：仅允许读写。

`secure (insecure)`：要求请求来自安全端口。

`no_subtree_check`：检查导出文件是否仍是目录的一部分。

`subtree_check`：检查导出文件是否仍是目录的一部分。

`sync (async)`：指定服务器在写入提交后回复。

`wdelay (no_wdelay)`：导致服务器不等待写入提交。

## 用户 ID 映射选项

每个用户在本地系统中有一个 UID 号和一个 GID 号。exports 实用可以将这些数字映射为名称。当用户向 NFS 服务器请求时，服务器使用这些数字来识别远程用户：

- 用户在两个系统的 ID 不同（解决方案请参见“NIS 与 NFS”）。
- 你可能不允许具有 root 权限的用户访问 root 文件。
- 你可能不允许远程用户访问 bin。

当使用 NIS（第 741 页）进行用户授权时，用户在两个系统中具有相同的 UID。如果你在大型网络上使用 NFS，使用 NIS 或 LDAP（第 758 页）等目录服务是好主意。如果没有服务，你必须手动同步所有系统的 passwd 文件。

## NFS 挂载目录中的文件应由 root 所有

尽管 root-squash 选项进行了映射，客户端系统上具有 root 权限的用户可以使用 sudo 或切换任何用户的身份并访问该用户的文件。因此，在不使用 all-squash 的情况下，你只能在 NFS 服务器上保护 root 的文件。确保只有 root——而不是 bin 或其他用户可以修改或删除任何目录内的关键文件。

采取这种预防措施无法完全防止具有 root 权限的攻击者，但它可以帮助阻止经验丰富的恶意用户。

对文件的所有权意味着远程用户可以执行甚至更糟——修改文件。NFS 提供了两种处理这些情况的方法：

- 你可以使用 `root_squash` 选项将客户端 root 账户的 ID 号映射为服务器上的 UID 65534。
- 你可以使用 `all-squash` 选项将客户端上的所有 NFS 用户映射为服务器上的 UID 65534。

使用 `anuid` 和 `anogid` 选项覆盖这些值。

`root_squash (no_root_squash)`

将远程系统 root 的请求映射为看似来自 UID 65534、本地系统的非特权用户或由 `anuid` 指定的用户。此选项不影响其他 UID（如 bin）。`no_root_squash` 选项关闭此映射，使得来自 root 的请求看起来来自 root。

## 设置 NFS 服务器 79

no_all_squash 不更改 NFS 服务器对用户请求的映射。

`(all_squash)` 选项将远程系统上所有用户（不仅仅是 root）的请求映射为来自本地系统 UID 65534（本地系统上的非特权用户），或由 anonid 指定的标识。此选项用于控制对导出的 FTP、NFS 以及其他目录的访问。

anonid=un 和 Set 将匿名账户的 UID 和 GID 分别设置为 `un` 或 `gn`。NFS 

anonid=gn 在无法识别传入的 UID 或 GID 且，且在被 root_squash 或 all_squash 指示执行操作时，使用这些账户。

## 系统在何处保存 NFS 挂载信息

服务器持有多个组要导出的目录层次结构列表。系统管理员使用的列表是 `/etc/exports`。接下来的讨论假设本地服务器 plum 正在导出这些目录层次结构：

```
$ /etc/exports
/home grape(rw,no_subtree_check)
/p16 192.168.0.12(rw,no_subtree_check) jam(rw,no_subtree_check)
```

如在 791 页详细解释的那样，exports 显示了导出的目录层次结构列表：

```
$ exports
/home grape
/p16 jam
/p16 192.168.0.12
```

文中描述了 NFS 工作的重要文件和伪文件（pseudofs）。

(export table) 在服务器上，列出了导出的目录层次结构（可以挂载，但并不一定已经挂载）以及它们导出时使用的选项：

```
$ /var/lib/nfs/stab
/home grape(rw,sync,wdelay,hide,nocrossmnt,secure,root_squash,no_all_squash,no_subtree_check,secure_locks,acl,mapping-identity,anonuid=65534,
anonid=65534)
/p16 jam(rw,sync,wdelay,hide,nocrossmnt,secure,root_squash,no_all_squash,sh,no_subtree_check,secure_locks,acl,mapping-identity,anonuid=65534,
anonid=65534)
/p16 192.168.0.12(rw,sync,wdelay,hide,nocrossmnt,secure,root_squash,no_all_squash,no_subtree_check,secure_locks,acl,mapping-identity,anonuid=65534)
anonid=65534)
```

前面的输出显示 grape 可以挂载 `/home`，而 jam 和 192.168.0.12 可以挂载 `/p16`。etab 文件在系统启动时从 `/etc/exports` 初始化，当客户端请求挂载目录层次结构时被 mount 读取，并在导出的目录层次结构列表变化时由 exports（第 791 页）修改。

`/var/lib/nfs/rmtab`

(远程挂载表) 在服务器上，列出了由客户端系统挂载的目录层次结构：

```
$ cat /var/lib/nfs/rmtab
192.168.0.12:/p16:0x0000002
```

前面的输出显示 p16 已被 192.168.0.12 挂载。rtab 文件在 mount 挂载和卸载目录层次结构时会更新。该文件“大多是装饰性的”（来自 mount 手页），可能不准确。

`/proc/` 在客户端上，此伪文件显示内核挂载表，列出了由本地系统挂载的文件。在接下来的示例中，grep 显示包含字符串 nfs 后紧跟空格（SPACE）的行。必须加引号的空格 消除了包含 nfs 字符串但不属于已挂载系统的行。

```
$ grep nfs /proc/mounts
plump:/p16 mnt nfs rw,vers=3,size=131072,wsize=131072,hard,intr,proto=tcp,timeo=600,retrans=2,sec=sys,addr=plump 0 0
```

## showmount: 显示 NFS 状态信息

在不带任何选项的情况下，showmount 工具显示允许挂载本地目录的系统列表。通常使用 showmount 显示服务器正在导出的目录层次结构列表。要显示远程系统的信息，请将远程系统的名称作为参数。然而，showmount 显示的信息可能完整，因为它依赖 mount 并信任远程服务器注册是准确的。

在接下来的示例中，192.168.0.12 被允许挂载本地目录，但你不知道具体是哪些：

```
$ showmount
Hosts on plum:
192.168.0.12
```

如果 showmount 显示类似 RPC: Program not registered 的错误，则 NFS 未在服务器上运行。使用 nfs-kernel-init 脚本（第 782 页）在服务器上启动 NFS。

- (all) 显示客户端系统列表并指示哪个客户端系统可以挂载。此信息存储在 `/etc/exports` 中。在接下来的示例中，showmount 列出了 192.168.0.12 可以从本地系统挂载的目录：

```
$ /sbin/showmount -a
All mount allowed by:
192.168.0.12
```

- (e) 显示导出的目录列表。

```
$ showmount -e
Export list for:
/home grape
/p16 jam
/p16 192.168.0.12
```

## exportfs: 维护导出的目录层次结构

exportfs 工具维护 `/etc/exports` 文件。当调用时，它检查 `/etc/exports` 并列出导出的目录层次结构（可以挂载，但并不一定已经挂载）以及它们导出时使用的选项，更新 `/var/lib/nfs/stab`：

```
$ exportfs -v
/home grape(rw,sync,wdelay,hide,nocrossmnt,secure,root_squash,no_all_squash,no_subtree_check,secure_locks,acl,mapping-identity,anonuid=65534,
anonid=65534)
/p16 jam(rw,sync,wdelay,hide,nocrossmnt,secure,root_squash,no_all_squash,sh,no_subtree_check,secure_locks,acl,mapping-identity,anonuid=65534,
anonid=65534)
/p16 192.168.0.12(rw,sync,wdelay,hide,nocrossmnt,secure,root_squash,no_all_squash,no_subtree_check,secure_locks,acl,mapping-identity,anonuid=65534)
anonid=65534)
```

- (all) 显示客户端系统列表并指示哪个客户端系统可以挂载。此信息存储在 `/etc/exports` 中。
- (f) 刷新导出表。
- (i) 显示导出的目录层次结构。
- (o) 指定导出的选项。
- (r) 重新导出 `/etc/exports` 中的项目。
- (s) 显示当前允许挂载的客户端系统。
- (u) 从导出表中移除目录层次结构。
- (v) 提供更多信息。

## 测试设置

从服务器上，运行 nfs-kernel-init 脚本并参数 status。如果一切正常，服务器将显示：

```
$ service nfs-kernel-init status
nfsd running
```
