
打开组 set-GID 位会导致在 /var/toyprojects（及其子目录）中创建的所有文件和目录都被分配给 toygroup 组，而不管是谁创建的。因为我将组权限设置得很宽松（7），因此在 /var/toyprojects 及其子目录中创建的任何内容都将完全受 toygroup 组中任何成员的控制。这是在组项目中共享文件的一种不错技巧。

> **CAUTION:** 设置 set-UID 和 GID 位可能很危险，特别是如果 root 用户打开了执行权限。任何人只要从 Linux 运行带有 set-UID 或 GID 位的应用程序，就会拥有与关联用户或组完全相同的权限来使用该应用程序执行操作。这可能包括覆盖关键系统文件。

一旦创建了顶级目录，netatalk 将会在 Mac 客户端添加文件和文件夹时创建其所需的文件和目录（例如 .AppleDouble 和 Network Trash Folder）。Netatalk 还应将正确的权限传播到这些项目。

以下是有关设置权限的一些提示：

- 用户必须对 .AppleDesktop 目录（及其子目录）具有写权限，才能在共享目录中创建应用程序。
- 将 Network Trash Folder 的权限设置为对有权访问共享卷的每个人都可写，否则他们的文件将始终被永久删除而不是放入此处。
- 对 Temporary Items 目录或应用程序（如 Photoshop）的权限开放将导致无法使用共享卷上的文件。
- 关闭对程序（可执行文件）的写权限以防止它们被利用。

## Setting Appletalk file/folder type and creator

要检查 Mac 文件的类型和创建者属性，请按如下方式使用 `file` 命令：

```
# file file
```

在上述形式中，您可以看到已知类型的文件和目录的属性。要查看所有文件（即使是 .AppleDouble 目录中未存储关联属性的文件），请使用 -a 选项对 `file`。

使用 `file` 命令更改 Macintosh 文件的类型（-t）和创建者（-c）。创建者/文件类型对在 /etc/atalk/AppleVolumes.system 文件中定义。您可以更改这些条目以使所选文件类型使用不同的应用程序。

## Moving, copying, and deleting netatalk files

当您从 Mac 客户端计算机访问 netatalk 卷上的文件时，文件属性会被正确维护或删除。然而，Linux 命令不处理 Mac 文件属性，因此您需要从 Linux 运行特殊命令来移动这些文件并维护其属性，而不是使用常规的 Linux 命令（mv、cp、rm 等）。

NOTE: 在使用 apple_cp 和相关命令将文件添加到您的 AppleTalk 卷之前，请从 Mac 客户端打开该卷并在其中创建一个文件。这将导致创建适当的目录和文件（.AppleDouble 等），以便从 Linux apple_** 命令添加属性。

从 shell 在您的 Netatalk 服务器卷上复制、移动和删除文件的命令分别是 apple_cp、apple_mv 和 apple_rm。例如：

```
# apple_cp mem01.doc /var/av1/memos/
```

此命令将当前目录中的 mem01.doc 文件复制到 /var/av2/memos/ 目录（ presumably 在同一个 Netatalk 卷上）。此操作还会将与文件关联的资源分支复制到 .AppleDouble 目录到您要移动到的目录。以下是移动和删除命令的示例：

```
# apple_mv mem01.doc /var/av1/memos/oldmemos/
# apple_rm mem01.doc
```

apple_mv 命令将 mem01.doc 文件从当前目录移动到 oldmemos 目录（将属性信息从 .AppleDouble 移动到新的 .AppleDouble 目录）。apple_rm 命令删除 mem01.doc 并删除其属性信息。

## Sharing files with Netatalk and Samba

如果同一网络上同时有 Mac 和 Windows 客户端需要共享相同的文件，则常见的做法是让 Samba 和 Netatalk 配置为共享同一卷（即一组目录）。在这样做之前，请注意以下事项：

- 默认情况下，从 Mac 客户端（在 Netatalk 卷上）创建的文件将最易于从 Mac 使用。
- 您可以使用 AppleVolumes.default 中的 veto 选项隐藏 Samba 用户的文件（从 Linux，参见 /usr/share/doc/netatalk\*/doc/README.veto 文件。）
- 如果您不关心 Mac 属性，可以在 AppleVolumes.default 文件中设置 noadouble 选项以创建没有它们的文件。
- 在文件和目录名称中避免使用某些字符可以更轻松地在不同类型的客户端之间共享这些项目。尽可能在命名文件时避免使用斜杠（/）、反斜杠（\）和冒号（:）等字符。此外，通配符字符如星号（*）和井号（#）也可能导致问题。
- Samba 的 veto 选项（在 smb.conf 中）可用于从 Samba 用户那里隐藏 Mac 文件（如 .AppleDouble 目录）。

以下是您可能希望添加到 /etc/samba/smb.conf 文件中的 veto 行示例。它防止 Samba 用户访问隐藏的 Netatalk 特定目录：

