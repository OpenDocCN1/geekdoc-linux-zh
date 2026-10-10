
`mount` 命令的输出显示了你的磁盘分区、文件系统和 NFS 文件系统。第一行输出显示了你的硬盘（`/dev/sda3`），挂载在根文件系统（`/`）上，具有读写权限 (`rw`)，文件类型为 `ext3`（标准 Linux 文件系统）。较小的 `/boot` 文件系统也是 `ext3`。`/proc`、`/sys`、`/dev`、`/pts` 和 `usbdevfs` 点代表特殊的文件系统类型。刚挂载的 NFS 文件系统是 maple 的 `/home/chris/files` 目录（`maple:/home/chris/files`）。它被挂载在 `/mnt/maple` 上，类型为 `nfs`。该文件系统以读写 (`rw`) 模式挂载，maple 的 IP 地址为 10.0.0.11。

我展示了一个使用 `mount` 挂载 NFS 的简单案例。当你重启计算机时，挂载不会重新挂载。你也可以为 NFS 挂载的 `mount` 命令添加选项：

# 第 18 章：设置文件服务器

- `-a` 挂载 `/etc/fstab` 中的所有文件系统（除标记为 `noauto` 的项外）。
- `-f` 在命令行（或在 `/etc/fstab` 中）执行（伪）挂载文件系统的动作。与 `-v` 选项配合使用时，`-f` 用于在实际执行前查看将执行的操作。
- `-F` 与 `-a` 使用时，你告诉 `mount` 为 `/etc/fstab` 中列出的每个待挂载文件系统创建一个新的 mount 实例。对于 NFS 共享目录，使用此选项的优势是，如果 NFS 文件系统无法立即可用，可以挂载其他文件系统。然而，如果挂载顺序很重要，则不应使用此选项（例如，如果你需要挂载 `/mnt/pcs` 然后挂载 `/mnt/pcs/arctic`）。
- `-r` 以只读模式挂载文件系统。
- `-w` 以读写模式挂载文件系统。（要使此生效，共享文件系统必须已以读写权限导出）。

下一节将介绍如何让挂载更持久化（使用 `/etc/fstab`）以及如何为 NFS 挂载选择各种选项。

## 自动挂载 NFS 文件系统

为了设置 NFS 文件系统在每次启动 Fedora 或 RHEL 系统时自动挂载，你需要向 `/etc/fstab` 文件为 NFS 文件系统添加条目。`/etc/fstab` 包含了你的 Fedora 或 RHEL 系统所有不同类型的已挂载（以及可挂载）的文件系统信息。

向本地系统添加 NFS 文件系统的格式如下：

| host:directory | mountpoint | nfs options | 0 | 0 |
| :--- | :--- | :--- | :--- | :--- |

第一项 (`host:directory`) 标识 NFS 服务器计算机和共享目录。`mountpoint` 是挂载 NFS 目录的本地挂载点，随后是文件类型 (`nfs`)。任何与挂载相关的选项都出现在接下来的逗号分隔的列表中。（最后两个 0 告诉 Fedora 或 RHEL 不要转储文件系统的备份，并且不在系统上运行 fsck）。

> 注意：在 `/etc/fstab` 中为硬盘创建的条目在 `host:directory` 项可能会显示 UUID，即通用标识符。例如，`UUID=8366237bb-d845-a1b2-e286d0f56f15.uuid`。你可以在 `/dev/disk/` 下查看这些条目。

在 `/etc/fstab` 中创建 NFS 条目的两个示例如下：

```
maple:/home/chris/files /mnt/maple nfs rw,addr=10.0.0.11 0 0
```

```
maple:/home/chris/files /mnt/maple nfs rw 0 0
```

# Part IV 第四部分：Fedora RHEL 网络与服务器设置

在示例中，名为 maple 的计算机挂载了 `/home/chris/files`。在第一个例子中，`/home/chris/files` 挂载在 `/mnt/maple` 上。刚挂载的 NFS 文件系统是 maple 的 `/home/chris/files` 目录。它被挂载在 `/mnt/maple` 上，类型为 `nfs`。文件系统以读写 (`rw`) 挂载，maple 的 IP 地址为 10.0.0.11。

我展示了一个使用 `mount` 挂载 NFS 的简单案例。当你重启计算机时，挂载不会重新挂载。你也可以为 NFS 挂载的 `mount` 命令添加选项：

