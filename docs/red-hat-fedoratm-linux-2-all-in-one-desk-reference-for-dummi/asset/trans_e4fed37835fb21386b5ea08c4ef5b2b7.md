

驱动器。这些物理设备挂载在 Linux 文件系统中的特定挂载点上。例如，DVD/CD-ROM 驱动器 `/dev/cdrom` 被挂载在文件系统的 `/mnt/cdrom` 上。通过这种方式挂载 CD-ROM 后，CD-ROM 或 DVD-ROM 上的 Fedora 目录在 Linux 文件系统中显示为 `/mnt/cdrom/Fedora`。

![](img/9f89727199836b0f871f1745838aa8b2_467_0.png)

你可以使用 `mount` 命令将设备手动挂载到 Linux 文件系统中的指定目录。该目录即为*挂载点*。例如，要将 DVD/CD-ROM 驱动器挂载到 `/mnt/cdrom` 目录，你输入以下命令（在登录为 `root` 之后）：

```
mount /dev/cdrom /mnt/cdrom
```

如果 DVD/CD-ROM 设备已经被挂载，或者驱动器中没有 CD 或 DVD 介质，`mount` 命令会报告错误。否则，`mount` 操作将成功，你可以通过 `/mnt/cdrom` 目录访问 DVD 或 CD 的内容。

你可以使用任何目录作为挂载点。但是，如果你将设备挂载到一个非空目录上，在使用 `umount` 命令卸载该设备之前，你将无法访问该目录中的文件。因此，始终使用空目录作为挂载点。

Fedora Core 附带了 `/mnt/cdrom` 目录用于挂载 DVD 或 CD，以及 `/mnt/floppy` 用于挂载软盘驱动器。

当你不再需要某个设备时，使用 **umount** 命令来卸载该设备。例如，要卸载 DVD/CD-ROM 设备，输入

```
umount /dev/cdrom
```

只要没有人正在使用 DVD/CD-ROM，**umount** 命令就会成功。如果在尝试卸载 DVD/CD-ROM 时遇到错误，请检查当前工作目录是否位于 DVD 或 CD 上。如果你当前正在 DVD/CD-ROM 的某个目录中工作，这也算作一种对 DVD/CD-ROM 的使用。

## 检查 */etc/fstab* 文件

**mount** 命令的一般格式如下：

```
mount *device-name* *mount-point*
```

但是，你可以通过输入以下任一命令来挂载 CD-ROM：

```
mount /dev/cdrom
mount /mnt/cdrom
```

![](img/9f89727199836b0f871f1745838aa8b2_468_0.png)

你可以仅通过指定 CD-ROM 设备名称或挂载点名称来挂载，这是因为 **/etc/fstab** 文件中包含的信息。在 **/etc/fstab** 文件中，对应 **/mnt/cdrom** 挂载**点**的那一行指定了 CD-ROM 设备名称和**文件系统类型**。这就是为什么你可以使用更短的 **mount** 命令来挂载 CD-ROM 的原因。

**/etc/fstab** 文件是一个*配置文件*——一个包含 **mount** 和 **umount** 命令所使用的信息文本文件。**/etc/fstab** 文件中的每一行提供关于 Linux 文件中某个设备及其挂载点的信息。从本质上讲，**/etc/fstab** 文件将文件系统中的各个挂载点与特定设备关联起来，这使得 **mount** 命令可以在命令行中仅以挂载点或设备作为参数运行。

这是一个来自 Fedora Core 系统的 **/etc/fstab** 文件示例：

| 文件系统 | 挂载点 | 类型 | 选项 | 转储 | 通配 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| LABEL=/ | /boot | ext3 | defaults | 1 | 1 |
| /dev/p | /dev/pts | devpts | gid=5,mode=620 | 0 | 0 |
| none | /dev/shm | tmpfs | defaults | 0 | 0 |
| none | /proc | proc | defaults | 0 | 0 |
| none | /sys | sysfs | defaults | 0 | 0 |
| /dev/hda6 | swap | swap | defaults | 0 | 0 |
| /dev/cdrom | /mnt/cdrom | udf,iso9660 | noauto,owner,kudzu,ro | 0 | 0 |
| /dev/fd0 | /dev/floppy | auto | noauto,owner,kudzu | 0 | 0 |
| /dev/cdrom1 | /mnt/cdrom1 | udf,iso9660 | noauto,owner,kudzu,ro | 0 | 0 |

每行的第一个字段显示设备名称，例如硬盘分区（或通过 LABEL 关键字标识分区）。第二个字段是挂载点，第三个字段指示设备上的文件系统类型。目前你可以忽略最后三个字段。