```
veto files = / .AppleDouble/.AppleDesktop/Network Trash Folder/TheVolume/SettingsFolder
```

以下是您可以添加到 `/etc/atalk/atalkd.conf` 文件中的 veto 行，以防止 netatalk 用户访问 Samba 使用的目录：

```
veto: recycled/desktop.ini/Folder.htt/Folder Settings/
```

以下是与 `veto` 选项相关的一些问题：

- 注意大小写是否正确（该选项区分大小写）。
- 完整输入 veto 名称。veto 功能不支持星号（`*`）、括号（`[]`）和其他通配符字符来匹配多个文件名。

## Printer Sharing

您可以使用 netatalk 设置打印机共享，以便使用标准 AppleTalk 打印服务（称为 *Printer Access Protocol*，或 **PAP**）的 Mac 客户端可以向您的 Linux 计算机打印。为此，您必须：

- 配置本地 Linux 打印机（参见第 17 章）。
- 设置 `/etc/atalk/papd.conf` 文件以指向该打印机。
- 重新启动 atalk 服务（或更具体地说，`papd` 守护进程）。

当 Mac 客户端向以这种方式配置的 Linux 打印机打印时，打印作业会被交给标准 Linux `lpd` 守护进程并放入用于打印的 spool 文件中，与该打印机的 Linux 打印作业一起。

> **NOTE:** Mac OS X 计算机可以直接打印到 Linux 打印服务（CUPS 或 LPRng），而无需 netatalk 打印。然而，较旧的 Mac OS/9 客户端可能需要看到您以这种方式使用 netatalk 设置的 AppleTalk 打印机。

`papd.conf` 文件遵循与 `/etc/printcap` 文件相同的基本格式（传统上用于 Linux 打印）。以下是 `papd.conf` 文件中配置的打印机示例：

```
LaserJet 2100M:\
:pr=l /usr/bin/lpr -P hp01:\
:pd=/etc/atalk/laserjet.ppd:\
:op=root:\
:am=uams_guest.so:
```

此示例中的打印机名为 **LaserJet2100M**。要从 Mac 客户端打印文件，它会将输出文件通过管道传输到 `lpr -P hp01` 命令（`hp01` 是本地打印机的名称）。`ppd` 文件为 `/etc/atalk/laserjet.ppd`。root 用户是操作员，允许访客打印到打印机（无需密码）。

打印机定义文件（`ppd`）必须安装在 netatalk 服务器（`papd.conf` 文件中注明的 location）和 Mac 客户端上。

要测试 AppleTalk 打印机的接口是否正常工作，请使用 *pap* 命令：

```
# pap -p LaserJet2100M /etc/hosts
```

*-p* 选项标识您的 netatalk 打印机。在此示例中，它打印您 */etc/hosts* 文件的副本。或者，您也可以仅检查打印机的状态：

```
# papstatus -p LaserJet2100M
```

### Troubleshooting netatalk

有多个工具可用于查看 AppleTalk 网络的状态。*aecho* 命令可以测试特定 AppleTalk 主机计算机是否处于活动状态。*nbplookup* 命令可用于检查当前在 AppleTalk 网络上可用的服务。

> **NOTE:** 通常，AppleTalk 应在受信任的网络上使用。但是，如果您在 netatalk 服务器上运行防火墙，则必须为 netatalk 工作打开多个端口。特别是，您可能需要打开端口 548（AFP over TCP/IP）、201（AppleTalk 路由）、202（AppleTalk 名称绑定）、204（AppleTalk 回显）和 206（AppleTalk 区域）。

使用 *aecho* 命令（类似于 TCP/IP *ping* 命令）来检查 AppleTalk 主机计算机是否处于活动状态。*aecho* 命令向您要检查的主机发送 Apple Echo Protocol（aep）数据包。以下是一个示例：

```
# aecho toys
14 bytes from 65280.115: aep_seq=0. time=0, ms
14 bytes from 65280.115: aep_seq=1. time=0, ms

---65280.115 AEP Statistics----
2 packets sent, 2 packets received, 0% packet loss
round-trip (ms) min/avg/max = 0/0/0
```

如果 AppleTalk 服务器已启动并正在运行，您可以使用 *nbplookup* 命令查看当前可用的打印机和卷。对于大型网络，您可以通过添加共享名称或打印机名称（如 ``:hpjet``）或输入主机名（例如 *toys*）来限制 *nbplookup* 的输出。以下是一个示例：

```
# nblookup :AFPServer
duck:AFPServer 65280.115:130
User Volume:AFPServer 65280.21:129
Guest Volume:AFPServer 65280.21:130
```

通过查询 :AFPServer，*nbplookup* 列出了本地网络上的所有 AppleTalk 文件服务器。显示的第一个来自名为 *duck* 的主机。第二行和第三行来自同一台计算机（地址为 65280.21），但注册为单独的服务器。

