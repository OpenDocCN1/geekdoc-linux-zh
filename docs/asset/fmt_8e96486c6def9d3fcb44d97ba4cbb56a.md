
```
mount /dev/hdb /mnt/zip
```

本示例使用了 `/dev/hdb`。IDE Zip 驱动器可以是 `/dev/hda`、`/dev/hdb`、`/dev/hdc` 或 `/dev/hdd`

如果您想使用 DOS 格式格式化的 Zip 磁盘，请使用以下命令：`mount -t mdos /dev/hdb4 /mnt/zip`

要使用软盘，命令应为：

```
mount /dev/fd0 /mnt/floppy
```

# 创建文件驱动器

打开驱动器管理窗口，然后从服务器管理窗口点击设备（Devices）-> 驱动器管理（Drives management）。创建一个名为 File Drive 的新驱动器。从驱动器管理窗口点击新建（New），输入名称 File Drive，类型为 FILE。勾选复选框，新驱动器名称将出现在右侧菜单中。再次勾选复选框返回服务器管理窗口。

# 创建驱动包

打开驱动器管理窗口，然后从服务器管理窗口点击设备（Devices）→ 驱动包（Drivepacks）。创建一个名为 File Drive 的新驱动包。从驱动包窗口点击新建（New），输入名称 File Drive，并勾选复选框，新驱动包名称将出现在右侧菜单中。再次勾选复选框返回服务器管理窗口。

# 创建新池

打开驱动器管理窗口，然后从服务器管理窗口点击设备（Devices）→ 池（Pools）。创建一个名为 File Pool 的新池。从池窗口点击新建（New），输入名称 File Pool，并勾选复选框，新池名称将出现在右侧菜单中。再次勾选复选框返回服务器管理窗口。

# 将磁带添加到池

打开池管理窗口，然后从服务器管理窗口点击设备（Devices）→ 添加到池（Add to Pool）。从列表中选择您想要添加磁带的池。然后从列表中选择您想要添加的磁带并点击添加（Add）按钮。Arkeia 将将磁带添加到池中。

# 创建文件库

文件库不用于驱动包。然而，任何使用磁带驱动器的备份都需要定义一个库。当您使用磁盘（软盘、硬盘）作为存储介质时，目录将显示为库。（使用独立驱动器执行的备份不需要定义库。如果您有磁带驱动器，那么在进行任何备份之前将需要定义并配置库。）

打开库管理窗口。从服务器管理窗口点击设备（Devices）→ 库管理（Libraries management）。创建一个名为 FileLib 的新库。从库管理窗口点击新建（New），输入名称 FileLib 并点击 FILE。勾选复选框，新库名称将出现在右侧菜单中。

点击驱动选项（Drive Options）按钮，它是底部从左起第第六个按钮。驱动库：FileLib 窗口现在应该出现。点击连接驱动器（Attach Drive）按钮，它位于窗口左下角，连接驱动器：FileLib 窗口激活。

勾选复选框，Arkeia 将将驱动器（FileDrive）与库关联。

再次勾选复选框返回库管理窗口。点击插槽使用（Slot usage）按钮，它是从左起第第七个按钮（连接驱动器使用的右侧），库插槽：File 窗口将出现。应该列出 100 个插槽，磁带字段显示为无磁带（No Tape）。点击前五个插槽每个插槽字段中的按钮。（如果您的窗口颜色映射正确，设置后按钮将变为橙色。）

点击设置磁带（Set tape）按钮，它位于窗口左下角。磁带管理窗口应激活并显示 Tapes-1 到 FileTape-5。

通过点击每个磁带名称左侧的按钮来选择磁带 1 到 5；您也可以使用窗口底部从左起第五个全选（Select All）按钮。如果您的 X 窗口颜色映射正确，设置后按钮应会变为橙色。

勾选复选框按钮。

您返回库插槽：File 窗口，并应看到 FileTape-1 到 FileTape-5。

# 第 10 章：全网络备份自动化

在 Voltag 子窗口中列为 `/mnt/zip/FileTape-1`, `/mnt/zip/FileTape-2`。

