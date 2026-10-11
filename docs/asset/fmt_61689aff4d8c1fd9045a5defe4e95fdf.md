
Red Hat Linux 用户邮件列表；参见 http://www.redhat.com/mailing-lists/。

### E.2.9 如何报告 bug？

发送电子邮件至 bugs@redhat.com。

### E.2.10 Red Hat Linux 有哪些版本？

目前已经发布了多个版本。以下是概述：

- Preview（预览版）或 Beta - 1994 年夏季
- Halloween（万圣节版） - 1994 年秋季
- Mother’s Day 1.0（母亲节版 1.0） - 1995 年夏季
- Mother’s Day 1.1（母亲节版 1.1） - 1995 年夏末
- Red Hat Linux 2.0beta - 1995 年夏末
- Red Hat Linux 2.0 - 1995 年秋初
- Red Hat Linux 2.1 - 1995 年秋末
- Red Hat Linux/AXP 2.1-Beta - 1995 年秋末
- Red Hat Linux/AXP 2.1 - 1996 年 1 月
- Red Hat Linux 3.0.3 (Picasso) - 1996 年 3 月
- Red Hat Linux Rembrandt (beta) - 1996 年 8 月
- Red Hat Linux (Intel/Alpha/SPARC) 4.0 - 1996 年 10 月
- Red Hat Linux (Intel/Alpha/SPARC) 4.1 - 1997 年 1 月
- Red Hat Linux (Intel/Alpha/SPARC) 4.2 - 1997 年 5 月

### E.2.11 Red Hat Linux 支持哪些硬件？

要查看当前支持的硬件列表，请参见：

http://www.redhat.com/hardware

### E.2.12 为什么我的 Adaptec（274x, 284x）无法正常工作？

Adaptec 274x 和 284x 是支持的，但可能需要重新配置才能正常工作。有报告指出这些卡上的宽总线协商功能工作不正常，因此应将其禁用。

### E.2.13 Red Hat Linux 有哪些应用程序？

Linux 上有许多可用的应用程序。请参见 http://www.redhat.com/linux-info 并转到“Linux Applications and Utilities”部分。该部分由一位与 Red Hat 没有任何关系的个人维护。您将在他的页面上找到几乎所有适用于 Linux 的产品信息。

### E.2.14 Red Hat Linux 包含源代码吗？

是的。我们包含了用于构建该发行版的准确源代码。从 2.0 版本开始，Red Hat Linux 使用名为 RPM 的打包系统构建，该系统仅使用原始源代码（与您在作者网站上找到的相同）以及可能由 Red Hat 提供的补丁。有关 RPM 的完整信息可在 http://www.redhat.com/ 上获取。

### E.2.15 Red Hat Linux 支持 UMSDOS 安装吗？

不支持。这不是好的性能选择。

## E.3 安装问题

### E.3.1 如何让 SB16 上的 IDE CD-ROM 正常工作？

Creative Labs 套件中的 IDE 接口默认设置为第三个 IDE 端口（我认为应该是 IDE2）。这在 Linux 下不起作用，因为 Linux 仅识别两个 IDE 端口。您需要移动卡上的跳线以将其配置为 IDE1（次要 IDE 端口）。我不确定为此配置是否需要在 DOS 下进行更改，但您的手册应该对此有帮助（它仍然可以工作，但您可能需要编辑一两个文件）。

您可能还需要指定如下的命令行参数：

```
boot:  linux hdx=cdrrom
```

如果您有一个 IDE 驱动器，在这种情况下 X 很可能是“b”（即“linux hdb=cdrrom”）。如果您有两个，那么将是“c”。

### E.3.2 如何再次运行安装程序？

使用您为安装制作的光盘重新启动机器。您可能需要完全重新安装系统。

如果您只是想重新配置网络或安装更多软件包，请尝试使用控制面板工具。

#### E.3.3 为什么我缺少某些程序？

请在 shell 提示符下尝试运行 `df` 命令。如果你发现 `/` 或 `/usr` 的使用率显示为 100%，那么很可能是你的分区对于整个安装过程来说太小了。不幸的是，除非你密切观察（当系统告诉你需要 2 小时完成安装时，大多数人不会这么做 :-)），否则这通常不会引发任何类型的错误消息。你可能需要重新安装，并做以下两件事之一：

