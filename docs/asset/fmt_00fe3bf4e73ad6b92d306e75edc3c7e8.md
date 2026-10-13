
```
D: counting packages to uninstall
D: opening database in /var/lib/rpm/
D: found 1 packages to uninstall
D: uninstalling record number 88728
D: will remove files test = 1
D: /usr/doc/taper-6.8.2/WARNING - removing
D: /usr/doc/taper-6.8.2/VERSION6.8 - removing
D: /usr/doc/taper-6.8.2/FAQ.txt - removing
D: /usr/doc/taper-6.8.2/CREDITS - removing
D: /usr/doc/taper-6.8.2/COPYING - removing
D: /usr/doc/taper-6.8.2/COMPRESSION - removing
D: /usr/doc/taper-6.8.2/CHANGES.html - removing
D: /usr/doc/taper-6.8.2/BUGS - removing
D: /usr/doc/taper-6.8.2 - removing
D: /sbin/taper - removing
D: /sbin/bg_restore - removing
D: /sbin/bg_backup - removing
D: removing database entry
```

## 使用 kpackage

`kpackage` 客户端随 K Desktop Environment 或 KDE 一起提供，是 `rpm` 程序的图形界面，并在 X Window 系统下运行。您必须以 root 操作员身份登录才能使用 `kpackage` 安装和删除软件。与其他需要 root 权限的命令一样，如果您未以 root 操作员身份登录，请从 X11 终端窗口的命令行启动客户端：

```
# su -c kpackage
```

这将启动 `kpackage`，其窗口将列出系统上已安装的软件包组（如图 22.3 所示）。

### 图 22.3

`kpackage` 客户端随 KDE 一起提供，在 X11 下运行，并使用 `rpm` 命令的数据库在您的 OpenLinux 系统中显示已安装的软件。

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_524_0.png)

请注意，您的 OpenLinux 软件被分组在单独的文件夹下。单击 Administration 下的 Archiving 文件夹前的小加号 (+) 标志，然后单击 `taper` 图标。软件包的描述将出现，如图 22.4 所示。

### 图 22.4

`kpackage` 客户端从系统 `rpm` 数据库中显示已安装软件包的信息。

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_524_1.png)

如果您单击 File List 选项卡，将显示 `taper` 软件包中每个文件及其在 Linux 文件系统中的位置，如图 22.5 所示。要卸载软件，请单击文件信息或文件列表底部的 Uninstall 按钮。

### 图 22.5

`kpackage` 客户端显示已安装软件包中每个文件的名称，并提供一键 Uninstall 按钮来删除软件。

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_525_0.png)

要安装软件包，请选择 File 菜单，然后单击 Open 菜单项。`kpackage` 文件选择对话框将出现，如图 22.6 所示。如果您的 OpenLinux CD-ROM 已插入并挂载，您可以导航到 RPMS 目录并通过双击其名称进行安装。

### 图 22.6

`kpackage` 客户端使用拖放或通过文件选择对话框安装软件。

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_525_1.png)

## 使用 lisa 命令

`lisa` 命令不仅是大多数 OpenLinux 系统管理任务的图形界面程序，还可以安装或删除软件。同样，您必须以 root 操作员身份登录才能使用 `lisa` 安装和删除软件。但是，您不需要运行 X11。

要直接进入软件包管理，请使用其 `--pkg` 选项从命令行启动 `lisa`：

```
# lisa --pkg
```

`lisa` 对话框将出现，如图 22.7 所示。

### 图 22.7

您也可以使用 `lisa` 命令来安装或删除 OpenLinux 软件。

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_526_0.png)

要安装软件包，您必须首先选择目录或文件系统。按 Enter 选择软件包所在的位置。选择对话框将出现，如图 22.8 所示。

### 图 22.8

使用 `lisa` 安装软件时，您必须首先选择软件包的位置。

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_526_1.png)

如果你选择 CD-ROM，`lisa` 会尝试首先检测你的 CD-ROM（你应该先挂载 CD-ROM），确认你的 CD-ROM，然后显示初始对话框（如图 22.7 所示），其中软件安装行（第 3 行）处于高亮状态。按 Enter 进入安装对话框，如图 22.9 所示。

### 图 22.9

`lisa` 命令在其软件安装对话框中使用可滚动的文件列表。

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_527_0.png)

在 CD-ROM 上的 `.rpm` 文件列表与 OpenLinux 系统 `rpm` 数据库中已安装的 `.rpm` 文件列表进行比较后，会显示可用软件包的列表。要选择文件，请滚动列表并按空格键。完成后，按 Enter 安装软件。

要删除软件，请在主软件管理对话框中（如图 22.7 所示）选择软件删除项并按 Enter。你将看到系统上已安装软件包的列表（如图 22.10 所示）。要删除软件包，请滚动列表并按空格键。完成后，按 Enter 删除软件。

### 图 22.10

`lisa` 命令在其软件删除对话框中使用可滚动的文件列表。

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_527_1.png)

要获取软件包的信息，请在主软件包管理对话框中（如图 22.7 所示）选择信息行项并按 Enter。`lisa` 命令随后将查询系统 `rpm` 数据库并显示软件包名称列表，如图 22.11 所示。

### 图 22.11

要获取软件包的信息，请滚动已安装软件列表，选择文件并按 Enter。

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_528_0.png)

滚动列表并使用空格键选择软件包，然后按 Enter 查看软件包信息。此信息与 `rpm` 命令的 `-qi` 选项显示的内容完全相同。

> OpenLinux 还包括 Caldera Open Administration System，它为系统 `rpm` 数据库提供了另一个图形界面。COAS 需要 X11，并使用一个大型窗口，可用于安装和删除软件。

## 摘要

本小时向你介绍了 OpenLinux 文件系统的概念，即 Linux 目录和文件的组织方式。你还了解了不同的文件系统以及如何读取 OpenLinux 文件系统表，即 `/etc` 目录中的 `fstab`。此外，你还学习了如何读取和更改文件所有权和权限。你还了解了如何使用三种不同的实用程序查询、安装和删除系统上的软件。所有这些技能都是管理、维护和排除 OpenLinux 故障的重要组成部分。

### 问答

Q 我尝试使用 `fdformat` 命令格式化软盘。插入软盘后，输入命令并指定 `/dev/fd0` 设备，命令报告 Could not determine current format type: No such device。我知道我的软盘可用。发生了什么？

A 可能你在驱动器中没有插入软盘。如果在插入软盘的情况下出现此错误，则软盘不是空白的并且之前已格式化。执行低级格式化时最佳做法是指定设备的确切类型（如 `/dev/fd0H1440`），例如 `fdformat /dev/fd0H1440`。

Q 如何为我的 KDE 桌面创建文件夹 参见 "KDE (K Desktop Environment):desktop" 参见 "K Desktop Environment (KDE):desktop"，打开时显示我的 Windows 分区的内容？

A 挂载你的 Windows 分区 参见 "Windows partition:mounting" 然后在主目录的 Desktop 文件夹内创建一个名为 `dos` 之类的符号链接 参见 "symbolic links"。确保此链接指向 Windows 桌面文件夹——例如，`ln -s /mnt/dos/windows/desktop $HOME/Desktop/dos`。

### 练习

- 1. 格式化软盘，然后使用 Linux `ext2` 文件系统准备磁盘。挂载软盘并从主目录复制文件到磁盘。你使用了哪些实用程序？
