
# 第 18 章：设置文件服务器

## NIS 组

`NIS groups` — 你可以允许包含 `NIS` 组中的主机访问。要指定 `NIS` 组，请在组名前面加上 `(@)` 符号（例如 `@group`）。

### `/etc/exports` 中的访问选项

当使用 `NFS` 导出目录时，并不非要直接提供文件和目录。在 `/etc/exports` 中每个条目的各个部分，你可以添加选项，通过设置读/写权限来允许或限制访问。传递给 `NFS` 的选项如下：

- `ro` — 仅允许客户端只读地挂载此导出的文件系统。默认是以读/写方式挂载文件。
- `rw` — 显式要求以读/写权限共享目录。（如果客户端选择，它仍然可以以只读方式挂载该目录。）

### `/etc/exports` 中的用户映射选项

除了定义如何处理权限的选项外，你还可以使用选项设置特定用户在 `NFS` 共享文件系统上的权限。

简化此过程的一种方法是在每台机器上使用具有相同用户名和 `UID` 的多个用户账户。这使得映射用户更容易，使得它们在挂载的文件系统上的权限与它们在本地硬盘上的文件权限相同。如果该方法不方便，可以通过多种方式映射 `UID`。设置用户权限的方法以及每种方法使用的 `/etc/exports` 选项如下：

- `root` 用户 — `root user` — 通常情况下，客户端的 `root` 用户被映射为 `nfsnobody` 用户名（`UID 65534`）。这防止了客户端的 `root` 用户更改共享文件系统中的所有文件。如果你想客户端的 `root` 用户在服务器上拥有权限，请使用 `no_root_squash` 选项。
- `nfsnobody` 用户/组 — `nfsnobody user/group` — 通过使用 `nfsnobody` 用户名和组名，你实际上创建了一个用户/组，其权限将允许任何用户访问（除非这些用户允许权限）。`nfsnobody` 用户被分配 `UIDs` 和 `GIDs` 为 `65534`。使用 `anoid` 选项可以更改 `nfsnobody` 用户或组。例如，`anoidid=175` 将匿名用户设置为 `175`，`anoidid=300` 将 `GID` 设置为 `300`。（只有在你列出权限时才会显示数字，除非你向 `/etc/password` 和 `/etc/group` 添加新的 `UIDs` 和 `GIDs`。）
- 用户映射 — `User mapping` — 如果一组计算机登录账户（并且它们具有相同的 `ID`），`NFS` 默认将映射这些 `ID`。这意味着如果用户...

# 第四部分：Fedora RHEL 网络与服务器设置

---

# 第 18 章：设置文件服务器

### 启动守护进程

出于安全考虑，`NFS` 服务在 `Fedora` 上默认是关闭的。你可以使用 `checkconfig` 命令开启 `NFS` 服务，以便在系统启动时导出文件。

有两个启动脚本需要开启以便 `NFS` 服务正常工作。`NFS` 服务导出文件并启动监听请求的 `nfsd` 守护进程。`lock` 服务启动 `lockd` 守护进程，允许文件锁定。

> 注意：如果你看到“Cannot register: RPC: Unable to receive; errno=connection refused”消息，你可能需要在客户端上启动 `portmap` 服务。

你可以通过输入以下命令（作为 `root`）开启 `NFS` 服务：

```
# chkconfig nfs on
```

下次重启计算机时，`NFS` 服务将自动启动，你的导出目录将可用。如果你想立即启动服务而不是等待重启，可以输入：

```
/etc/init.d/nfs start
```

`NFS` 服务现在应该运行并准备好共享目录。

### 使用 NFS 文件系统

当服务器使用 `NFS` 导出目录后，客户端计算机使用 `mount` 命令将该目录连接到自己的文件系统。`mount` 命令与挂载本地硬盘、`CD` 和 `USB` 闪存的命令相同。挂载选项略有不同。

`Mount` 可以自动检测添加到 `/etc/fstab` 中的 `NFS` 目录，就像处理本地磁盘一样。`NFS` 目录也可以通过某种方式添加到 `/etc/fstab`，使其不自动挂载。使用 `noauto` 选项，`/etc/fstab` 中出的 `NFS` 目录在系统启动后、使用 `mount` 命令之前处于非活动状态。

### 手动挂载 NFS 文件系统

如果你知道网络上某台计算机的目录已经导出（即已可以挂载），你可以使用 `mount` 命令手动挂载该目录。这是在设置之前确保其可用且正常工作的好方法。

### 永久挂载

以下是在本地计算机上从名为 `maple` 的计算机挂载 `/home/chris/files` 目录的示例：

```
# mkdir /mnt/maple
# mount maple:/home/chris/files /mnt/maple
```

第一条命令 (`mkdir`) 创建了挂载点目录（`/mnt` 是存放临时挂载目录和 `NFS` 文件系统的常用位置）。`mount` 命令通过冒号分隔符远程服务器和文件系统（`maple:/home/chris/files`）。接着是本地挂载点目录（`/mnt/maple`）。

> 注意：如果挂载失败，请确保服务器上的 `NFS` 服务正在运行，并且防火墙规则没有拒绝对该服务的访问。在服务器上执行 `ps ax | grep nfs`，你应该能看到一个 `nfs` 进程列表。如果没有，请按照上一节的描述启动你的 `nfs` 守护进程。要查看你的规则，请使用 `iptables -L`（防火墙的描述请参见第 14 章）。默认情况下，`nfs` 守护进程在端口 `2049` 上监听请求。你的防火墙必须接受端口 `2049` (`nfs`) 和 `111` (`rpc`) 的 `udp` 请求。此外，在 `/etc/sysconfig/nfs` 文件中为相关 `NFS` 服务设置静态 `NFS` 端口，并确保也打开这些端口。

要确保挂载已发生，请使用 `mount`。此命令列出所有已挂载的磁盘和 `NFS` 文件系统。以下是 `mount` 命令及其输出示例：

```
# mount grep nfs
/dev/sda3 on type ext3 (rw)
none on /proc type procfs (rw)
none on /dev/sys type sysfs (rw)
none on /dev/pts type devdevfs (rw,gid=5,mode=620) usbdevfs on
/proc/bus/usb type usbdevfs (rw)
/dev/sda on /boot type ext3 (rw)
none on /dev/shm type tmpfs (rw)
maple:/home/chris/files on /mnt/maple type nfs (rw,addr=10.0.0.11)
```
