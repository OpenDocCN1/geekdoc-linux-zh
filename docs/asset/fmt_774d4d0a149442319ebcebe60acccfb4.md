
`mount` 命令的输出显示了你挂载的磁盘、分区文件系统和 NFS 文件系统。第一行输出显示了你的硬盘（`/dev/sda3`），挂载在根文件系统（`/`）上，具有读写权限（`rw`），文件系统类型为 `ext3`（标准的 Linux 系统类型）。较小的 `/boot` 文件系统也是 `ext3` 类型。`/proc`、`/sys`、`/dev/shm`、`/dev/pts` 和 `usbdevfs` 挂载点代表特殊文件类型。挂载的 NFS 文件系统是 `maple` 的 `/home/chris/files` 目录（`maple:/home/chris/files`）。它挂载在 `/media/maple` 上，类型为 `nfs`。该文件系统以读写（`rw`）模式挂载，`map` 的 IP 地址为 `10.0.0.11`。

我刚刚展示了一个使用 NFS 的简单案例。该挂载是临时的，当你重启计算机时不会重新挂载。你也可以为 NFS 的 `mount` 命令添加选项：

- `-a` 挂载 `/etc/fstab` 中的所有文件系统（标记为 `noauto` 的除外）。
- `-f` — 这在命令行上（或在 `/etc/fstab` 中）执行（模拟）挂载文件系统的动作。配合 `-v` 选项使用时，`-f` 用于在实际执行之前查看挂载将执行的操作。
- `-F` 当配合 `-a` 使用时，你告诉 `mount` 为 `/etc/fstab` 中列出的每个文件系统派生（fork）一个新的 `mount` 实例。使用此选项（涉及 NFS 共享目录）的优点是，如果 NFS 文件系统无法立即可用，可以挂载其他文件系统。然而，如果挂载顺序很重要，则不应使用此选项（例如，如果你需要挂载 `/mnt/pcs/arctic`）。
- `-r` 以只读模式挂载文件系统。
- `-w` 以读写模式挂载文件系统。（要使此项生效，共享文件系统必须已以读写权限导出）

下一节将描述如何使挂载更具持久性（使用 `/etc/fstab` 文件）以及如何为 NFS 挂载选择各种选项。

# 第 18 章：设置文件服务器

## 自动挂载 NFS 文件系统

为了在每次启动 Fedora 或 RHEL 系统时自动挂载 NFS 文件系统，你需要在 `/etc/fstab` 文件中为 NFS 文件系统添加条目。`/etc/fstab` 文件包含了关于你的 Fedora 或 RHEL 系统所有不同类型的已挂载（以及可挂载）文件系统的信息。

将 NFS 文件系统添加到本地系统中的格式如下：

```
host:directory mountpoint nfs options 0 0
```

第一项（`host:directory`）识别 NFS 服务器计算机和共享目录。`mountpoint` 是挂载 NFS 目录的本地挂载点，随后是文件类型（`nfs`）。任何与挂载相关的选项将以逗号分隔列表的形式出现在后面。（最后的两个 0 只是告诉 Fedora 或 RHEL 不要转储（dump）文件系统的内容，并且不对文件系统运行 `fsck`）。

以下是 `/etc/fstab` 中 NFS 条目的两个示例：

```
maple:/home/chris/files /media/maple nfs size=8192,wsize=8192 0 0
o:/apps /oak/apps nfs noauto,ro 0 0
```

在第一个示例中，来自名为 `maple` 的计算机的远程目录 `/home/chris/files`（`/home/chris/files`）被挂载在本地目录 `/media/maple` 上（本地目录必须存在）。文件类型是 `nfs`，读（`size`）和写（`wsize`）设置为 `8192`。在第二个示例中，远程目录 `o:/apps` 被挂载在 `/oak/apps`，选项为 `noauto,ro`。

## Autofs 按需挂载 NFS 文件系统

自动检测和移除设备的改进意味着你只需插入或连接设备即可对其进行检测、挂载和显示。然而，要让检测和移除远程 NFS 文件系统自动化，仍然需要使用如 `autofs` 这样的设施。

配置并开启 `autofs` 后，你可以缓存任何共享目录以按需挂载。如果你知道另一主机共享的主机名和目录，只需切换到默认 `autofs` 挂载目录（`/net`），共享资源就会自动挂载并供你访问。

以下步骤说明了如何开启 `autofs` 设施：

1. 在终端窗口中以 `root` 用户身份打开 `/etc/auto.master` 文件，并查找如下所示的行：

```
/net -hosts
```

这使得 `/net` 目录作为你要在网络上访问的 NFS 共享目录的挂载点。（如果该行开头有注释字符，请将其删除。）

2. 以 `root` 用户身份输入以下命令启动 `autofofs` 服务：

```
# service autofofs start
```

3. 设置 `autofofs` 在每次启动系统时自动重启：

```
# chconfig autofofs on
```

信不信由，你只需要做这些操作就了。只要你到你想要共享目录的 NFS 服务器有网络连接，你就可以尝试访问共享的 NFS 目录。例如，如果你知道网络上名为 `shuttle` 的电脑共享了 `/usr/local/share` 目录，请执行以下操作：

+ 1. 输入以下内容：

```
$ cd /net/shuttle
```

如果名为 `shuttle` 的电脑有任何你可用的共享目录，你将能够成功切换到该目录。另外需要注意的是的是，你可以使用 IP 地址而不是主机名（例如 `cd /net/10.0.0.1`）。

+ 2. 输入以下内容：

```
$ ls
```

`usr`

你应该能看到 `usr` 目录是共享目录路径的一部分。如果其他顶级目录下也有共享目录，你也应该看到它们（例如 `/var` 或 `/home`）。当然，能否看到其中任何目录取决于服务器上的安全设置。

+ 3. 接下来，你可以直接进入共享目录。例如：

```
$ cd /net/shuttle/usr/local/share
$ ls
```

`info manic television`

此时，`ls` 应该显示名为 `shuttle` 的电脑上 `/usr/local/share` 目录的内容。你对这些内容可以做什么取决于服务器如何配置这些内容进行共享。

## 卸载 NFS 文件系统

在挂载 NFS 文件系统后，卸载它是非常简单的。你使用 `umount` 命令，并配合本地挂载点或远程文件系统名称。例如，这里有两种从本地目录卸载 `maple:/home/chris/files` 的方法：

```
# umount maple:/home/chris/files
# umount /media/maple
```
