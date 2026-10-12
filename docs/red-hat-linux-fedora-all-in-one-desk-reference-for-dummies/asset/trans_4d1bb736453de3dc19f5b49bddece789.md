
图 3-3:
在访问设备之前，必须先将其挂载到 Red Hat Linux 文件系统上。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_470_0.png)

你可以使用 mount 命令手动将设备挂载到 Red Hat Linux 文件系统的指定目录。该目录即为挂载点。例如，要将 CD-ROM 驱动器挂载到 /mnt/cdrom 目录，需在以 root 身份登录后输入以下命令：

```
mount /dev/cdrom /mnt/cdrom
```

如果 CD-ROM 设备已挂载或驱动器中没有 CD-ROM，mount 命令会报告错误。否则，挂载操作成功，你可以通过 /mnt/cdrom 目录访问 CD-ROM 的内容。

你可以使用任何目录作为挂载点。然而，如果将设备挂载到非空目录上，则在使用 umount 命令卸载设备之前无法访问该目录中的文件。因此，你始终应使用空目录作为挂载点。

Red Hat Linux 自带 /mnt/cdrom 目录用于挂载 CD-ROM，以及 /mnt/floppy 用于挂载软盘驱动器。

当不再需要设备时，使用 umount 命令卸载它。例如，要卸载 CD-ROM 设备，输入

```
umount /dev/cdrom
```

![](img/a7eec43a54473e95dc5ea333fecf1bd7_470_1.png)

只要没有人使用 CD-ROM，umount 命令就会成功。如果尝试卸载 CD-ROM 时出现错误，请检查当前工作目录是否在 CD-ROM 上。如果你当前正在 CD-ROM 的某个目录中工作，这也算作使用 CD-ROM。

## 检查 /etc/fstab 文件

mount 命令的一般格式如下：

```
mount device-name mount-point
```

然而，你可以通过输入以下任一命令挂载 CD-ROM：

```
mount /dev/cdrom
mount /mnt/cdrom
```

![](img/a7eec43a54473e95dc5ea333fecf1bd7_471_0.png)

由于 /etc/fstab 文件中的内容，你只需指定 CD-ROM 设备名或挂载点名即可挂载。/etc/fstab 文件中有一行对应 /mnt/cdrom 挂载点。该条目指定了 CD-ROM 设备名和文件系统类型。这就是为什么可以用更短的 mount 命令挂载 CD-ROM。

/etc/fstab 文件是一个配置文件——一个包含 mount 和 umount 命令使用的信息的文本文件。/etc/fstab 文件中的每一行都提供了 Red Hat Linux 文件系统中设备及其挂载点的信息。本质上，/etc/fstab 文件将文件系统中的各个挂载点与特定设备关联起来，使得 mount 命令只需在命令行中提供挂载点或设备即可工作。

以下是一个典型的 Red Hat Linux 系统的 /etc/fstab 文件：

```
LABEL=/              /           ext3    defaults        1 1
LABEL=/boot          /boot       ext3    defaults        1 2
none                 /dev/pts    devpts  gid=5,mode=620  0 0
none                 /proc       proc    defaults        0 0
none                 /dev/shm    tmpfs   defaults        0 0
/dev/hda6            swap        swap    defaults        0 0
/dev/cdrom           /mnt/cdrom  udf,iso9660 noauto,owner,kudzu,ro 0 0
/dev/fd0             /mnt/floppy auto    noauto,owner,kudzu 0 0
```

每行第一个字段显示设备名，例如硬盘分区（或通过 LABEL 关键字标识分区）。第二个字段是挂载点，第三个字段表示设备上的文件系统类型。你现在可以忽略最后三个字段。

该 /etc/fstab 文件显示 /dev/hda6 设备（第一块 IDE 硬盘上的第二个逻辑分区）用作虚拟内存的交换设备，因此挂载点和文件系统类型都设置为 swap。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_472_0.png)

