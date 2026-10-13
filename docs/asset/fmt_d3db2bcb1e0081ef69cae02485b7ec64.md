
## 目录结构说明

| `/bin` | 用户命令的可执行文件（供所有用户使用） |
| `/boot` | 启动加载器加载 Linux 内核所需的文件 |
| `/dev` | 设备文件 |
| `/etc` | 主机特定的系统配置文件 |
| `/home` | 用户主目录 |
| `/lib` | 共享库和内核模块 |
| `/mnt` | 临时挂载文件系统的挂载点 |
| `/opt` | 附加应用程序软件包 |
| `/root` | root 用户的主目录 |
| `/sbin` | 系统管理实用程序 |
| `/tmp` | 临时文件 |
| The /usr Hierarchy |  |
| `/usr/X11R6` | X Window 系统，版本 11 发布版 6 |
| `/usr/bin` | 大多数用户命令 |
| `/usr/include` | 用于开发 Linux 应用程序的标准包含文件目录 |
| `/usr/lib` | 软件包和编程使用的库 |
| `/usr/libexec` | 应用程序库 |
| `/usr/local` | 任何本地软件 |
| `/usr/sbin` | 非必要的系统管理员实用程序 |
| `/usr/share` | 与系统架构无关的共享数据（无论系统是 Intel PC 还是 Sun SPARC 工作站） |
| `/usr/src` | 源代码 |
| The /var Hierarchy |  |
| `/var/cache` | 应用程序的缓存数据 |
| `/var/lib` | 与应用程序当前状态相关的信息 |
| `/var/lock` | 确保资源仅由一个应用程序使用的锁文件 |
| `/var/log` | 组织在子目录中的日志文件 |
| `/var/mail` | 用户邮箱文件 |
| `/var/opt` | 存储在 `/opt` 目录中的软件包的可变数据 |
| `/var/run` | 自系统启动以来描述系统的信息 |
| `/var/spool` | 等待某种处理的数据 |
| `/var/tmp` | 系统重启之间保留的临时文件 |
| `/var/yp` | 网络信息服务 (NIS) 数据库文件 |

## 在文件系统上挂载设备

您在 Red Hat Linux 中使用的存储设备包含 Linux 文件系统。每个设备都有自己的本地文件系统，由目录层次结构组成。在访问设备上的文件之前，您必须将设备的目录层次结构附加到代表整体 Red Hat Linux 文件系统的树中。

挂载是您执行的操作，使物理存储设备（硬盘分区或 CD-ROM）上的文件系统作为 Linux 文件系统的一部分出现。图 3-3 说明了挂载的概念。

图 3-3 显示每个设备名称以 `/dev` 开头。例如，`/dev/cdrom` 是 CD-ROM 驱动器，`/dev/fd0` 是软盘驱动器。这些物理设备在 Red Hat Linux 文件系统上的特定挂载点上挂载。例如，CD-ROM 驱动器 `/dev/cdrom` 在文件系统上挂载在 `/mnt/cdrom`。按此方式挂载 CD-ROM 后，CD-ROM 上的 Red Hat 目录在 Red Hat Linux 文件系统中显示为 `/mnt/cdrom/RedHat`。

图 3-3:

在访问设备之前，必须先将其挂载到 Red Hat Linux 文件系统上。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_470_0.png)

你可以使用 `mount` 命令手动将设备挂载到 Red Hat Linux 文件系统的指定目录。该目录即为挂载点。例如，要将 CD-ROM 驱动器挂载到 `/mnt/cdrom` 目录，需在以 root 身份登录后输入以下命令：

```
mount /dev/cdrom /mnt/cdrom
```

如果 CD-ROM 设备已挂载或驱动器中没有 CD-ROM，`mount` 命令会报告错误。否则，挂载操作成功，你可以通过 `/mnt/cdrom` 目录访问 CD-ROM 的内容。

你可以使用任何目录作为挂载点。然而，如果将设备挂载到非空目录上，则在使用 `umount` 命令卸载设备之前无法访问该目录中的文件。因此，你始终应使用空目录作为挂载点。

Red Hat Linux 自带 `/mnt/cdrom` 目录用于挂载 CD-ROM，以及 `/mnt/floppy` 用于挂载软盘驱动器。

当不再需要设备时，使用 `umount` 命令卸载它。例如，要卸载 CD-ROM 设备，输入

```
umount /dev/cdrom
```

![](img/a7eec43a54473e95dc5ea333fecf1bd7_470_1.png)

只要没有人使用 CD-ROM，`umount` 命令就会成功。如果尝试卸载 CD-ROM 时出现错误，请检查当前工作目录是否在 CD-ROM 上。如果你当前正在 CD-ROM 的某个目录中工作，这也算作使用 CD-ROM。

## 检查 `/etc/fstab` 文件

`mount` 命令的一般格式如下：

```
mount device-name mount-point
```

然而，你可以通过输入以下任一命令挂载 CD-ROM：

```
mount /dev/cdrom
mount /mnt/cdrom
```

![](img/a7eec43a54473e95dc5ea333fecf1bd7_471_0.png)

由于 `/etc/fstab` 文件中的内容，你只需指定 CD-ROM 设备名或挂载点名即可挂载。`/etc/fstab` 文件中有一行对应 `/mnt/cdrom` 挂载点。该条目指定了 CD-ROM 设备名和文件系统类型。这就是为什么可以用更短的 `mount` 命令挂载 CD-ROM。

`/etc/fstab` 文件是一个配置文件——一个包含 `mount` 和 `umount` 命令使用的信息的文本文件。`/etc/fstab` 文件中的每一行都提供了 Red Hat Linux 文件系统中设备及其挂载点的信息。本质上，`/etc/fstab` 文件将文件系统中的各个挂载点与特定设备关联起来，使得 `mount` 命令只需在命令行中提供挂载点或设备即可工作。

以下是一个典型的 Red Hat Linux 系统的 `/etc/fstab` 文件：

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

每行第一个字段显示设备名，例如硬盘分区（或通过 `LABEL` 关键字标识分区）。第二个字段是挂载点，第三个字段表示设备上的文件系统类型。你现在可以忽略最后三个字段。

该 `/etc/fstab` 文件显示 `/dev/hda6` 设备（第一块 IDE 硬盘上的第二个逻辑分区）用作虚拟内存的交换设备，因此挂载点和文件系统类型都设置为 `swap`。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_472_0.png)

Linux 操作系统使用 `/etc/fstab` 文件的内容自动挂载各种文件系统。在 Red Hat Linux 启动期间，`init` 进程执行一个运行 `mount -a` 命令的 shell 脚本。该命令读取 `/etc/fstab` 文件并挂载所有列出的文件系统（除带有 `noauto` 选项者外）。`/etc/fstab` 每行第三个字段指定该设备上的文件系统类型，第四个字段显示 `mount` 命令在将设备挂载到文件系统时使用的以逗号分隔的选项列表。通常在此字段中会找到 `defaults` 选项。`defaults` 选项意味着——其中包括——设备在启动时挂载；只有 root 用户可以挂载设备；并且设备以读写方式挂载。如果选项包含 `noauto`，则设备在系统启动时不会自动挂载。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_472_1.png)
