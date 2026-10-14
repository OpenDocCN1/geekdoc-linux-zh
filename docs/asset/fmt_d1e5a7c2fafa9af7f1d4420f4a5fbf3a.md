
你应将此行修改为连接到 Apple 网络的网卡的名称。在运行 `atalkd` 服务并完成 `netatalk` 包的配置后，`atalkd` 守护进程将向此文件添加更多行。

# 在 SuSE Linux 上添加 Apple 卷

在设置 `atalkd.conf` 和 `afpd.conf` 文件（网络配置文件）之后，你必须管理在 Apple 网络上作为 Apple 卷出现的 Linux 共享。三个主要的卷配置文件如下：

- `/etc/atalk/AppleVolumes.system`—此文件用于设置用户登录和系统用户可以看到的卷。此文件还包含访客账户的设置。
- `/etc/atalk/AppleVolumes.default`—此文件用于设置用户访问和系统用户可以看到的卷。
- `AppleVolumes` 或 `.AppleVolumes` 在用户的主目录中—如果任何用户在其主目录中有这两个文件中的任何一个，则该文件中的设置将覆盖 `AppleVolume.defaut` 文件中的设置。

# 管理用户的卷

当 `afpd` 启动时，它将读取 `/etc/atalk/AppleVolumes.system` 中的系统范围设置。然后它将读取 `/etc/atalk/AppleVolumes.default` 文件以获取用户登录信息。如果用户在其主目录中有 `AppleVolumes` 或 `.AppleVolumes` 文件，则将读取该文件而不是默认文件。

随 SuSE Linux 提供的 `AppleVolumes.default` 文件仅包含 `~` 路径。换句话说，它在登录时仅显示用户的主目录。

> NOTE 有关管理用户卷时的系统安全性的更多信息，请参阅章节“设置 `afpd`”。大多数安全调整都是通过管理 `/etc/atalk/afpd.conf` 完成的。此外，用户必须为每个用户组拥有 `AppleVolumes.default` 和 `AppleVolumes.system` 文件，并在 `/etc/atalk/afpd.conf` 中为每个用户组提供一个条目。

`AppleVolumes.default` 语法格式如下：

```
path [name] [casefold=x] [codepage=y] [options=z,l,j]

path [name] [access=a,@b,c,d] [dbpath=path] [password=p]
```

要为卷设置条目，你必须在单独的行上输入每个条目。

- `path`—这是 SuSE Linux 盒子上卷的路径。它可以是用户通过其用户权限可以访问的任何路径。
- `casefold`—此选项用于设置文件和目录的字母大小写。`casefold` 选项可以接受以下值：
  - `tolower`—在客户端和服务器两侧都将名称小写。
  - `toupper`—在客户端和服务器两侧都将名称大写。
  - `xlatelower`—在客户端侧小写，在服务器侧大写。
  - `xlateupper`—在客户端侧大写，在服务器侧小写。
- `access`—此选项用于将卷访问限制为列出的用户和组。列表使用逗号分隔用户名和组名。用户和组按其 Linux 用户名列出。在组名前加上 at 符号（`@`）。此选项的示例是 `user1,@group,user2`。

`options`—这些是你可能想要设置的其它选项

+   `-prodos`—此选项使卷与 AppleII 客户端兼容。
+   `-crlf`—此选项为文本文件启用 crlf 翻译。

`noadouble`—如果不想浪费时间清理，这个选项很重要。`afpd` 会创建两个名为 `.AppleDesktop` 和 `Network Trash Folder` 的目录。你访问的每个目录都会在其下创建一个 `.AppleDouble`，以便存储资源分支。你需要此选项来告诉 `afpd` 不要创建 `.AppleDouble`，除非需要创建资源分支。

`codepage`—此选项从目录加载 nls 代码页文件名。在此选项中，你只需输入文件名的路径。

`dbpath`—此选项告诉 `afpd` 在何处存储卷数据库文件。你必须指定一个路径。

`password`—如果你想用密码保护卷，可以通过创建用户在访问卷之前必须输入的密码来实现。

