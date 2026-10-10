
## 启动 nfsd 守护进程

出于安全考虑，Fedora 系统默认关闭 NFS 服务。你可以使用 `chkconfig` 命令开启 NFS 服务，以便在系统启动时导出文件并运行 `nfsd` 守护进程。

为了让 NFS 服务正常工作，你需要开启两个启动脚本。`nfs` 服务用于导出文件系统（来自 `/etc/exports`）并启动监听服务请求的 `nfsd` 守护进程。`nfslock` 服务则启动 `lockd` 守护进程，它有助于通过文件锁定防止通过网络对关键文件进行多重并发使用。

> 注意：如果你看到“Cannot register service: RPC: Unable to receive; errno = connection refused”的消息，你可能需要在客户端机器上启动 portmap 服务。

你可以输入以下命令（以 root 用户身份）使用 `chkconfig` 命令来开启 `nfs` 服务：

```
# chkconfig nfslock on; chkconfig nfs on
```

下次启动计算机时，NFS 服务将自动启动，你导出的目录也将可用。如果你希望立即启动服务而不必等待重启，可以输入以下命令：

```
# service nfslock start; /etc/init.d/nfs start
```

此时，NFS 服务应该正在运行，并准备好与网络中的其他计算机共享目录。

## 使用 NFS 文件系统

当服务器使用 NFS 通过网络导出目录后，客户端计算机使用 `mount` 命令将该目录挂载到其自身的文件系统上。`mount` 命令与用于从本地硬盘、CD 和 USB 闪存驱动器挂载文件系统的命令相同。唯一不同的是传递给 `mount` 的选项略有差异。

就像处理本地磁盘一样，添加到 `/etc/fstab` 文件中的 NFS 目录可以由 `mount` 在启动时自动挂载。NFS 目录也可以以不被自动挂载的方式添加到 `/etc/fstab` 文件中。使用 `noauto` 选项时，`/etc/fstab` 中列出的 NFS 目录在系统启动并运行后保持非活动状态，直到使用 `mount` 命令挂载该文件系统。

## 手动挂载 NFS 文件系统

如果你知道网络中某台计算机上的目录已被导出（即可供挂载），你可以使用 `mount` 命令手动挂载该目录。这是在将其设置为永久挂载之前，确保其可用且正常工作的好方法。以下是从名为 maple 的计算机上挂载 `/home/chris/files` 目录到你本地计算机的示例：

```
# mkdir /mnt/maple
# mount maple:/home/chris/files /mnt/maple
```

第一个命令 (mkdir) 创建挂载点目录（/mnt 是放置临时挂载磁盘和 NFS 文件系统的常见位置）。然后，mount 命令通过冒号分隔来识别远程计算机和共享文件系统（maple:/home/chris/files）。接着，跟上本地挂载点目录（/mnt/maple）。

> **注意：** 如果挂载失败，请确保服务器上的 NFS 服务正在运行，且服务器的防火墙规则没有拒绝访问该服务。在服务器上输入 `ps ax | grep nfsd`。你应该能看到 nfsd 服务器进程的列表。如果没有，请尝试按照上一节所述启动你的 NFS 守护进程。要查看你的防火墙规则，请输入 `iptables -L`（关于防火墙的描述请参见第 13 章）。默认情况下，nfsd 守护进程监听端口号 2049 上的 NFS 请求。你的防火墙必须接受端口 2049 (nfs) 和 111 (rpc) 上的 udp 请求。此外，在 `/etc/sysconfig/nfs` 文件中为相关的 NFS 服务设置静态 NFS 端口，并确保这些端口也是开放的。

为了确保挂载成功，请输入 `mount`。此命令会列出所有已挂载的磁盘和 NFS 文件系统。以下是 mount 命令及其输出的示例：

```
# mount | grep nfs
/dev/sda3 on / type ext3 (rw)
none on /proc type proc (rw)
none on /sys type sysfs (rw)
none on /dev/pts type devpts (rw,gid=5,mode=620)
usbdevfs on /proc/bus/usb type usbdevfs (rw)
/dev/sda1 on /boot type ext3 (rw)
none on /dev/shm type tmpfs (rw)
maple:/home/chris/files on /mnt/maple type nfs (rw,addr=10.0.0.11)
```

mount 命令的输出显示了你的已挂载磁盘分区、特殊文件系统和 NFS 文件系统。第一行输出显示你的硬盘 (/dev/sda3)，挂载在根文件系统 (/) 上，具有读/写权限 (rw)，文件系统类型为 ext3（标准的 Linux 文件系统类型）。小的 /boot 文件系统也是 ext3 类型。/proc、/sys、/dev/shm、/dev/pts 和 /usr/usb 文件挂载点代表特殊的文件系统类型。刚刚挂载的 NFS 文件系统是来自 maple 的 /home/chris/files 目录（maple:/home/chris/files）。它挂载在 /mnt/maple 上，挂载类型为 nfs。该文件系统是以读/写方式 (rw) 挂载的，并且 maple 的 IP 地址是 10.0.0.11 (addr=10.0.0.11)。

我刚才展示了一个使用 mount 和 NFS 的简单案例。这种挂载是暂时的，重启计算机时不会重新挂载。你也可以为 NFS 挂载的 mount 命令行添加选项：

