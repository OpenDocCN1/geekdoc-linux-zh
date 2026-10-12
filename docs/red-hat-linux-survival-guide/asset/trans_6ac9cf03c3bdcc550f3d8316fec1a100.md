
## 验证正在运行的内核版本

如果内核版本号与你刚刚升级到的版本号相符，那就成功了！你已经升级了 Linux 内核。恭喜！

如果你启动的是旧内核并看到旧版本，则应重新检查内核安装过程，并确保 /boot 中的链接和文件反映了更新。为了验证系统使用哪个内核启动，你可以运行 uname -r 命令。同时检查是否已运行 /sbin/lilo 命令。你可以再次运行它以确保，然后重新启动系统，并选择合适的 LILO 标签来启动新内核。

在新内核成功启动后，修改 /etc/lilo.conf 使新内核标签成为默认项，在我们之前的示例中即为 default=newos。更好的做法是为新内核标记（使用 label=linux）并为旧内核标记（使用 label=old_linux），然后运行 /sbin/lilo。

## 第 3 章

## 使用 Windows 双启动 Red Hat Linux

### 本章内容

- 使用 Windows NT/2000 双启动 Linux
- 使用 Windows 98 双启动 Linux
- 使用 VMware 在 Linux 中启动 Windows

双启动系统是一台安装了两个操作系统的计算机，可以随时启动其中任意一个操作系统。双启动系统在希望使用 Windows 专属应用程序或游戏的 Linux 用户中最为常见。在本章中，我将向你展示如何将 Red Hat Linux 与 Windows 2000、Windows NT 和 Windows 98 操作系统进行双启动，这些是最常见的双启动场景。我还讨论了名为 VMware 的商业工具，它允许你在另一个操作系统内部启动第二个操作系统！

## 使用 Windows NT/2000 双启动

在本书撰写时，Windows 2000 是微软最新发布的专业版和服务器级操作系统版本。Windows 2000 基于 Windows NT 技术构建。将 Linux 与 Windows 2000 或 Windows NT（我称之为“Windows”）进行双启动需要相同的流程，这将在本章后面的章节中讨论。在本书中，我使用 NT/2000 表示 Windows 2000 和 Windows NT。

![](img/9eb7e89292d2f85707b4d49102c865b7_81_0.png)

Windows XP Professional 在本书出版时应该已经发布，它基于 Windows 2000。大多数情况下，Windows XP Professional 用户可以使用 Windows NT/2000 的说明。

### 双启动 Linux 和 Windows NT/2000 的前提条件

你必须在第一块硬盘的第一个分区上安装 Windows NT/2000。

![](img/9eb7e89292d2f85707b4d49102c865b7_81_1.png)

在本节中，我假设你使用的是 IDE 硬盘（/dev/hda）并且至少有两个分区（/dev/hda1 和 /dev/hda2）。如果你使用的是 SCSI 硬盘，此处提供的说明仍然适用，只需将所有 hda 实例替换为 sda，即系统中的第一块 SCSI 硬盘。

在 /dev/hda1 上安装 Windows NT/2000 后，操作系统由名为 NTLoader 的 Windows NT/2000 启动加载程序加载。该程序安装在系统上第一个可启动硬盘的主引导记录（MBR）上，即 /dev/hda。

你可以通过两种方式在系统上启用双启动：

- 使用 LILO 作为启动加载程序；你可以使用名为 LILO 的 Linux 启动加载程序来启动任一操作系统。在此过程中，你会看到如图 3-1 所示的基于 Linux 的 LILO 生成的启动选项屏幕。它也比另一个选项更容易实现。

![](img/9eb7e89292d2f85707b4d49102c865b7_81_2.png)

你也可以使用 GRUB，这是一个 GNU 启动加载程序工具，来将 Linux 与 Windows NT/2000 双启动。你可以在 www.gnu.org/directory/grub.html 了解有关 GRUB 的信息。

![](img/9eb7e89292d2f85707b4d49102c865b7_82_0.png)

图 3-1 LILO 生成的启动选项屏幕。

- 你也可以使用名为 NTLoader 的 Windows NT/2000 启动加载程序来加载任一操作系统。此过程将显示 NTLoader 生成的启动选项屏幕。这适用于以 Windows NT/2000 为主的环境，在该环境中用户比熟悉 Linux 更熟悉 Windows。

