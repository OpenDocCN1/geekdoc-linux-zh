
不可用。如果在这些情况下尝试访问远程文件，您将收到一条错误消息，例如 **NFS 服务器 xxx 无响应**。当本地系统能够再次联系到服务器时，NFS 将显示另一条消息，例如 **NFS 服务器 xxx 正常**。稳定的网络和服务器（或者不使用 NFS）是防止此问题的最佳方法。

**mount: RPC: Program not registered** 消息可能意味着 NFS 未在服务器上运行。在服务器上启动 **nfsd** 和 **rpcbind** 守护进程。

**Stale NFS filehandle** 消息出现在客户端上打开的文件被删除、重命名或替换时。请尝试重新挂载目录层次结构。

## 测试服务器

在服务器上，运行 **systemctl**。如果一切正常，系统将显示类似于以下内容：

```
# systemctl status nfs.service
nfs-server.service - NFS Server
   Loaded: loaded (/usr/lib/systemd/system/nfs-server.service; disabled)
   Active: active (exited) since Tue 2013-06-25 19:22:31 PDT; 26s ago
 Process: 1972 ExecStartPost=/usr/lib/nfs-utils/scripts/nfs-server.postconfig (code=exited, status=0/SUCCESS)
 Process: 1955 ExecStart=+/usr/sbin/rpc.nfsd $RPCNFSDARGS $RPCNFSDCOUNT (code=exited, status=0/SUCCESS)
 Process: 1947 ExecStartPre=/usr/sbin/exportfs -r (code=exited, status=0/SUCCESS)
 Process: 1940 ExecStartPre=/usr/lib/nfs-utils/scripts/nfs-server.preconfig (code=exited, status=0/SUCCESS)

Jun 25 19:22:31 plum systemd[1]: Starting NFS Server...
Jun 25 19:22:31 plum systemd[1]: Started NFS Server.
```

还要检查 **mountd** 是否正在运行：

```
$ ps -ef | grep mountd
 root      2110   0 18:31 ?        00:00:00 /usr/sbin/rpc.mountd
```

接下来，在服务器上，使用 **rpcinfo** 确保 NFS 已在 **rpcbind** 中注册：

```
$ rpcinfo -p localhost | grep nfs
100003   2   tcp   2049 nfs
100003   3   tcp   2049 nfs
100003   4   tcp   2049 nfs
100227   2   tcp   2049 nfs_acl
100227   3   tcp   2049 nfs_acl
100003   2   udp   2049 nfs
100003   3   udp   2049 nfs
100003   4   udp   2049 nfs
100227   2   udp   2049 nfs_acl
100227   3   udp   2049 nfs_acl
```

在客户端重复上述命令，将 **localhost** 替换为服务器名称。结果应该相同。

如果您收到权限拒绝消息，请检查是否

- 当客户端对目录层次结构只有读取权限时，您在 `/etc/exports` 中指定了 **rw** 访问权限。
- 您在 `/etc/exports` 中正确指定了目录层次结构和客户端。
- 自上次运行 `exportfs -r` 以来，您没有编辑过 `/etc/exports`。
- 您没有尝试导出一个目录层次结构以及该层次结构的一个子目录。从客户端，您可以分别挂载目录层次结构和该层次结构的子目录，但不能从服务器导出两者。仅导出较高级别的目录。

最后，尝试从远程系统挂载目录层次结构并验证访问权限。

## automount：按需挂载目录层次结构

在分布式计算环境中，当您登录网络上的任何系统时，您的所有文件——包括启动脚本——都可以访问。所有系统通常也能够挂载所有服务器上的所有目录层次结构：无论您登录哪个系统，您的主目录都在等待您。

例如，假设 `/home/zach` 是一个按需挂载的远程目录层次结构。当 Zach 登录或当您发出命令 `ls /home/zach` 时，`autofs` 开始工作：它在 `/etc/auto.misc` 映射中查找，发现 `/home/zach` 是一个键，表示要挂载 `plum:/home/zach`，然后挂载远程目录层次结构。一旦目录层次结构被挂载，`ls` 就会显示该目录中的文件列表。

`automount` 映射可以存储在 NFS 和 LDAP 服务器上，也可以存储在本地文件系统中。除非您更改 `/etc/nsswitch.conf` 文件中的 `automount` 条目（第 495 页），否则 `automount` 守护程序将把映射视为本地系统上的文件进行查找。

### 先决条件

安装以下软件包：

- `autofs`

运行 `systemctl` 使 `autofs` 服务（**automount** 守护程序）在系统每次进入多用户模式时启动，然后启动 `autofs` 服务。使用 `systemctl status` 命令确保服务正在运行。

```
# systemctl enable autofs.service
# systemctl start autofs.service
```

修改 `autofs` 配置文件后，再次给出第二个命令，将 **start** 替换为 **restart** 以使 `autofs` 重新读取这些文件。

## autofs：自动挂载的目录层次结构

