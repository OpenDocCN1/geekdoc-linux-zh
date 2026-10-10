
# 启动 nfsd 守护进程

出于安全考虑，Fedora 或 RHEL 系统中的 NFS 服务默认处于关闭状态。你可以使用 `chkconfig` 命令来启用 NFS 服务，以便系统在启动时导出文件并运行 `nfsd` 守护进程。

为了使 NFS 服务正常工作，你需要运行两个启动脚本。NFS 服务负责导出文件系统（来自 `/etc/exports`）并启动监听服务请求的 `nfsd` 守护进程。`nfslck` 服务则启动 `lockd` 守护进程，该守护进程有助于实现文件锁定，以防止通过网络对关键文件进行多个同时使用。

> **注意：** 如果你看到“无法注册服务：RPC：无法接收；errno = 连接被拒绝”的消息，你可能需要在客户端机器上启动 portmap 服务。

你可以通过键入以下命令（作为 root 用户）使用 `chkconfig` 命令来开启 nfs 服务：

```
# chkconfig nfs on
```

下次启动计算机时，NFS 服务将自动启动，你导出的目录也将变得可用。如果你想立即启动服务而无需等待重启，可以键入以下内容：

```
# /etc/init.d/nfs start
```

此时，NFS 服务应该正在运行，并准备好与你网络中的其他计算机共享目录。

# 使用 NFS 文件系统

当服务器使用 NFS 通过网络导出目录后，客户端计算机使用 `mount` 命令将该目录连接到其自身的文件系统。`mount` 命令与用于从本地硬盘、CD 和软盘挂载文件系统的命令是相同的。仅用于 `mount` 的选项略有不同。

Mount 可以自动挂载添加到 `/etc/fstab` 文件中的 NFS 目录，就像它处理本地磁盘一样。NFS 目录也可以以不会自动挂载的方式添加到 `/etc/fstab` 文件中。通过 `noauto` 选项，列在 `/etc/fstab` 中的 NFS 目录在系统启动并运行后，在用于挂载文件系统之前是处于非活动状态的。

# 手动挂载 NFS 文件系统

如果你知道网络中某台计算机上的目录已被导出（即已准备好供挂载），你可以使用 `mount` 命令手动挂载该目录。这是在将其设置为永久挂载之前，确保其可用且运行良好的好方法。以下是挂载名为 maple 的计算机上的 /home/chris/files 目录到你本地计算机的示例：

```
# mkdir /media/maple
# mount maple:/home/chris/files /media/maple
```

第一个命令（mkdir）创建挂载点目录（/media 是放置临时挂载磁盘和 NFS 文件系统的常见位置）。mount 命令随后通过冒号标识远程计算机和共享文件系统（maple:/home/chris/files）。然后，本地挂载点目录跟随其后（/media/maple）。

> **注意：** 如果挂载失败，请确保服务器上的 NFS 服务正在运行，且服务器的防火墙规则未拒绝对该服务的访问。从服务器端，键入 `ps ax | grep nfsd`。你应该能看到 `nfsd` 服务器进程列表。如果没有，请尝试按照上一节所述启动你的 NFS 守护进程。要查看防火墙规则，键入 `iptables -L`（有关防火墙的描述，请参见第 14 章）。默认情况下，`nfsd` 守护进程在端口号 2049 上监听 NFS 请求。你的防火墙必须接受端口 2049 (nfs) 和 111 (rpc) 上的 udp 请求。

为了确保挂载成功，请键入 `mount`。此命令列出所有已挂载的磁盘和 NFS 文件系统。以下是 `mount` 命令及其输出的示例：

```
# mount
/dev/sda3 on / type ext3 (rw)
none on /proc type proc (rw)
none on /sys type sysfs (rw)
none on /dev/pts type devpts (rw,gid=5,mode=620) usbdevfs on
/proc/bus/usb type usbdevfs (rw)
/dev/sda1 on /boot type ext3 (rw)
none on /dev/shm type tmpfs (rw)
maple:/home/chris/files on /media/maple type nfs (rw,addr=10.0.0.11)
```

mount 命令的输出显示了你已挂载的磁盘分区、特殊文件系统和 NFS 文件系统。第一行输出显示你的硬盘（/dev/sda3），挂载在根文件系统（/）上，具有读写权限（rw），文件系统类型为 ext3（标准的 Linux 文件系统类型）。小型的 /boot 文件系统也是 ext3 类型。/proc、/sys、/dev/pts 和 usbdevfs 挂载点代表特殊类型文件系统。刚刚挂载的 NFS 文件系统是来自 maple 的 /home/chris/files 目录（maple:/home/chris/files）。它挂载在 /media/maple 上，其挂载类型为 nfs。该文件系统以读写模式（rw）挂载，且 maple 的 IP 地址为 10.0.0.11（addr=10.0.0.11）。

我刚才展示的是使用 mount 配合 NFS 的简单情况。这种挂载是临时的，在你重启计算机时不会重新挂载。你还可以为 NFS 挂载的 mount 命令行添加选项：