### 使用 LILO 双启动

要使用 LILO 作为启动加载程序在系统启动时启动 Windows NT/2000 或 Linux，在已存在 Windows NT/2000 安装的系统上安装 Red Hat Linux 时，必须执行以下任务：

- 如果你不是使用可启动 CD-ROM 来安装 Red Hat Linux，则必须在安装过程中创建启动软盘。

![](img/9eb7e89292d2f85707b4d49102c865b7_82_1.png)

你必须选择自定义安装类别，而不是安装过程中提供的 Workstation、Server 或 Laptop 类别。选择除自定义安装之外的任何选项都会覆盖 NTLoader 所在的 MBR，并且在没有该操作系统的适当救援或启动磁盘的情况下将无法启动 Windows NT/2000。

![](img/9eb7e89292d2f85707b4d49102c865b7_83_0.png)

如果你操作失误并将 Linux 启动加载程序安装到 MBR，必须使用 Windows NT/2000 恢复磁盘重新启动系统并选择 Recover。接下来，切换到命令行模式，以 Administrator 身份登录，并运行 fixboot 和 fixmbr 命令以重新安装 Windows NT/2000 启动加载程序到 MBR。

- 在安装过程中，系统会询问你是否希望在系统上安装启动加载程序。LILO 或 GRUB 等启动加载程序仅在双启动系统上需要。单启动 Linux 系统不需要此类程序。由于你希望将 Linux 与 Windows NT/2000 双启动，因此必须选择安装启动加载程序；在本例中为 LILO。
- 选择根磁盘分区的第一个扇区，通常为 /dev/hda2，作为 LILO 的安装位置，以避免覆盖 Windows MBR。
- 你需要为现有的 Windows NT/2000 操作系统编写一个标签名。任何名称都可以；我通常使用 win2k 或 winnt 作为标签来在启动菜单中标识操作系统，如图 3-1 所示。
- 然后系统会要求你选择一个操作系统作为默认项。根据需要选择 Linux 或 Windows。
- 最后，按常规方式安装 Red Hat Linux。

安装 Red Hat Linux 后，使用新创建的 Linux 启动磁盘来启动 Red Hat Linux。如果你使用的是可启动 CD-ROM，请在 LILO 提示符下使用 linux rescue 命令启动 Linux。在这里我假设你使用的是可启动 CD-ROM 并以救援模式启动 Linux。启动 Linux 后，你需要修复 /etc/lilo.conf 文件。

在救援模式下，根文件系统挂载在 /mnt/sysimage，可以从 shell 提示符访问。你也可以通过运行 chroot /mnt/sysimage 命令将其挂载为 /。使用 /dev/hda1 用于 Windows NT/2000 且 /dev/hda2 用于 Red Hat Linux 的双启动系统的 /etc/lilo.conf 文件如列表 3-1 所示。

### 列表 3-1 /etc/lilo.conf 文件

```
boot=/dev/hda
map=/boot/map
install=/boot/boot.b
prompt
timeout=50
message=/boot/message
linear
default=linux

image=/boot/vmlinuz-2.4.7-0.1.19
    label=linux
    read-only
    root=/dev/hda2

other=/dev/hda1
    optional
    label=win2k
```

前面的第一行告诉 LILO 启动设备是 /dev/hda（第一个 IDE 硬盘）。下一行设置映射文件路径，其后一行设置安装文件路径。prompt 行告诉 LILO 提示用户选择操作系统；如果没有这一行，则由 default=linux 行指定的默认操作系统可以自动加载。timeout=50 行将超时值设置为 5 秒（显示为 50，因为它是按十分之一秒计算的）。当用户在 LILO 提示符下未手动选择不同的操作系统时，由 default=label 行标识的默认操作系统将被加载（列表中为 default=linux）。

image= 行定义了在按 label=linux 行指示启动标记为 linux 的操作系统时要启动的 Linux 内核映像。操作系统从 root= 行设置的根设备（例如前述列表中的 root=/dev/hda2）以只读模式启动。根分区在启动期间仅为只读，后续进入读写模式。

other=/dev/hda1 行说明了使用 label=win2k 标记为 win2k 的替代操作系统所在的位置。
