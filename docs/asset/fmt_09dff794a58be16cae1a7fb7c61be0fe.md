
如果你的系统当前处于强制模式，请检查 `nfs_selinux` 手页，获取可能影响你 `vsftpd` 服务运行 SELinux 设置信息。以下是你可能需要了解的几个 NFS SELinux 文件上下文：

- `nfs_export_all_ro`：开启此布尔值后，SELinux 允许你使用 NFS 以只读权限共享文件。无论共享文件和目录的 SELinux 文件上下文如何，NFS 只读文件共享都因此此分配。
- `nfs_export_all_rw`：开启此布尔值后，SELinux 允许你使用 NFS 以读写权限共享文件。与上一个布尔值一样，无论共享文件和目录设置的文件上下文如何都有效。
- `use_nfs_home_dirs`：要允许 NFS 服务器通过 NFS 共享你的家目录，请将此布尔值设置为开启。

在这些布尔值，前两个是默认开启的。`use_nfs_home_dirs` 布尔值为关闭。若要关闭 `use_nfs_home_dirs` 目录，你可以输入：

```bash
# setsebool -P use_nfs_home_dirs on
```

然而，通过更改想要通过 NFS 共享的文件和目录的文件上下文，你可以忽略所有与 NFS 文件共享相关的布尔值。`public_content_t` 和 `public_content_rw_t` 文件上下文可以设置在任何你想要通过 NFS 共享（或 HTTP、FTP 等）的目录上。例如，要设置规则允许 `/whatever` 目录及其子目录通过 NFS 进行读写共享并应用该规则，请执行以下：

```bash
# semanage fcontext -a -t public_content_rw_t "whatever(/.*)*"
# restorecon -F -v /whatever
```

![](img/cc1e2b1a5739a47bac1a4c7cfac7c1a6_552_0.png)

## 第四部分：成为 Linux 服务器管理员

如果你只想让用户能够读取目录中的文件而不能写入，你可以转而将 `public_content_t` 文件上下文分配给目录。

### 使用 NFS 文件系统

在服务器通过 NFS 在网络上导出一个目录后，客户端计算机使用 `mount` 命令将该目录连接到它自己的文件系统。这与挂载硬盘、DVD 和 USB 驱动器上的文件系统使用的是相同的命令，但选项略有不同。

`mount` 命令允许客户端将 NFS 目录自动挂载到 `/etc/fstab` 文件中，就像处理本地磁盘一样。NFS 目录也可以被添加到 `/etc/fstab` 文件中，但使其不自动挂载（这样你可以在需要时手动挂载）。通过 `noauto` 选项，`/etc/fstab` 将处于非活动状态，直到在系统启动后使用 `mount` 命令挂载文件系统为止。

除了 `/etc/fstab` 文件外，你还可以使用 `/etc/nfs-mount.conf` 文件设置挂载选项。在该文件中，你可以设置适用于任何 NFS 目录的挂载选项，或仅适用于与特定挂载点或 NFS 服务器关联的目录。

在你开始挂载共享目录之前，可能可能想先使用 `showmount` 命令检查通过 NFS 可用的共享目录有哪些。

### 查看 NFS 共享

从客户端 Linux 系统，你可以使用 `showmount` 命令查看从选定计算机提供的可用共享目录如下例所示：

```bash
$ showmount -e server.example.com
/export/myshare client.example.com
/mnt/public *
```

`showmount` 的输出显示名为 `/export/myshare` 的共享目录仅对主机 `client.example.com` 可用。然而，`/mnt/public` 共享目录对所有人可用。

### 手动挂载 NFS 文件系统

当你知道网络上某台计算机的目录已经导出（即已可以挂载）后，你可以使用 `mount` 命令手动挂载它。这是在将其设置为永久挂载之前确保其可用且运行良好的良好方法。以下是从你的本地计算机向名为 `maple` 的计算机挂载 `/stuff` 目录的示例：

```bash
# mkdir /mnt/maple
# mount maple:/stuff /mnt/maple
```

第一条命令 (`mkdir`) 创建挂载点目录（`/mnt` 是放置临时挂载磁盘和 NFS 文件系统的常用位置）。`mount` 命令识别远程计算机和共享文件系统，并用冒号分隔（`maple:/stuff`），随后是本地挂载点目录（`/mnt/nfs`）。

> 注意：如果挂载失败，请确保 NFS 服务正在运行，并且服务器的防火墙规则没有阻止对服务的访问。在服务器上，输入 `ps ax | grep nfsd` 查看 `nfsd` 进程列表。如果你没有看到列表，请按照本章描述启动你的 NFS 守护进程。要查看规则，输入 `iptables -vnl`。默认情况下，nfs 守护进程在端口号 2049 上监听 NFS 请求。你的防火墙必须接受端口 2049 (`nfs`) 和 111 (`rpc`) 上的 udp 请求。在 Red Enterprise Linux 6 及早版本的 Fedora 中，你需要为相关服务设置静态端口，然后在防火墙中打开这些服务的端口。请参考本章前面的“保护你的 NFS 服务器”部分回顾如何解决这些安全问题。

为了确保挂载发生，使用 `mount -t nfs4`。此命令列出所有已挂载的文件系统。这里是命令及其输出的示例（未讨论的文件系统已编辑）：

```bash
# mount -t nfs4
192.168.122.240:/mnt on /mnt/fedora nfs4
(rw,relime,vers=4.2,size=262144)
```

输出显示 `192.168.122.240:/mnt` 已通过 `nfs4` 挂载到 `/mnt/fedora`。`(rw,relime,vers=4.2,size=262144)` 表示选项。`mount` 命令列出所有已挂载的文件系统。（注：此处原文存在重复，译文已按要求处理）

# 第 20 章：配置 NFS 服务器

提示
在命名挂载点时，名称中包含远程 NFS 服务器的名字可以帮助你记住文件实际存储在何处。如果你共享家目录 (`/home`) 或邮件目录 (`/var/spool/mail`)，这可能无法实现。例如，你可能将来自名为 `duck` 的机器上的文件系统挂载到目录 `/mnt/duck` 上。

## 使用挂载选项

你可以向 `/etc/fstab` 文件（或命令行本身）添加多个挂载选项，以影响文件系统的挂载方式。在 `/etc/fstab` 中添加选项时，必须用逗号隔开。例如，这里在挂载 `oak:/apps` 时使用了 `noauto`、`ro` 和 `hard` 选项：

```
oak:/apps  nfs  noauto, ro, hard  0 0
```