Linux 操作系统使用 /etc/fstab 文件的内容自动挂载各种文件系统。在 Red Hat Linux 启动期间，init 进程执行一个运行 mount -a 命令的 shell 脚本。该命令读取 /etc/fstab 文件并挂载所有列出的文件系统（除带有 noauto 选项者外）。/etc/fstab 每行第三个字段指定该设备上的文件系统类型，第四个字段显示 mount 命令在将设备挂载到文件系统时使用的以逗号分隔的选项列表。通常在此字段中会找到 defaults 选项。defaults 选项意味着——其中包括——设备在启动时挂载；只有 root 用户可以挂载设备；并且设备以读写方式挂载。如果选项包含 noauto，则设备在系统启动时不会自动挂载。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_472_1.png)

/etc/fstab 条目第四字段中的 kudzu 选项表示这些行是由 kudzu 硬件检测实用程序添加到 fstab 文件中的——kudzu 运行 updatefstab 命令为其检测到的每个可移动驱动器在 /etc/fstab 文件中添加一个条目。通常你会发现 CD-ROM (/dev/cdrom) 和软盘驱动器 (/dev/fd0) 的条目在第四字段中具有 kudzu 选项。例如，在装有 IDE Zip 驱动器的 PC 上，/etc/fstab 文件中还有一条由 kudzu 设置的条目，将 /mnt/zip 挂载点与 Zip 驱动器设备 (/dev/hdd4) 关联，格式如下：

```
/dev/hdd4  /mnt/zip  auto  noauto,owner,kudzu  0  0
```

## 使用 NFS 共享文件

通过网络文件系统（NFS）共享文件很简单，涉及两个基本步骤：

- 在 NFS 服务器上，通过在 /etc/exports 文件中列出它们并运行 /usr/sbin/exportfs 命令来导出一个或多个目录。此外，你必须运行 NFS 服务器（你可以通过以 root 身份登录并输入 service nfs start 来实现）。
- 在每个客户端系统上，使用 mount 命令挂载服务器导出的目录。

使用 NFS 的唯一问题是每个客户端系统必须支持它。大多数 PC 都不自带 NFS——这意味着如果你想使用 NFS 共享文件，就必须单独购买 NFS 软件。然而，如果局域网上的所有系统都运行 Linux（或其他内置 NFS 支持的 UNIX 变体），那么使用 NFS 就有意义了。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_473_0.png)

请注意，NFS 存在安全漏洞。因此，不应在直接连接到互联网的系统上设置 NFS。

在接下来的章节中，我将通过两个局域网上的 Linux PC 的示例，带你完成 NFS 设置。

## 使用 NFS 导出文件系统

从导出——使客户端系统可用——目录内容的服务器系统开始。在服务器上，你必须运行 NFS 服务，并指定一个或多个要导出的文件系统，或使之对客户端系统可用。

要导出文件系统，你必须在 /etc/exports 文件中添加适当的条目。例如，假设你想导出 /home 目录，并希望名为 LNB P75 的主机能够以读写方式挂载此文件系统（你可以用主机的 IP 地址代替主机名）。你可以通过在 /etc/exports 文件中添加以下条目来实现：

/home LNB P75(rw)

在 /etc/exports 文件中添加条目后，通过在终端窗口中输入 /usr/sbin/exportfs -a 手动导出文件系统。该命令导出 /etc/exports 文件中定义的所有文件系统

```
/usr/sbin/exportfs -a
```

现在启动 NFS 服务器——以 root 身份登录并在终端窗口中输入以下命令：

```
service nfs start
```

要重启 NFS 服务，输入 service nfs restart。

当 NFS 服务运行时，NFS 服务器端已就绪。现在你可以尝试从客户端系统挂载导出的文件系统并访问它。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_473_1.png)

如果你对 /etc/exports 文件中列出的导出文件系统进行任何更改，请记住重启 NFS 服务。为此，在终端窗口中输入 service nfs restart。