点击复选框返回库管理窗口，再次返回服务器管理窗口。

# 创建备份包 (CREATE A SAVEPACK)

打开 Savepack 管理窗口。在服务器管理窗口中，点击 Backup（备份）→ Savepacks（备份包）。

创建一个名为 FileSave 的新备份包，然后在 Savepacks 管理窗口中点击回车键（Enter）、名称 FileSave 并勾选复选框。

将一个或多个文件系统附加到备份包上。在 Savepacks 管理窗口中，点击 Savepacks 子菜单中 FileItem 旁边的框（该框应变为橙色）。点击屏幕底部左侧的 Navigator（导航）按钮，它是左侧的第四个按钮。

请记住你通过点击服务器图标左侧的按钮（在本例中为 chivas）选择了备份你的服务器的整个文件系统。但是，如果可能，双击 chivas 图标，你将看到显示的所有顶层目录。点击 `/etc` 目录，然后点击复选框，控制权返回 Savepacks 管理窗口。

点击复选框，返回服务器管理窗口。

# 执行测试备份 (MAKE A TEST BACKUP)

打开交互式备份窗口。在服务器管理窗口中，点击 Backup（备份）→ Interactive（交互式）。

出现交互式备份窗口。原始的 Testhp应该出现在 Savepacks 子菜单中。点击菜单（menu）并选择 FileSave 备份包。

点击复选框和 Arkeia 窗口。它会像以前一样显示你的备份信息。备份应该会运行很快，结果将出现在窗口底部。

请注意，在配置交互式备份时，你可以选择将不同的备份包（savepacks）与不同的驱动器包（drivepacks）以及不同的池（pools）相关联。这为你提供了一种灵活使用资源的方法。

# 使用 SCSI 磁带驱动器或磁带库

为了更好地利用此备份系统，你可能需要一个能够存储 GB 级设备。最常见的介质是 DAT 驱动器。它们在第 6 章中已简要讨论。

本书没有详细描述使用 DAT 驱动器或真实磁带库的过程。接下来的段落提供了如果你有一个 DAT 驱动器，如何找到其相关信息的信息。它指出了为了适应此类驱动器，你应该更改上一个示例中的哪些部分。

在不购买磁带库的情况下，可以使用 4mm 或 8mm DAT 驱动器。它们通常是 SCSI 设备。最好购买一个良好的 SCSI 控制器来配合 DAT 使用。（从技术上讲，用于数据存储的磁带被称为 DDS，但通常称为 DAT。）

如果你想使用 SCSI 驱动器，请查阅 `/usr/doc/HOWTO/HARDWAREHOWTO` 获取安装的详情。Linux 带有许多 SCSI 驱动程序。一旦安装并配置，DAT 设备将显示类似于 `/dev/st0` 或 `/dev/st1`。

Arkeia 在你的内联文档中提供了安装和配置信息。使用你的浏览器查看 `file:/usr/doc/arkeisererver-4.0.9/html/setup.htm` 和 `file:/usr/doc/arkeisererver4.0.9/html/install/setup.htm` 以获取配置 Arkeia 用于 DAT 磁带、磁带库和其他设备的详细信息。

# 配置 Windows 客户端 (Configuring a Windows Client)

Arkeia 提供了一个 Windows 95 客户端。它存储在随附 CD-ROM 上 `/mnt/cdrom/IDG/Arkeia` 目录下的 windows.zip 文件中。要安装 Windows 客户端，请以 root 身份登录，安装 unzip 程序（gunzip 无法处理 .zip 文件）并使用以下命令进行解压：

```
rpm -ivh /mnt/cdrom/RedHat/RPMS*
mdir /var/tmp/arkeia
cd /var/tmp/arkeia
unzip /mnt/cdrom/IDG/Arkeia/client
```

你可以将解压后的文件拷贝到 Windows 机器，然后运行 Arkeia 软件。但更灵活的方法是将其共享到 Linux 服务器上，这样在 Windows 机器上就可以访问。如果需要，请通过编辑 `/etc/smb.conf` 文件：

```
[arkeia]
path = /var/tmp/arkeia
public = yes
```
