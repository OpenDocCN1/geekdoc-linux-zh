

options—这些是你可能想要设置的其它选项

+   - prodos—此选项使卷与 AppleII 客户端兼容。
+   - crlf—此选项为文本文件启用 crlf 翻译。

noadouble—如果不想浪费时间清理，这个选项很重要。afpd 会创建两个名为 .AppleDesktop 和 Network Trash Folder 的目录。你访问的每个目录都会在其下创建一个 .AppleDouble，以便存储资源分支。你需要此选项来告诉 afpd 不要创建 .AppleDouble，除非需要创建资源分支。

codepage—此选项从目录加载 nls 代码页文件名。在此选项中，你只需输入文件名的路径。

dbpath—此选项告诉 afpd 在何处存储卷数据库文件。你必须指定一个路径。

password—如果你想用密码保护卷，可以通过创建用户在访问卷之前必须输入的密码来实现。

以下是 /etc/AppleVolumes.default 文件中三个用户卷的简单示例：

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
> 如果用户编辑其 .AppleVolume 或 AppleVolume 文件以至于看不到其主目录，她将无法再次访问这些文件，因此也无法修复此问题或应用任何设置。请告诉你的用户在编辑这些文件时要小心，并始终将主目录作为条目记住。

## File Types and Systemwide Settings

Apple 文件名与 Linux 文件名的风格不同。Mac 文件名或目录条目由两个部分组成，数据分支和资源分支。Linux 上的文件名和目录条目仅由一个部分组成。这会导致 Linux 文件名在用户查看 Linux 上共享的卷时显示为未知文档。为了解决这个问题，你必须编辑 /etc/atalk/AppleVolumes.system 文件中的条目，在其中你可以将程序注册到 Apple 以获得官方的创建者映射。以下示例将扩展名为 .moov（*.moov 文件）的文件映射到 Apple 客户端上的 Moov 文件。它还将此文件类型与 mMPG 播放器关联，因此它具有程序图标并显示为电影文件。

```
.moov  Moov  mMPG
```

SuSE Linux 附带了一个很大的 /etc/atalk/AppleVolumes.system 文件，其中已映射了多个文件类型。你可以根据 Apple 客户端侧的现有程序添加或修改这些文件类型。

默认的 cr-lf 转换发生在文本文件类型上。所有文本文件类型在从 Apple 客户端打开时都会被修改，以便修复 cr-lf 差异。但是，/etc/atalk/AppleVolumes.system 文件上的一个选项告诉 afpd 如何处理未知文件类型。不要将此选项设置为将未知文件类型视为文本，否则如果你打开并再次保存它们，你的文件可能会被破坏。你的 /etc/atalk/AppleVolumes.system 文件中应有以下行：

```
.  BINA  UNIX
```

此行告诉 afpd 将未知文件类型视为不应经过任何转换的二进制文件。

## Managing Guest Volumes

如果你了解如何管理用户的卷，管理访客卷就很容易。适用于 /etc/atalk/AppleVolumes.default 文件的相同选项也适用于 /etc/atalk/AppleVolumes.system 文件。在 /etc/atalk/AppleVolumes.system 中，你可以添加访客用户可以使用且通过与 AppleVolumes.default 相同的条件传递的卷——除了与用户名和组相关的条件之外。

## Exporting a Printer to the Apple Network

默认情况下，你的 SuSE Linux 上所有可用的打印机都会被导出，以便 Apple 客户端可以看到它们。但，只有被允许在你的 SuSE Linux 上打印的用户才能在此处打印。访客用户默认情况下不能打印。

要将打印机导出到 Apple 网络，首先必须确保你的 SuSE Linux 可以打印。按照第 11 章“Printing”中的说明在你的 SuSE Linux 上设置打印。

在配置并启动打印服务后，只要他们被允许使用你的 SuSE Linux 打印，从任何 Apple 客户端连接的 Linux 用户就可以使用打印机。有关打印权限的更多信息，请参阅第 11 章。

你可以在 Apple 客户端中关闭后台打印选项，因为 SuSE Linux 仍会进行 spooling。

