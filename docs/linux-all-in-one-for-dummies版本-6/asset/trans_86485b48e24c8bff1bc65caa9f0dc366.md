
现在您已准备好进行自动备份。您需要做的只是每天在磁带驱动器中放入一条新磁带。还请记得为每条磁带贴上适当的标签。

## 访问 DOS 或 Windows 文件系统

如果您使用的是不想丢弃的旧机器，并且硬盘上安装了非常旧版本的 Microsoft Windows，那么您可能已经在 Linux 下挂载了 DOS 或 Windows 分区。如果没有，您可以轻松地在 Linux 中挂载 DOS 或 Windows 分区。挂载会使 DOS 或 Windows 目录层次结构作为 Linux 文件系统的一部分出现。

## 挂载 DOS 或 Windows 磁盘分区

要在 Linux 中挂载 DOS 或 Windows 硬盘分区或存储设备，请使用 mount 命令，但包含选项 -t vfat 以将文件系统类型指定为 DOS。如果您的 DOS 分区恰好是 IDE（集成驱动电子设备）驱动器上的第一个分区，并且您想将其挂载到 /dosc，请使用以下 mount 命令：

```
mount -t vfat /dev/hda1 /dosc
```

-t vfat 部分指定您要挂载的设备 — /dev/hda1 — 具有 MS-DOS 文件系统。图 3-4 说明了此 mount 命令的效果。

图 3-4 显示了 DOS 分区中的目录如何映射到 Linux 文件系统。在 DOS 下原本是 C:\DOS 的目录在 Linux 下变为 /dosc/dos。同样，C:\WINDOWS 现在是 /dosc/windows。您大概能看出规律。要将 DOS 文件名转换为 Linux（当您将 DOS 分区挂载到 /dosc 时），请执行以下步骤：

- 1. 将 DOS 名称更改为小写。
- 2. 将 C:\ 更改为 /dosc/。
- 3. 将所有反斜杠（\）更改为斜杠（/）。

![](img/322157d1fa7d965f05bcd68ed0ffc36b_365_0.png)

图 3-4：
以下是如何在 /dosc 目录上挂载 DOS 分区。

## 挂载那些古老的 DOS 软盘

就像您将 DOS 硬盘分区挂载到 Linux 文件系统一样，您也可以在旧机器上挂载 DOS 软盘。您必须以 root 身份登录才能挂载软盘，但您可以设置系统，使任何用户都可以挂载 DOS 软盘。您还需要知道软盘驱动器的设备名称。默认情况下，Linux 定义了以下两个通用软盘设备名称：

- /dev/fd0 是 A 驱动器（第一个软盘驱动器）。
- /dev/fd1 是 B 驱动器（第二个软盘驱动器，如果您有的话）。

您可以使用文件系统中的任何空目录作为挂载点，但 Linux 系统自带一个目录，/media/floppy，专门用于挂载软盘。

要将 DOS 软盘挂载到 /media/floppy 目录，请将软盘放入驱动器中，然后键入以下命令：

```
mount -t vfat /dev/fd0 /media/floppy
```

![](img/322157d1fa7d965f05bcd68ed0ffc36b_366_0.png)

## 挂载那些旧的 DOS 软盘

您可以设置 Linux 系统，使任何用户都可以挂载 DOS 软盘。例如，要使任何用户都可以在 /a 目录上挂载 A 驱动器中的 DOS 软盘，请执行以下步骤：

- **1. 以 root 身份登录。**
- **2. 通过在终端窗口中键入以下命令创建 /a 目录（挂载点）：**
  `mkdir /a`
- **3. 在文本编辑器（如 vi 或 emacs）中编辑 /etc/fstab 文件，插入以下行，然后保存文件并退出编辑器：**
  `/dev/fd0 /a vfat noauto,user 0 0`
  该行中的第一个字段是软盘驱动器的设备名称（/dev/fd0）；第二个字段是挂载目录（/a）；第三个字段显示文件系统类型（vfat）。user 选项（紧跟在 noauto 之后）使所有用户都可以挂载 DOS 软盘。
- **4. 注销然后以普通用户身份重新登录。**
- **5. 为确认您可以用普通用户而不仅仅是 root 挂载 DOS 软盘，请将 DOS 软盘插入 A 驱动器，然后键入以下命令：**
  `mount /a`
  挂载操作成功，并且当您键入命令 ls /a 时，您会看到 DOS 软盘的列表。
- **6. 要卸载 DOS 软盘，请键入 umount /a。**

```
mkdir /a
```

```
/dev/fd0 /a vfat noauto,user 0 0
```

```
mount /a
```

挂载软盘后，您可以使用 Linux 复制命令（cp）将文件复制到软盘和从软盘复制。要将当前目录中的文件 gnome1.pcx 复制到软盘，请键入以下内容：