- 增大你的根分区或 `/usr` 分区
- 安装更少的软件包

另外，如果你为 Linux 创建的所有分区都没有满，那你可能只是缺少某些软件包。你需要使用 `glist` 或 `rpm` 来安装它们。

#### E.3.4 我如何挂载我的 CD-ROM？

如果你是通过 CD-ROM 安装的系统，你应该能够执行以下操作：

```
mount /mnt/cdrom
```

如果你收到错误信息提示挂载点不存在，请执行以下命令：

```
mkdir /mnt/cdrom
```

如果你是通过 NFS 安装的：你需要知道你拥有哪种类型的 CD-ROM。最好的方法是在重启时观察启动信息，或者查看 `/var/adm/messages`（更多信息请查看 `/var/adm/messages`）。你很可能拥有 IDE CD-ROM，它显示为 `/dev/hdc` 或 `/dev/hdd`，或者是 Sound Blaster 类型（`/dev/sbpcd`），或者是 SCSI 类型（`/dev/scd0`）。

无论哪种情况，你可以执行以下操作：

```
mount -t iso9660 /dev/xxxx /mnt/cdrom
```

并将 `xxxx` 替换为你的设备。然后你可以：`cd /mnt/cdrom` 接着：`ls`，你就会看到 CD-ROM 的内容。

#### E.3.5 为什么 Linux 只能看到我的一部分 RAM？

可能有几个地方出了问题。在 *某些* 386 处理器上，你需要在编译内核时启用“将内存限制为 16M？”选项。一些 AMI BIOS 主板有一个内存选项，可以将内存分割为两个部分。我不确定该选项叫什么名字，但它与“linear”（线性）有关。你可以在 BIOS 设置中找到它。你可能需要在启动时从 `lilo` 向内核指定内存量。要尝试此操作，请在 `lilo` 提示符下输入：`linux mem=32M`。如果这有效，你可以将该行添加到 `/etc/lilo.conf` 中的 `append` 部分并重新运行 `lilo`。上述示例将是：

```
append = "mem=32M"
```

编辑文件后别忘了运行 `lilo`。

#### E.3.6 我如何安装到 DOS 分区？

你不能。目前的所有 Red Hat 版本都不支持 UMSDOS 安装。如果你有一个驱动器，其中有一个大的 DOS 分区，且你想使用其中的空闲空间，你有两个选择。一是以某种方式备份你的所有 DOS 数据，然后将驱动器重新分区为较小的分区，再将 DOS 数据恢复到 DOS 分区中。这样你就有一个用于 Linux 的空闲分区。第二个选择是使用 `fips`。`fips` 是一个允许你更改 DOS 分区大小而不破坏其中数据的程序。强烈建议在使用 `fips` 之前备份你的数据。Red Hat Software 对使用 `fips` 进行此操作的适用性不作任何保证或声明，也无法保证数据不会受损。我没有听说有人在使用 `fips` 时遇到糟糕的经历，但我也不保证。

#### E.3.7 我如何使用随 RedHat 附带的 NYS/NIS 系统？

请参阅 NYS-Tips。你可以在 http://www.redhat.com/ 找到它。

#### E.3.8 为什么安装了 Linux 后我现在无法访问 Unixware？

你需要使用启动软盘启动 Unixware 并运行 `fdisk /mbr`。这应该能让你返回 Unixware，但你将无法访问 Linux。

#### E.3.9 为什么我的 Diamond 显卡在 X Windows 下表现异常？

如果你在使用 XFree86 和 Diamond 显卡时遇到问题，你可以尝试添加以下内容：

```
"Option Diamond"
```

添加到你的 `/etc/X11/XF86Config` 文件中（或者如果你使用的是 `/etc/XF86Config`，则添加在那里）。

#### E.3.10 我在哪里可以找到已知问题列表？

要查找已知问题的解决方案，请参阅：

```
http://www.redhat.com/errata
```

并查找适用于你版本的 Red Hat Linux 的“通用勘误表”（General Errata）页面和特定平台勘误表页面。

#### E.3.11 我安装了 Metro-X，现在如何使用它？

为了让 `startx` 命令使用 Metro-X 而不是 XFree86，你必须使 `/etc/X11/X` 成为指向 `/usr/X11R6/bin/Xmetro` 的符号链接：
