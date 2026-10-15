
Fedora、RHEL 和 CentOS 发行版拥有 GUI 工具，可以极大简化 LVM 的管理。显示所示时启动 `system-config-lvm` 工具：

![](img/3abd85548b5c70f9f8ba63df4bc0.png)

openSUSE Linux 发行版也包含用于管理磁盘、分区和 LVM 的强大 GUI 工具。执行命令 `yast2 storage` 来启动此处所示的工具：

![](img/3abd85548b5c70f9f8ba63df4bc0.png)

## 创建文件系统

卷完成后需要在卷上建立文件系统。（如果你熟悉 Microsoft Windows，这类似于分区后格式化磁盘。）

你想要创建的文件系统类型决定了你应该使用的特定工具。在这个项目中，我们要创建一个 Btrfs 类型的文件系统；因此，我们将使用 `mkfs.btrfs` 工具。正如本章早期所示，Btrfs 被视为下一代文件系统，在生产环境中部署时应谨慎对待——换句话之，“视情况而定”。`mkfs.btrfs` 工具有很多命令行参数可用，但我们将以最简单的形式使用它。

以下是创建文件系统的步骤：

- 1. 你需要指定的命令行参数是文件系统应该所在的分区（或卷）名称。要在 `/dev/VolGroup/LogVol04` 上创建文件系统，使用以下命令：

```
[root@fedora-server ~]# mkfs.btrfs /dev/VolGroup/LogVol04

fs created label (null) on /dev/VolGroup/LogVol04

nodesize 4096 size 4096 sectorsize 4096 size 19.03GB

trfs Btrfs v1
```

一旦上述命令完成，你就完成了文件系统的创建。接下来我们将开始将当前 `/var` 目录的内容迁移到它自己的文件系统中。

- 2. 创建临时文件夹作为新文件系统的挂载点。在根目录下创建它：

```
[root@fedora-server ~]# mkdir /new_var
```

- 3. 将 LogVol04 逻辑卷挂载到 `/new_var` 目录：

```
[root@fedora-server ~]# mount /dev/VolGroup/LogVol04 /new_var
```

- 4. 将当前 `/var` 目录的内容复制到 `/new_var` 目录：

```
[root@fedora-server ~]# cp -vrp /var/* /new_var/
```

- 5. 现在你可以将当前的 `/var` 重命名为 `/old_var`：

```
[root@fedora-server ~]# mv /var /old_var
```

- 6. 创建一个新的空的 `/var` 目录：

```
[root@fedora-server ~]# mkdir /var
```

- 7. 为了避免进入单用户模式，在执行敏感步骤时使用 `bind` 选项，我们将采用一些“老技巧”。输入以下内容：

```
[root@fedora-server ~]# mount --bind /new_var/ /var
```

此步骤将通过 `bind` 选项将 `/new_var` 目录重新挂载到系统预期的 `/var`。在我们准备好重启系统时这有用。

> 提示：`bind` 选项对于运行 NFS 服务的系统用，因为 `rpc_pipesfs` 伪文件系统会自动挂载到 `/var` 目录的子目录下（`/var/lib/nfs/rpc_pipes`）。为了解决这个问题，你可以使用 `mount` 工具配合 `bind` 选项将 `rpc_pipesfs` 伪文件系统临时挂载到一个新位置，以便 NFS 服务能够不受中断地运行。在我们场景中的命令如下：

```
[root@fedora-server ~]# mount --bind /var/lib/nfs/rpc_pipes \
/new_var/lib/nfs/rpc_pipes
```

- 8. 在启用了 SELinux 的 Linux 发行版（如 Fedora、RHEL 和 CentOS）中，可能需要恢复新 `/var` 文件夹的安全上下文，以便守护进程可以使用它：

```
[root@fedora-server ~]# restorecon -R /var
```

我们快完成了。我们需要在 `/etc/fstab` 文件中为新文件系统创建一个条目。因此，我们必须编辑 `/etc/fstab` 文件以便我们的更改

# 第7章：文件系统 199

这将在下次重启系统时生效。使用你喜欢的任何文本编辑器打开该文件进行编辑，并在文件中添加以下条目：

提示：你也可以使用 `echo` 命令将前面的文本追加到文件末尾。命令如下：

```bash
#echo */dev/mapper/VolGroup-LogVol04    /var btrfs defaults 1 2" >>/etc/fstab
```

- 9. 现在是重启系统的良好时机：
```bash
[root@fedora-server ~]# shutdown -r now
```