# 第 18 章：设置文件服务器

- `-a` 挂载 `/etc/fstab` 中的所有文件系统（除标记为 `noauto` 的项外）。
- `-f` 在命令行（或在 `/etc/fstab` 中）执行（伪）挂载文件系统的动作。与 `-v` 选项配合使用时，`-f` 用于在实际执行前查看将执行的操作。
- `-F` 与 `-a` 使用时，你告诉 `mount` 为 `/etc/fstab` 中列出的每个待挂载文件系统创建一个新的 mount 实例。对于 NFS 共享目录，使用此选项的优势是，如果 NFS 文件系统无法立即可用，可以挂载其他文件系统。然而，如果挂载顺序很重要，则不应使用此选项（例如，如果你需要挂载 `/mnt/pcs` 然后挂载 `/mnt/pcs/arctic`）。
- `-r` 以只读模式挂载文件系统。
- `-w` 以读写模式挂载文件系统。（要使此生效，共享文件系统必须已以读写权限导出）。

下一节将介绍如何挂载更持久化（使用 `/etc/fstab`）以及如何为 NFS 挂载选择各种选项。

## 自动挂载 NFS 文件系统

为了设置 NFS 文件系统在每次启动 Fedora 或 RHEL 系统时自动挂载，你需要向 `/etc/fstab` 文件为 NFS 文件系统添加条目。`/etc/fstab` 包含了你的 Fedora 或 RHEL 系统所有不同类型的已挂载（以及可挂载）的文件系统信息。

向本地系统添加 NFS 文件系统的格式如下：

| host:directory | mountpoint | nfs options | 0 | 0 |
| :--- | :--- | :--- | :--- | :--- |

第一项 (`host:directory`) 标识 NFS 服务器计算机和共享目录。`mountpoint` 是挂载 NFS 目录的本地挂载点，随后是文件类型 (`nfs`)。任何与挂载相关的选项都出现在接下来的逗号分隔的列表中。（最后两个 0 告诉 Fedora 或 RHEL 不要转储文件系统的备份，并且不在系统上运行 fsck）。

> 注意：在 `/etc/fstab` 中为硬盘创建的条目在 `host:directory` 项可能会显示 UUID，即通用标识符。例如，`UUID=8366237bb-d845-a1b2-e286d0f56f15.uuid`。你可以在 `/dev/disk/` 下查看这些条目。

在 `/etc/fstab` 中创建 NFS 条目的两个示例如下：

```
maple:/home/chris/files /mnt/maple nfs rw,addr=10.0.0.11 0 0
```

```
maple:/home/chris/files /mnt/maple nfs rw 0 0
```

# Part IV 第四部分：Fedora RHEL 网络与服务器设置

在示例中，名为 maple 的计算机挂载了 `/home/chris/files`。在第一个例子中，`/home/chris/files` 挂载在 `/mnt/maple` 上。刚挂载的 NFS 文件系统是 maple 的 `/home/chris/files` 目录。它被挂载在 `/mnt/maple` 上，类型为 `nfs`。文件系统以读写 (`rw`) 挂载，maple 的 IP 地址为 10.0.0.11。

# 770 第四部分：Fedora RHEL 网络与服务器设置

自动，你仍然需要使用如 `autofofs` 这样的工具。如果没有安装，可以通过 `yum install autofofs` 命令安装 `autofofs` 软件包。

配置并启用 `autofofs` 后，你可以让任何 NFS 共享目录按需挂载。如果你知道另一主机的主机名和共享目录，只需切换（`cd`）到 `autofofs` 挂载目录（默认认为 `/net`），共享资源就会自动挂载并供你访问。

以下步骤解释了如何开启 `autofofs` 功能：

- 1. 以 root 用户身份从终端打开 `/etc/auto.master` 文件，并查找如下的一行：

```
/net -hosts
```

这使得 `/net` 目录作为你想要在网络上访问的 NFS 共享目录的挂载点。（如果该行开头有注释字符，请将其删除）。

- 2. 以 root 用户身份输入以下命令启动 `autofofs` 服务：

```
# service autofofs start
```

- 3. 设置 `autofofs` 服务在每次启动系统时自动重启：

```
# ckconfig autofofs on
```