以下是 `/etc/AppleVolumes.default` 文件中三个用户卷的简单示例：

```
#The following entry specifies that a user
#can see his home directory.
~ "HOME"

#The following entry specifies that a user can see
#the mp3 directory on the server
#On the Apple side, the volume name will be
# MUSIC DIRECTORY
/usr/local/share/mp3 "MUSIC DIRECTORY"

#The following entry specifies that a user can see
#the downloads directory on the server if he belongs
#to the root group
/usr/local/share/downloads "DOWNLOADS" @root
```

> CAUTION
> 如果用户编辑其 `.AppleVolume` 或 `AppleVolume` 文件以至于看不到其主目录，她将无法再次访问这些文件，因此也无法修复此问题或应用任何设置。请告诉你的用户在编辑这些文件时要小心，并始终将主目录作为条目记住。

## File Types and Systemwide Settings

Apple 文件名与 Linux 文件名的风格不同。Mac 文件名或目录条目由两个部分组成，数据分支和资源分支。Linux 上的文件名和目录条目仅由一个部分组成。这会导致 Linux 文件名在用户查看 Linux 上共享的卷时显示为未知文档。为了解决这个问题，你必须编辑 `/etc/atalk/AppleVolumes.system` 文件中的条目，在其中你可以将程序注册到 Apple 以获得官方的创建者映射。以下示例将扩展名为 `.moov`（`*.moov` 文件）的文件映射到 Apple 客户端上的 Moov 文件。它还将此文件类型与 `mMPG` 播放器关联，因此它具有程序图标并显示为电影文件。

```
.moov  Moov  mMPG
```

SuSE Linux 附带了一个很大的 `/etc/atalk/AppleVolumes.system` 文件，其中已映射了多个文件类型。你可以根据 Apple 客户端侧的现有程序添加或修改这些文件类型。

默认的 cr-lf 转换发生在文本文件类型上。所有文本文件类型在从 Apple 客户端打开时都会被修改，以便修复 cr-lf 差异。但是，`/etc/atalk/AppleVolumes.system` 文件上的一个选项告诉 `afpd` 如何处理未知文件类型。不要将此选项设置为将未知文件类型视为文本，否则如果你打开并再次保存它们，你的文件可能会被破坏。你的 `/etc/atalk/AppleVolumes.system` 文件中应有以下行：

```
.  BINA  UNIX
```

此行告诉 `afpd` 将未知文件类型视为不应经过任何转换的二进制文件。

## Managing Guest Volumes

如果你了解如何管理用户的卷，管理访客卷就很容易。适用于 `/etc/atalk/AppleVolumes.default` 文件的相同选项也适用于 `/etc/atalk/AppleVolumes.system` 文件。在 `/etc/atalk/AppleVolumes.system` 中，你可以添加访客用户可以使用且通过与 `AppleVolumes.default` 相同的条件传递的卷——除了与用户名和组相关的条件之外。

## Exporting a Printer to the Apple Network

默认情况下，你的 SuSE Linux 上所有可用的打印机都会被导出，以便 Apple 客户端可以看到它们。但，只有被允许在你的 SuSE Linux 上打印的用户才能在此处打印。访客用户默认情况下不能打印。

要将打印机导出到 Apple 网络，首先必须确保你的 SuSE Linux 可以打印。按照第 11 章“Printing”中的说明在你的 SuSE Linux 上设置打印。

在配置并启动打印服务后，只要他们被允许使用你的 SuSE Linux 打印，从任何 Apple 客户端连接的 Linux 用户就可以使用打印机。有关打印权限的更多信息，请参阅第 11 章。

你可以在 Apple 客户端中关闭后台打印选项，因为 SuSE Linux 仍会进行 spooling。

如果 Apple 客户端尝试打印时打印设施不能开箱即用使用，可能需要一些配置。你需要的配置文件位于 `/etc/atalk/papd.conf`。此文件是你的 SuSE Linux 盒子的主要配置文件，并使其充当 Apple 打印服务器。该文件的格式如下：

```
Name

pd: Pathname to ppd file.

pr: LPD printer name.
```