-   `-a` — 挂载 /etc/fstab 中的所有文件系统（除了标记为 noauto 的那些）。
-   `-f` — 模拟（fakes）挂载命令行（或 `/etc/fstab`）中文件系统的操作。与 -v 选项一起使用时，-f 用于在实际执行之前查看 mount 将要执行的操作。
-   `-F` — 当与 -a 一起使用时，你告诉 mount 为列在 `/etc/fstab` 文件中待挂载的每个文件系统派生（fork off）一个新的 mount 实例。使用此选项的一个优点是，对于 NFS 共享目录，如果某个 NFS 文件系统不可立即用，其他文件系统仍可以被挂载。但是，如果挂载顺序很重要（例如，如果你需要先挂载 `/mnt/pcg` 然后挂载 `/mnt/pcg/arctic`），则不应使用此选项。
-   `-r` — 以只读模式挂载文件系统。
-   `-w` — 以读写模式挂载文件系统。（要实现这一点，共享文件系统必须已以读写权限导出。）

下一节将描述如何使挂载更加永久（使用 `/etc/fstab` 文件）以及如何为 NFS 挂载选择各种选项。

# 自动挂载 NFS 文件系统

要设置 NFS 文件系统以便每次启动 Fedora 或 RHEL 系统时自动挂载，你需要为该 NFS 文件系统向 `/etc/fstab` 文件添加一个条目。`/etc/fstab` 文件包含有关 Fedora 或 RHEL 系统所有不同类型的已挂载（以及可挂载）文件系统的信息。

向本地系统添加 NFS 文件系统的格式如下：

```
host:directory  mountpoint  nfs  options    0   0
```

第一项（host:directory）标识 NFS 服务器计算机和共享目录。mountpoint 是挂载 NFS 目录的本地挂载点，后面跟着文件系统类型（nfs）。与挂载相关的任何选项接着以逗号分隔的列表形式出现。（最后两个零只是告诉 Fedora 或 RHEL 不要转储文件系统的内容，也不要在文件系统上运行 fsck。）

以下是 `/etc/fstab` 中两个 NFS 条目的示例：

```
maple:/home/chris/files /media/maple nfs rsize=8192,wsize=8192 0 0
oak:/apps       /oak/apps     nfs         noauto,ro  0 0
```

在第一个示例中，名为 maple 的计算机上的远程目录 `/home/chris/files`（maple:/home/chris/files）被挂载到本地目录 /media/maple（本地目录必须已存在）。文件系统类型为 nfs，并且读取（rsize）和写入（wsize）缓冲区大小设置为 8192，以加速与此连接相关的数据传输。在第二个示例中，是名为 oak 的计算机上的远程目录 /apps。它被设置为一个可以在本地 /oak/apps 目录上挂载的 NFS 文件系统（nfs）。然而，此文件系统不会自动挂载（noauto），并且只能在系统已经运行之后，使用 `mount` 命令以只读方式（ro）挂载。

> **提示：** 默认情况下，NFS 文件系统以 `read/write`（读写）方式挂载。但是，导出文件系统的默认设置是 `read-only`（只读）。如果你无法写入 NFS 文件系统，请检查它是否已从服务器导出为 `read/write`（读写）。

## 挂载 noauto 文件系统

在你的 `/etc/fstab` 文件中，也可能包含其他不自动挂载的文件系统设备。例如，你的硬盘上可能有多个磁盘分区，或者你可能想要偶尔才挂载的 NFS 共享文件系统。`noauto` 文件系统可以手动挂载。其优点在于，当你键入 `mount` 命令时，你可以键入较少的信息，其余部分将由 `/etc/fstab` 文件的内容填充。因此，例如，你可以键入：

```
# mount /oak/apps
```

使用此命令，`mount` 知道要检查 `/etc/fstab` 文件以获取要挂载的文件系统（`oak:/apps`）、文件系统类型（`nfs`）以及要与 `mount` 一起使用的选项（在这种情况下是 `ro` 表示只读）。代替键入本地挂载点（`/oak/apps`），你也可以键入远程文件系统名称（`oak:/apps`），让其他信息自动填充。

> **提示：** 在命名挂载点时，在名称中包含远程 NFS 服务器的名称可以帮助你记住文件实际存储在哪里。如果你正在共享主目录（`/home`）或邮件目录（`/var/spool/mail`），这可能无法实现。

## 使用 mount 选项

你可以向 `/etc/fstab` 文件（或 `mount` 命令行本身）添加多个 `mount` 选项，以影响文件系统的 `mounted`（挂载）方式。当你向 `/etc/fstab` 添加选项时，它们必须用逗号分隔。以下是一些对挂载 NFS 文件系统有价值的选项：

-   `hard` — 开启此选项时，如果在进程等待访问 NFS 服务器期间服务器断开连接或宕机，该进程将挂起（hang），直到服务器恢复。如果在处理数据时，确保数据与访问它的程序保持同步至关重要，那么这个选项很有帮助。（这是默认选项。）
-   `soft` — 如果 NFS 服务器断开连接或宕机，开启此选项时，试图从服务器访问数据的进程会在经过设定的超时时间后超时。
-   `rsize` — 从 NFS 服务器一次读取的数据字节数。默认值是 `1024`。使用较大的数字（例如 `8192`）在快速且相对无错（即没有太多噪声或冲突）的网络（例如局域网）上可获得更好的性能。