如果 Apple 客户端尝试打印时打印设施不能开箱即用使用，可能需要一些配置。你需要的配置文件位于 /etc/atalk/papd.conf。此文件是你的 SuSE Linux 盒子的主要配置文件，并使其充当 Apple 打印服务器。该文件的格式如下：

```
Name
pd: Pathname to ppd file.
pr: LPD printer name.
op: Operator name, needed for spooling.
```

你不必使用所有之前的语句。最重要的语句是 Name 和 pr。其他设置通常在你按照第 11 章所述配置打印机时进行。以下是将名为 lp 的打印机（在 /etc/printcap 文件中出现）与你的当前 Apple 区域共享的示例：

```
HP Deskjet 610c:
:pr=lp:
```

在此示例中，LPD 打印机名称为 lp，但从你的区域连接的 Apple 客户端将看到此打印机的名称为 HP Deskjet 610c。

如果你希望从其他区域连接的 Apple 客户端看到你的打印机，该文件会略有不同。如果你希望从 ZONE2 连接的 Apple 客户端看到你的打印机，配置文件将如下例所示：

```
Deskjet@ZONE2:
:pr=lp:
```

现在，从 ZONE2 连接的客户端可以使用你的 SuSE Linux 盒子上的打印机。

## Playing the Client Role

Apple 客户端能够访问你的 SuSE Linux 卷和打印机很重要，但你的 SuSE Linux 能够看到 Apple 卷和打印机也很重要。在以下各节中，你将学习如何在你的 SuSE Linux 上挂载 Apple 设备和卷。你还将学习如何使用 Apple 共享打印机。

## Mounting Apple Devices

在内核中拥有 Apple 文件系统支持后，你可以挂载任何使用 Apple HFS 格式格式化的存储介质。例如，你可以通过发出以下命令挂载在 Apple 机器上格式化的软盘：

```
bash#mount /dev/fd0 -t hfs /floppy
```

之前的命令列出了网络上的所有区域。你也可以使用其他区域的资源，只要你有权限即可。你可以通过在资源名称后附加 @other_zone_name 来使用其他区域的资源。

## Mounting Apple Volumes

SuSE Linux 不支持挂载 Apple 卷，因为该软件包仍处于开发的早期阶段，目前还不安全使用。强烈建议你不要使用此软件包。如果你必须挂载 Apple 卷，请注意要使该软件包工作，你需要将其的一部分作为内核模块安装。由于该模块仍处于早期阶段，它可能会崩溃。如果内核模块崩溃，你的整个系统将崩溃，你将丢失数据。如果你仍必须使用它，请确保你已备份所有重要数据。另请确保在从 Apple 卷获取所需内容后卸载该模块。一般来说，切勿尝试在必须始终保持运行的 SuSE Linux 服务器上运行不稳定的内核模块。

该软件包可从 http://www.panix.com/~dfoster/afpfs/ 获取。搜索软件包源并下载它。下载软件包后，使用以下命令解压并编译它：

```
bash#tar xzvf <package_name.tar.gz>
bash#cd <package_name>
bash#make
```

你必须先配置 netatalk，然后才能实际挂载 Apple 卷。

你还需要加载 afpfs 模块，你可以使用以下命令完成：

```
bash#/sbin/insmod ./afpfs.o
```

加载模块后，你可以使用 afpmount 命令挂载 Apple 卷。该命令接受以下参数：

```
afpmount -u <username> -p <password> mount-point servername[@zone] volume-name
```

以下是将名为 Joe（属于 ZONE1 区域）的 Apple 机器上的名为 Shared 的卷挂载到挂载点 /mnt/mac 的示例：

```
afpmount -u joeadlib -p mypass /mnt/mac 'Joe@ZONE1' 'Shared'
```

你也可以通过使用普通的 mount 命令来挂载 Apple 共享。

## Printing to an Apple Shared Printer

首先，你应该查找共享打印机的名称。你可以通过发出此命令搜索你的区域中可用的打印机：

```
bash#nbplkup
```

这将返回该区域中所有可用资源列表。假设例如，你发现输出包含以下行：

```
Shared Printer:LaserWriter 12398.73:191
```

