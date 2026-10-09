

## NFS 服务器选项：`all_squash` 和匿名用户 ID

- `no_all_squash`（`all_squash`）：不更改对 NFS 服务器发起请求的用户的映射。`all_squash` 选项将来自远程系统上所有用户（不仅仅是 root）的请求映射为看起来像是来自本地系统的 UID 65534（一个非特权用户），或者由 `anounid` 指定的用户。此选项有助于控制对导出的公共 FTP、新闻组以及其他目录的访问。
- `anounid=uid` 和 `anongid=gid`：分别将匿名用户账户的 UID 或 GID 设置为 `uid` 或 `gid`。当 NFS 不识别传入的 UID 或 GID，且被指示这样做时（通过 `root_squash` 或 `all_squash`），NFS 会使用这些账户。

## 系统存储 NFS 挂载信息的位置

服务器持有若干可导出的目录层次结构列表。作为系统管理员，您操作的列表是 `/etc/exports`。以下讨论假设本地服务器 `plum` 正在导出这些目录层次结构：

```bash
$ cat /etc/exports

/home grape(rw,no_subtree_check)

/pl6 192.168.0.12(rw,no_subtree_check) jam(rw,no_subtree_check)
```

如第 791 页更详细地所述，`exportfs` 显示导出目录层次结构的列表：

```bash
$ exportfs

/home grape

/pl6 jam
192.168.0.12
```

NFS 处理的重要文件和伪文件描述如下。

`/var/lib/nfs/etab`（导出表）：在服务器上，列出被导出的目录层次结构（可以挂载，但当前不一定已挂载）以及它们导出时使用的选项：

```bash
$ cat /var/lib/nfs/etab

/home grape(rw,sync,wdelay,hide,nocrossmnt,secure,root_squash,no_all_squash,no_subtree_check,secure_locks,acl,mapping=identity,anounid=65534,anongid=65534)

/pl6 jam(rw,sync,wdelay,hide,nocrossmnt,secure,root_squash,no_all_squash,no_subtree_check,secure_locks,acl,mapping=identity,anounid=65534,anongid=65534)

/pl6 192.168.0.12(rw,sync,wdelay,hide,nocrossmnt,secure,root_squash,no_all_squash,no_subtree_check,secure_locks,acl,mapping=identity,anounid=65534,anongid=65534)
```

前面的输出显示 `grape` 可以挂载 `/home`，而 `jam` 和 `192.168.0.12` 可以挂载 `/pl6`。`etab` 文件在系统启动时由 `/etc/exports` 初始化，当客户端请求挂载目录层次结构时由 `mountd` 读取，并随着导出目录层次结构列表的变化由 `exportfs`（第 791 页）修改。

`/var/lib/nfs/rmtab`（远程挂载表）：在服务器上，列出由客户系统挂载的目录层次结构：

```bash
$ cat /var/lib/nfs/rmtab
192.168.0.12:/pl6:0x00000002
```

前面的输出显示 `/pl6` 被 `192.168.0.12` 挂载。`rmtab` 文件由 `mountd` 在挂载和卸载目录层次结构时进行更新。该文件是“主要起装饰作用”（摘自 `mountd` 的手册页），可能并不准确。

`/proc/mounts`：在客户端，这个伪文件显示内核挂载表，其中列出了由本地系统挂载的文件系统。在下面的示例中，`grep` 显示包含字符串 `nfs` 后跟一个空格（SPACE）的行。您必须加引号的空格（SPACE）用于排除那些与已挂载文件系统无关的包含字符串 `nfs` 的行。

```bash
$ grep nfs\ /proc/mounts
plum:/pl6 /mnt nfs rw,vers=3, rsize=131072, wsize=131072,hard,intr,proto=tcp,timeo=600,retrans=2,sec=sys,addr=plum 0 0
```

### showmount：显示 NFS 状态信息

不带任何选项时，`showmount` 实用程序显示允许挂载本地目录的系统列表。通常使用 `showmount` 来显示服务器正在导出的目录层次结构列表。要显示远程系统的信息，请将远程系统的名称作为参数提供。然而，`showmount` 提供的信息可能不完整，因为它依赖于 `mountd`，并信任远程服务器报告的信息是准确的。

在下面的示例中，`192.168.0.12` 被允许挂载本地目录，但你不知道具体是哪些目录：

```bash
$ showmount
Hosts on plum:
192.168.0.12
```

如果 `showmount` 显示诸如 `RPC: Program not registered` 的错误，则表示 NFS 未在服务器上运行。使用 `nfs-kernel-server` 初始化脚本（第 782 页）在服务器上启动 NFS。

选项：

- `-a`（all）：显示客户系统列表，并指示每个客户系统可以挂载哪些目录。这些信息存储在 `/etc/exports` 中。在下面的示例中，`showmount` 列出 `192.168.0.12` 可以从本地系统挂载的目录：
  ```bash
  $ /sbin/showmount -a
  All mount points on plum:
  192.168.0.12:/pl6
  ```
