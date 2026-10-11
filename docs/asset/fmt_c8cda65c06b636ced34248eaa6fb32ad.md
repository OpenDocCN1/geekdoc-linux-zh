
使用`smbmount`命令，你可以将SMB服务器完全集成到你的Linux文件系统中。如果你以前用过`mount`命令，就会知道它让另一个文件系统表现得像根文件系统的一部分。例如，当你使用此命令时：

```bash
# mount /mnt/cdrom
```

你可以进入`/mnt/cdrom`目录并访问CD-ROM驱动器的内容，就像它是另一个子目录一样，而实际上它位于独立的设备上。这就是Linux文件系统的设计方式。

取决于你的系统设置，有时需要更完整的挂载命令。例如，你可以使用类似这样的命令访问远程NFS文件服务器：

```bash
# mount -t nfs sundance:/home/nwells /mnt/sundance
```

该命令指示了远程文件系统的类型（NFS）、远程服务器和路径以及作为挂载点（访问点）的本地路径。当然，你必须拥有通过NFS访问`sundance`服务器的权限，该命令才能正常工作。

NFS在跨UNIX系统共享文件方面非常好；由于Samba套件适用于许多平台，SMB是几乎所有跨平台文件共享的良好解决方案。Samba工具包包含一个名为`smbfs`的包，用于SMB文件系统。使用此包，你可以像挂载NFS文件系统或本地文件系统设备（如CD-ROM设备）一样挂载SMB文件系统。

![](img/35c1af90d4f3af9cd7cfd006c6b752f5_367_0.png)

> 注意：`smbfs`工具在Red Hat 7或安装之前提到的`samba-common`和`samba-client`包时默认安装。非Red Hat系统可能需要你加载内核模块。请使用命令`insmod smbfs`。

特殊的SMB挂载命令称为`smbmount`。该命令与`smbclient`命令类似，但可能需要额外的参数。命令的通用格式如下：

```bash
$ smbmount //servername/sharename /mnt/point -U username
```

在以下示例中，名为`sundance`的服务器上的共享被挂载到本地目录`/mnt/sundance`。这是以用户`nwells`的权限执行的，必须提示输入其密码。

```bash
$ smbmount //sundance/c /mnt/sundance -U nwells
```

Password:

作为`smbclient`，输入你在SMB服务器上的账户密码。如果此命令成功，你可以使用`cd`命令进入你指定的挂载点（示例中的`/mnt/sundance`），并开始访问远程SMB文件系统，就像它是你本地文件系统的一部分一样。

# 从 Linux 访问 Windows NT 服务器

由于远程SMB服务器现在是目录结构的一部分，因此你所有的标准文件管理工具都可以用于你的Windows共享。但这里有两点注意事项：

- 你只能执行Windows账户权限允许你执行的任务。例如，SMB (Windows) 服务器的管理员可能不允许你创建新文件或删除新文件。

- 你只能执行Windows文件系统（由SMB服务器和客户端进行映射）允许的任务。例如，你无法设置UNIX文件权限；SMB服务器使用的系统与UNIX不同。

在某些情况下，可能需要额外的参数才能让`smbmount`（甚至是`smbclient`）正常工作。例如，你可能会看到消息：“hostname too long as a netbios name”（作为NetBIOS名称主机过长）。在这种情况下，你可以像示例所示将客户端的主名添加到命令中：

```bash
$ smbmount //sundance/c /mnt/sundance -U nell -c bright
```

下一图显示了KDE 2中的一个文件管理器，其中在`/mnt/sundance`目录下挂载了一个Windows文件服务器，正如本文示例所示。你可能从所有的`.INI`和`.EXE`文件中看出，该结构属于标准的Windows系统。使用此接口，你可以在Windows与所有其他本地或挂载的文件系统（如NFS或FTP文件系统）之间拖放文件。

![](img/35c1af90d4f3af9cd7cfd006c6b752f5_368_0.png)

# 克隆 Windows NT

> 注意：使用`smbmount`挂载远程Windows系统是运行你想通过WINE执行的Windows应用程序的一种极方法。

一旦使用`smbmount`命令挂载了SMB文件系统，可以使用标准的`umount`命令将其卸载。例如：

```bash
# umount /mnt/sundance
```

> 注意：你也可以在`/etc/fstab`文件中添加条目，以便在启动时自动挂载SMB文件系统，就像处理本地或NFS文件系统一样。详情请参阅`mount`命令的man手册。

## 41 在 Linux 上克隆 Windows NT 服务器

在玩过Samba客户端工具后，你可能可能会在Linux上搭建自己的Samba服务器。许多系统管理员依赖运行Samba服务器的Linux机器作为整个Windows客户端网络的默认文件服务器。这种方式成本低且稳定性无与伦比。

Red Hat 7包含了Samba服务器软件包，但如果你选择的是工作站（Workstation）安装，默认不会安装。`samba`包包含在CD的`/Part10/Execute/Samba`目录下。你可以使用标准的`rpm`命令安装它。请记住，`samba`包是服务器端；`samba-client`包是客户端端（带有`smbclient-command`）。当你计划使用服务器或客户端时，应该安装`samba-common`包。

# 设置 Samba 服务器

Samba服务器套件包含在大多数Linux发行版中。如果你在安装Red Hat 7时没有包含`samba`包（通过使用命令`rpm -q samba`进行检查），可以使用此命令从Red Hat CD将其添加到你的系统中：

```bash
rpm -Uvh /mnt/cdrom/RedHat/RPMS/samba-2.0.7-21ss1.i386.rpm
```

此外，`/Part10/Execute/Samba`目录包含适用于各种系统的rpm格式存档，你可以在你的Linux副本上安装它们。CD上的`/Part10/Source/Samba`同时也包含了源码存档。

你可以使用以下命令检查安装了哪些Samba包：

```bash
$ rpm -qa | grep samba
```

如果你使用的是非Red Hat的Linux发行版，包名可能会有所不同，因此你可以尝试此命令：

```bash
$ rpm -qa | grep smb
```

如果你使用的是服务器类型的Linux安装，而不是我一直假设你使用的工作站类型安装，那么Samba服务器可能已经运行在你的Linux机器上了。

你可以通过以下命令判断Samba服务器是否正在运行，该命令会在你系统运行的进程列表中搜索包含`mbd`字母的进程。在这种情况下，你正在寻找Net-BEUI名称服务器`nmbd`和Samba共享管理守护进程`smbd`：

```bash
$ ps aux | grep smbd
root 556 0.0 2.1 1312 652 ? S 13:46 0:00 smbd -
root 558 0.0 1.9 1104 608 ? S 13:46 0:00 nmbd -
```

示例输出中出现的两行显示了正在运行的Samba组件。

> 注意：有一个问题是，Samba已安装并尝试在启动时运行，但如果没有有效的配置文件，它将会停止。请继续阅读本节以了解如何解决这个问题。

## 352 克隆 Windows NT

如果这些程序尚未在你的系统中运行，请按照本节中的配置步骤进行。配置完成后，按照所示步骤启动Samba服务器。然后你可以再次运行上面的`ps`命令检查服务器是否正在运行。

Red Hat 7上的Samba配置文件为`/etc/samba/smb.conf`。该文件将...

```ini
[printers]
comment = All Printers
path = /var/spool/samba
browseable = no
guest ok = no
writable = no
printable = yes
create mask = 0700
```

```ini
[public]
comment = Public Stuff
path = /home/public
browseable = yes
public = yes
writable = yes
printable = no
write List = @users
```

> **注意** 上述示例文件中的每个功能都是Red Hat 7默认设置的一部分。只是去掉所有注释后，内容看起来更直观了。