**autofs** 目录层次结构与其他目录层次结构类似，但在需要之前保持未挂载状态，届时系统会自动挂载它（*按需挂载*）。当不再需要 **autofs** 目录层次结构时，系统会将其卸载——默认情况下，在五分钟不活动之后。自动挂载的目录层次结构是以一致方式管理大量系统的重要组成部分。**automount** 守护程序在安装包含大量服务器或大量目录层次结构时特别有用。它还有助于消除服务器之间的依赖关系（下文）。

当启动使用传统基于 fstab 挂载且 NFS 服务器宕机的系统时，由于等待服务器超时，系统可能需要很长时间才能启动。同样，当有两个服务器，每个都从另一个挂载目录层次结构，并且两个系统都宕机时，在启动过程中，当每个系统都试图从另一个系统挂载目录层次结构时，两个系统都可能挂起。这种情况称为 *服务器间依赖*。**automount** 功能通过仅在进程尝试访问目录层次结构时才从另一个系统挂载它，从而避免了这些问题。

- **服务器间依赖**

当进程尝试访问未挂载的 **autofs** 目录层次结构内的文件之一时，内核通知 **automount** 守护程序，该守护程序随后挂载目录层次结构。您必须给出一个访问 **autofs** 挂载点（在这种情况下为 **/home/zach**）的命令，例如 `cd /home/zach`，以创建促使 **automount** 挂载 **autofs** 目录层次结构的请求；只有在那时，系统才能显示或使用 **autofs** 目录层次结构。在您发出此 `cd` 命令之前，zach 不会出现在 **/home** 中。

控制 **automount** 行为的主要文件是 **/etc/auto.master**。此文件中的每一行描述一个挂载点，并引用指定要挂载在挂载点上的目录的 **autofs** 映射。一个简单的例子如下：

```
$ cat /etc/auto.master
/-      /etc/auto.misc --timeout=60
/plum   /etc/auto.plum
```

- **挂载点**

**auto.master** 文件有三列。第一列指定 **autofs 挂载点**的父目录——即要挂载 **autofs** 目录层次结构的位置。第一列中的 `/-` 表示挂载点是根目录。

- **映射文件**

第二列指定称为 *映射文件* 的文件，该文件存储补充配置信息。可选的第三列保存 **autofs** 映射条目的选项。在上面的例子中，第一行将超时时间（目录未使用时保持挂载的时间长度）设置为 60 秒；默认超时时间是 600 秒。您可以在 **/etc/sysconfig/autofs** 中更改 **autofs** 的默认值。

虽然映射文件可以有任何名称，但其中一个传统上命名为 **auto.misc**。以下是前一个 **auto.master** 文件中指定的两个映射文件：

```
$ cat /etc/auto.misc
/music        -fstype=ext4     :/dev/mapper/fedora-music
/home/zach    -fstype=nfs4    plum:/home/zach

$ cat /etc/auto.plum
public        -fstype=nfs4    plum:/home/public
```

| 类型 | 描述 |
| :--- | :--- |
| 相对挂载点 | 映射文件的第一列保存绝对或相对 autofs 挂载点。出现在 auto.master 第一列中除 / 以外的路径名指定了相对 autofs 挂载点。相对挂载点将附加到 auto.master 第一列中对应的 autofs 挂载点。在此例中，public（来自 auto.plum）附加到 /plum（来自 auto.master）形成 /plum/public。 |
| 绝对挂载点 | 出现在 auto.master 第一列中的 / 指定了绝对 autofs 挂载点。在此例中，auto.master 为 auto.misc 映射文件指定了 / 作为挂载点，因此该映射文件中指定的挂载点是绝对的，并完全在 auto.misc 映射文件中指定。auto.misc 文件指定了 autofs 挂载点 /music 和 /home/zach。 |

第二列保存 autofs 选项，第三列显示要挂载的服务器和目录层次结构。

auto.misc 文件指定了本地文件系统（/dev/mapper/vg_guava-music；一个 LV（第 44 页））和远程 NFS 目录（plum/home/zach）。您可以通过冒号前没有系统名称以及通常的 ext4 文件系统类型来识别本地目录层次结构。远程目录层次结构文件系统的冒号前出现系统名称，且文件系统类型始终为 nfs4。

在新的设置能够工作之前，您必须重启 autofs 服务（第 821 页）。此过程会在必要时创建保存挂载点的目录。

以下示例从 automount 守护程序（autofs 服务）未运行开始。第一个 ls 命令显示 /music 和 /plum 目录是空的。下一条命令以 root 权限运行，启动 autofs 服务。现在当您列出 /music 时，autofs 会挂载它，ls 显示其内容。/plum 的列表显示为空：它不是一个 autofs 挂载点。

```bash
$ ls /music /plum
/music:
/plum:

$ su -c 'systemctl start autofs.service'

$ ls /music /plum
/music:
lost+found mp3 ogg
/plum:

$ ls /plum/public
memos personal
$ ls /plum
public
```

当您给出 ls 命令并指定挂载点（/plum/public）时，automount 会挂载它，ls 显示其内容。一旦 public 挂载在 /plum 上，ls /plum 显示 public 目录已就位。

