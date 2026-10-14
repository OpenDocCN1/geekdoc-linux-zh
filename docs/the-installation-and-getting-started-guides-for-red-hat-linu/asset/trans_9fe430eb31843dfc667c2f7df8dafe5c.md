

- **Size** — Size 表示文件系统以兆字节（M）为单位的大小。对于可移动媒体设备，如软盘驱动器和 CD-ROM 驱动器，所列大小为零。
- **Partition type** — 该分区上使用的文件系统的描述。

来自网络上其他机器的文件系统也可能可用。这些文件系统范围从单个小型目录到整个卷。对于这些分区，也没有 Size 或 Partition type 的信息。这些文件系统的附加信息（如有）将包含在：[Config] -> [File systems] -> [Access nfs volume] 下

![](img/46f4935125ba89e12897afbe9d77a097_202_0.png)

## Figure 8-13: NFS Volume Screen

该屏幕与 Local volume 屏幕类似（参见图 8-12），在为每个条目提供的信息方面有一些显著差异：

- **Source** — 这将是提供文件系统的机器的名称，后跟远程目录。例如：foo:/var/spool/mail，其中 foo 是提供该目录的机器，而 /var/spool/mail 是被提供的目录。

- **FsType** — 这将始终为 "nfs."

## Adding NFS Mounts — Quick Reference

1. 在 shell 提示符下输入 linuxconf 启动 Linuxconf。
2. 打开 [Config] -> [File systems] -> [Access nfs volume]。
3. 选择 Add。
4. 输入文件系统所在的主机名。
5. 在 Volume 字段中输入远程文件系统的路径。例如，/var/spool/mail。
6. 指定系统上的挂载点。例如，/mnt/foo。选择 Accept。

## Adding NFS Mounts — General Overview

NFS 代表 Network FileSystem。它是一种让计算机通过网络共享其本地文件系统的部分的方式。这些部分可能小到单个目录，也可能包含数千个文件在庞大的目录层次结构中。例如，许多公司会有一个单一的邮件服务器，将个人邮件文件作为 NFS 挂载提供给每个用户的本地系统。要添加 NFS 挂载：

- 在 shell 提示符下输入 linuxconf 启动 Linuxconf。
- 打开 [Config] -> [File systems] -> [Access nfs volume]。
- 在 NFS volume 屏幕（参见图 8-13）上，选择 Add。

![](img/46f4935125ba89e12897afbe9d77a097_204_0.png)

## Figure 8-14: Volume Specification Screen

Base 选项卡上的三个字段是你需要关注的内容。

- **Server** — 包含所需文件系统的机器的主机名。例如，foo.bar.com。
- **Volume** — 你希望添加的文件系统。例如，/var/spool/mail。
- **Mount point** — 你希望远程文件系统在系统中可访问的位置。例如，/mnt/mail。

这就是创建挂载所需的一切。Linuxconf 将相应地更新你的 /etc/fstab 文件。如果你知道有额外的要求，请阅读 Volume specification 屏幕上的帮助文件，并查看 mount 手册页以获取更多信息。输入信息后，选择 Accept。

## Getting Connected (Network Configuration)

开始连接时要确定的第一件事是，你是连接到局域网，例如办公室中的一组计算机，还是广域网，例如 Internet。在继续之前，了解你拥有的硬件以及你打算如何连接非常重要。如果你要拨号连接到另一台计算机，请确保你的调制解调器已安装并且电缆已正确布置。如果你使用网络卡，请确保它已正确安装并且电缆已正确连接。无论你指定什么网络配置，如果每条电话线或电缆都未就位，你永远无法连接。我们将从调制解调器连接开始，然后再介绍使用网络卡。

## Adding Modem/PPP/SLIP connections — Quick Reference

1. 在 shell 提示符下输入 linuxconf 启动 Linuxconf。
2. 打开 [Config] -> [Networking] -> [PPP/SLIP/PLIP]。
3. 选择 Add。
4. 选择连接类型。
5. 输入电话号码、登录名和密码。
6. 仅在必要时选择 Use PAP authentication only（仅适用于 PPP 账户）。
7. 选择 Accept。

## Adding Modem/PPP/SLIP connections — General Overview

在让你的 PPP 或 SLIP 账户工作之前，你需要从你的 ISP（Internet Service Provider）或系统管理员那里获取几条信息。对于某些提供商，你可能需要查阅如何在 Linux 系统上设置 PPP 连接的说明。一些 ISP 不善于处理使用 Linux 的个人。别担心，你仍然可以连接；你只需要从你的 ISP 获取一些额外信息。以下是在 Red Hat Linux 上连接所需的内容。ISP 代表可能会回复你不需要这些信息，或者可能会建议