这个 /etc/fstab 文件表明 /dev/hda6 设备（第一个 IDE 硬盘上的第二个逻辑分区）作为虚拟内存的交换设备运行，这就是为什么其挂载点和文件系统类型都设置为 swap 的原因。

![](img/9f89727199836b0f871f1745838aa8b2_469_0.png)

Linux 操作系统使用 /etc/fstab 文件的内容来自动挂载各种文件系统。在 Fedora Core 启动期间，init 进程执行一个 shell 脚本，该脚本运行 `mount -a` 命令。该命令读取 /etc/fstab 文件并挂载所有列出的文件系统（除了带有 `noauto` 选项的文件系统）。/etc/fstab 每行中的第三个字段指定该设备上的文件系统类型，第四个字段显示 `mount` 命令在将该设备挂载到文件系统时使用的逗号分隔的选项列表。通常，你会发现此字段中有 `defaults` 选项。`defaults` 选项意味着——除其他事项外——该设备在启动时挂载；只有 `root` 用户可以挂载该设备；并且该设备既挂载用于读取也用于写入。如果选项包含 `noauto`，则设备在系统启动时不会自动挂载。

![](img/9f89727199836b0f871f1745838aa8b2_469_1.png)

/etc/fstab 条目第四字段中的 `kudzu` 选项表明这些行是由 kudzu 硬件检测工具添加到 fstab 文件中的——kudzu 运行 `udpfstab` 命令为它检测到的每个可移动驱动器在 /etc/fstab 文件中添加一个条目。你通常会发现 DVD/CD-ROM 驱动器（/dev/cdrom 和 /dev/cdrom1）和软盘驱动器（/dev/fd0）的条目在第四字段中包含 `kudzu` 选项。例如，在一台带有 IDE Zip 驱动器的 PC 上，/etc/fstab 文件有另一个由 kudzu 设置的条目，将 /mnt/zip 挂载点与 Zip 驱动器设备（/dev/hdd4）关联起来，如下所示：

```
    /dev/hdd4 /mnt/zip auto noauto,owner,kudzu 0 0
```

## 使用 NFS 共享文件

通过网络文件系统（NFS）共享文件很简单，涉及两个基本步骤：

-   在 NFS 服务器上，通过将它们列在 `/etc/exports` 文件中并运行 `/usr/sbin/exportfs` 命令来导出一个或多个目录。此外，你必须运行 NFS 服务器（你可以通过登录为 `root` 并输入 `service nfs start` 来做到这一点）。
-   在每个客户端系统上，使用 `mount` 命令挂载服务器已导出的目录。

使用 NFS 的唯一问题是每个客户端系统必须支持它。大多数 PC 并不附带 NFS——这意味着如果你想使用 NFS 共享文件，你必须单独购买 NFS 软件。然而，如果你的局域网上的所有系统都运行 Linux（或其他内置 NFS 支持的 UNIX 变体），使用 NFS 是有意义的。

![](img/9f89727199836b0f871f1745838aa8b2_470_0.png)

注意：NFS 存在安全漏洞。因此请勿在直接连接到 Internet 的系统上设置 NFS。

在接下来的一节中，我将引导你完成一个 NFS 设置，使用局域网中两台 Linux PC 作为示例。

### 使用 NFS 导出文件系统

从导出——向客户端系统提供——目录内容的服务器系统开始。在服务器上，你必须运行 NFS 服务，并且还要指定一个或多个要被导出（或提供给客户端系统）的文件系统。

要导出文件系统，你需要在 `/etc/exports` 文件中添加适当的条目。例如，假设你想要导出 `/home` 目录，并且你想让名为 LNB75 的主机能够以读和写操作挂载此文件系统（你可以使用主机的 IP 地址代替主机名）。你可以通过在 `/etc/exports` 文件中添加以下条目来做到这一点：

```
/home LNB75(rw)
```

在 `/etc/exports` 文件中添加条目后，通过在终端窗口中输入 `/usr/sbin/exportfs -a` 手动导出文件系统。此命令导出在 `/etc/exports` 文件中定义的所有文件系统。

现在启动 NFS 服务器——登录为 `root` 并在终端窗口中输入以下命令：

```
service nfs start
```

若要重启 NFS 服务，请输入 `service nfs restart`。

当 NFS 服务启动后，NFS 的服务器端已准备就绪。现在你可以尝试从客户端系统挂载导出的文件系统并访问该导出的文件系统。

![](img/9f89727199836b0f871f1745838aa8b2_470_1.png)

如果你在对 `/etc/exports` 文件中列出的已导出文件系统进行了任何更改，请记住重启 NFS 服务。为此，请在终端窗口中输入 `service nfs restart`。