- `-e`（exports）：显示导出目录的列表以及每个目录导出到哪些系统。
  ```bash
  $ showmount -e
  Export list for plum:
  /pl6 192.168.0.12
  ```

### exportfs：维护导出目录层次结构列表

`exportfs` 实用程序维护 `/var/lib/nfs/etab` 文件（第 789 页）。当调用 `mountd` 时，它会检查此文件以确定是否允许挂载请求的目录层次结构。通常，`exportfs` 会带有简单选项调用，并根据 `/etc/exports` 中的变化修改 `etab` 文件。当使用客户端和目录参数调用时，它可以添加或删除由这些参数指定的目录层次结构到 `etab` 中维护的列表中，而无需参考 `exports` 文件。`exportfs` 命令的格式如下：

```bash
/usr/sbin/exportfs [options] [client dir ...]
```

其中 `options` 是一个或多个选项（如下一节所述），`client` 是 `dir` 导出到的系统名称，`dir` 是位于被导出的目录层次结构根部的目录的绝对路径名。不带任何参数时，`exportfs` 报告哪些目录层次结构导出到了哪些系统：

```bash
$ exportfs
/home       grape
/pl6        jam
/pl6        192.168.0.12
```

系统启动时（位于 `nfs-kernel-server` 初始化脚本中）执行以下命令。此命令重新导出 `/etc/exports` 中的条目，并从 `/var/lib/nfs/etab` 中移除无效条目，以便 `etab` 与 `/etc/exports` 保持同步：

```bash
$ sudo exportfs -r
```

#### 选项

1. `-a`（all）：导出在 `/etc/exports` 中指定的目录层次结构。此选项不会取消导出您已从 `exports` 中移除的条目（即，它不会从 `/var/lib/nfs/etab` 中移除无效条目）；请使用 `-r` 来执行此任务。
2. `-f`（flush）：从内核的导出表中清除所有内容。
3. `-i`（ignore）：忽略 `/etc/exports`；仅使用命令行上指定的内容。
4. `-o`（options）：指定选项。您可以像在 `exports` 文件中那样指定跟随 `-o` 的选项。例如，`exportfs -i -o ro dog:/home/sam` 将本地系统上的 `/home/sam` 以只读权限导出给 `dog`。
5. `-r`（reexport）：重新导出 `/etc/exports` 中的条目，并从 `/var/lib/nfs/etab` 中移除无效条目，以便 `/var/lib/nfs/etab` 与 `/etc/exports` 保持同步。
6. `-u`（unexport）：使已导出的目录层次结构不再导出。如果在取消导出时某个目录层次结构已挂载，用户尝试从远程系统访问该目录层次结构时会看到消息 `Stale NFS file handle`。
7. `-v`（verbose）：提供更多信息。当您使用 `exportfs` 显示导出信息时，会显示导出选项。

### 测试服务器配置

从服务器运行 **nfs-kernel-server** 初始化脚本，并带 *status* 参数。如果一切正常，系统将显示以下内容：

```bash
$ service nfs-kernel-server status

nfsd running
```

还要检查 **mountd** 是否正在运行：

```bash
$ ps -e | grep mountd

29609 ? 00:00:00 rpc.mountd
```

接下来，从服务器使用 **rpcinfo** 确保 NFS 已注册到 portmap：

```bash
$ rpcinfo -p localhost | grep nfs

100003 2 udp 2049 nfs
100003 3 udp 2049 nfs
100003 4 udp 2049 nfs
100003 2 tcp 2049 nfs
100003 3 tcp 2049 nfs
100003 4 tcp 2049 nfs
```

从客户端重复上述命令，用服务器名称替换 **localhost**。结果应该相同。

最后，尝试从远程系统挂载目录层次结构并验证访问权限。

### automount：按需挂载目录层次结构

在分布式计算环境中，当您在网络上的任何系统上登录时，您的所有文件——包括启动脚本——都可用。通常，所有系统也能够挂载所有服务器上的所有目录层次结构：无论您登录哪个系统，您的主目录都在等待您。

举个例子，假设 `/home/zach` 是一个按需挂载的远程目录层次结构。当您发出命令 `ls /home/zach` 时，**autofs** 开始工作：它查找 `/etc/auto_home` 映射，发现 **zach** 是一个键，指示要挂载 **plum:/export/home/zach**，然后挂载该远程目录层次结构。一旦目录层次结构被挂载，`ls` 显示该目录中的文件列表。如果在这个挂载序列之后给出命令 `ls /home`，`ls` 显示 **zach** 存在于 `/home` 目录中。`df` 实用程序显示 **zach** 是从 **plum** 挂载的。

### 先决条件

安装以下软件包：

- autofs