- `-a` — 挂载 `/etc/fstab` 中的所有文件系统（不包括标记为 `noauto` 的那些）。
- `-f` — 模拟执行（伪造）挂载命令行中（或 `/etc/fstab` 中）的文件系统的动作。与 `-v` 选项一起使用时，`-f` 对于在 mount 实际执行前查看它会做什么很有用。
- `-P` — 当与 `-a` 一起使用时，你告诉 mount 为 `/etc/fstab` 文件中列出的每个待挂载文件系统分派一个新的 mount 进程实例。使用此选项的一个优势（就 NFS 共享目录而言）是，如果某个 NFS 文件系统无法立即获取，其他文件系统仍然可以挂载。然而，如果挂载顺序很重要（例如，你需要先挂载 `/mnt/pco` 然后挂载 `/mnt/pco/axctic`），则不应使用此选项。
- `-r` — 以只读方式挂载文件系统。
- `-w` — 以读/写方式挂载文件系统。（为此，共享文件系统必须以读/写权限导出。）

下一节描述如何使挂载更加持久（使用 `/etc/fstab` 文件）以及如何选择各种 NFS 挂载选项。

## 自动挂载 NFS 文件系统

为了设置每次启动 Fedora 系统时自动挂载 NFS 文件系统，你需要为该 NFS 文件系统添加一个条目到 `/etc/fstab` 文件中。`/etc/fstab` 文件包含关于你的 Fedora 系统所有不同类型已挂载（以及可供挂载）文件系统的信息。

在本地系统中添加 NFS 文件系统的格式如下：

```
host:directory  mountpoint  nfs  options  0  0
```

第一项 (*host:directory*) 标识 NFS 服务器计算机和共享目录。*mountpoint* 是本地挂载点，NFS 目录将挂载在此处，随后是文件系统类型 (*nfs*)。与挂载相关的任何选项接下来以逗号分隔的列表形式出现。（最后两个零只是告诉 Fedora 不要对该文件系统的 `dump` 备份内容，并且不要对该文件系统运行 `fsck`。）

> 注意：`/etc/fstab` 中系统创建的硬盘挂载条目可能会显示 UUID（通用标识符），而不是 *host:directory* 条目——例如，`UUID=8366237bb-d845-4117-a1b2-e286d056f15`。你可以在 `/dev/disk/by-uuid` 下查看这些条目。

以下是 `/etc/fstab` 中两个 NFS 条目的示例：

```
maple:/home/chris/files  /mnt/maple  nfs  size=8192,wsize=8192  0  0
oak:/apps  /oak/apps  nfs  noauto,ro  0  0
```

在第一个示例中，名为 **maple** 的计算机上的远程目录 `/home/chris/files` (`maple:/home/chris/files`) 被挂载到本地目录 `/mnt/maple`（本地目录必须已经存在）。文件系统类型是 **nfs**，并且**读** (`rsize`) 和**写** (`wsize`) 缓冲区大小被设置为 **8192**，以加速与此连接相关的数据传输。在第二个示例中，名为 **oak** 的计算机上的远程目录是 `/apps`。它被设置为一个可以挂载到本地 `/oak/apps` 目录的 **NFS** 文件系统 (`nfs`)。该文件系统**不会**自动挂载 (`noauto`)；但是，在系统运行后，只能使用 **mount** 命令以**只读** (`ro`) 方式挂载它。

> **提示：** 默认情况下，NFS 文件系统以读/写方式挂载。但是，导出文件系统的默认方式是只读。如果你无法写入 NFS 文件系统，请检查它是否已从服务器以读/写方式导出。

## 挂载 noauto 文件系统

在你的 `/etc/fstab` 文件中，还可以包含其他不会自动挂载的文件系统的设备。例如，你可能在硬盘上有多个磁盘分区，或者有一个你只想偶尔挂载的 NFS 共享文件系统。可以手动挂载 **noauto** 文件系统。其优点在于，当你输入 **mount** 命令时，你可以输入较少的信息，其余内容由 `/etc/fstab` 文件的内容填充。因此，例如，你可以输入：

```
# mount /oak/apps
```

使用此命令，**mount** 知道检查 `/etc/fstab` 文件以获取要挂载的文件系统 (`oak:/apps`)、文件系统类型 (**nfs**) 以及要使用的 **mount** 选项（在这种情况下是**只读**的 `ro`）。代替输入本地挂载点 (`/oak/apps`)，你也可以输入远程文件系统名称 (`oak:/apps`)，让其他信息被填充。

> **提示：** 在命名挂载点时，在该名称中包含远程 NFS 服务器的名称有助于你记住文件实际存储在哪里。如果你正在共享主目录 (`/home`) 或邮件目录 (`/var/spool/mail`)，这可能无法实现。

## 使用 mount 选项

你可以向 `/etc/fstab` 文件（或 **mount** 命令行本身）添加多个 **mount** 选项，以影响文件系统的挂载方式。当你向 `/etc/fstab` 添加选项时，它们必须用逗号分隔。以下是一些对于挂载 NFS 文件系统很有价值的选项：

- `hard` - 开启此选项后，如果 NFS 服务器在进程等待访问它时断开连接或宕机，该进程将挂起直到服务器恢复。如果你正在处理的数据至关重要，且不能与访问它的程序不同步，此选项很有帮助。（这是默认行为。）