```
cp gnome1.pcx /media/floppy
```

同样，要查看软盘的内容，请键入以下内容：

```
ls /media/floppy
```

如果您想从驱动器中取出软盘，请先卸载软盘驱动器。卸载会移除软盘文件系统与 Linux 文件系统上的挂载点之间的关联。使用 umount 命令卸载软盘，如下所示：

```
umount /dev/fd0
```

## 挂载 NTFS 分区

如今，大多数 PC 在硬盘上预装了 Windows 10 或 Windows 8。这两个版本的 Windows 以及较旧的 Windows 7、Vista 和 XP 通常使用 NT 文件系统（NTFS）。Linux 支持对 NTFS 分区的只读访问，许多发行版都附带 ntfs.ko 内核模块，该模块是访问 NTFS 分区所必需的。

如果您在 Windows 系统上安装了 Linux 并希望访问 NTFS 分区上的文件，但您的发行版不包含 ntfs.ko 模块，您可以在内核配置步骤中启用 NTFS 模块后构建内核。

重新构建并从新内核启动后，以 root 身份登录，然后键入以下命令为 NTFS 分区创建挂载点。（在这种情况下，您正在 /mnt 目录中创建挂载点。）

```
mkdir /mnt/windir
```

现在您可以使用以下命令挂载 NTFS 分区：

```
mount /dev/hda2 /mnt/windir -t ntfs -r -o umask=0222
```

![](img/322157d1fa7d965f05bcd68ed0ffc36b_367_0.png)

如有必要，请将 /dev/hda2 替换为您系统上 NTFS 分区的设备名称。在大多数预装 Windows 的 PC 上，NTFS 分区是第二个分区（/dev/hda2）；第一个分区（/dev/hda1）通常是隐藏分区，其中包含用于 Windows 安装的文件。

## 本章内容

- 使用网络文件系统共享文件
- 安装和配置 Samba

## 第 4 章

## 使用 Samba 和 NFS

如果您的局域网（LAN）与其他大多数网络类似，它需要能够在运行 Linux 的系统和其他系统之间共享文件的功能。虽然随着 Linux 使用量的增长，这一比例可能在缩小，但它仍然太大而无法忽视。因此，Linux 包含两个突出的文件共享服务：

- Network File System (NFS)：用于与其他 Unix 系统（或具有 NFS 客户端软件的 PC）共享文件
- Samba：用于与 Windows 系统共享文件和打印机

本章描述了如何使用 NFS 和 Samba 共享文件。

## 使用 NFS 共享文件

通过 NFS 共享文件很简单，涉及两个基本步骤：

- 在运行 NFS 服务器的 Linux 系统上，您通过在 /etc/exports 文件中列出它们并运行 exportfs 命令来导出（共享）一个或多个目录。此外，您必须启动 NFS 服务器。

在每个客户端系统上，您使用 mount 命令挂载服务器导出的目录。

使用 NFS 的唯一问题是每个客户端系统都必须支持它。Microsoft Windows 不附带 NFS，因此如果您想使用 NFS 共享文件，则必须单独购买 NFS 软件。然而，如果您局域网上的所有系统都运行 Linux（或其他具有内置 NFS 支持的 Unix 变体），使用 NFS 是有意义的。

![](img/322157d1fa7d965f05bcd68ed0ffc36b_370_0.png)

NFS 存在安全漏洞，因此如果不使用随 NFS 版本 4（NFSv4）提供的 RPCSEC_GSS 安全机制，就不应在直接连接到 Internet 的系统上设置 NFS。版本 4.2 于 2016 年 11 月发布；您应将其用于大多数用途，因为它包含所有所需更新。

下几节将指导您进行 NFS 设置，使用局域网上两台 Linux PC 的示例。

## 使用 NFS 导出文件系统

从导出服务器系统开始 — 使客户端系统可用 — 目录的内容。在服务器上，您必须运行 NFS 服务并指定一个或多个要导出的文件系统。

要导出文件系统，您必须在 /etc/exports 文件中添加适当的条目。假设您想导出 /home 目录，并希望启用名为 LNBP75 的主机以便进行读写操作挂载此文件系统。您可以通过向 /etc/exports 文件添加以下条目来实现：

```
/home LNBP75(rw,sync)
```

如果您想为 192.168.0.0 等局域网上的所有主机提供访问权限，您可以将此行更改为

```
/home 192.168.0.0/24(rw,sync)
```

/etc/exports 文件中的每一行都有以下通用格式：

```
Directory host1(options) host2(options) ...
```

第一个字段是通过 NFS 共享的目录，其后是一个或多个字段，指定哪些主机可以远程挂载该目录以及括号中的几个选项。您可以使用名称或 IP 地址指定主机，包括地址范围。
